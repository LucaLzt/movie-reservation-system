# Data Models and Architecture
By implementing **Spring Modulith** as the underlying architecture, the system is logically divided into several
cohesive, decoupled modules. This document details each module, its responsibilities, and its integrating data models.

## Module: Identity
Handles user management, role-based access control (RBAC), JWT generation and validation, registration, login, and user 
promotion operations. It exposes internal ports (APIs) allowing other modules to query the identity context without 
coupling to its internal implementation.

* **User:** `id` (UUID), `email` (String), `password_hash` (String), `role` (Enum), `created_at` (Timestamp).
* **Role:** Enum con  `ADMIN`, `USER`.

## Module: Catalog
Manages the movie catalog. It exposes CRUD operations exclusively for administrators. Poster image uploads are 
abstracted and delegated to the `Storage` module via the `ImageStorageFacade`.

* **Movie:** `id` (UUID), `title` (String), `description` (Text), `genre` (String), `poster_key` (String), 
`active` (Boolean).
* **Genre:** List of categories (`List<String>`).

## Module: Scheduling
Manages the `Room` and `Showtime` entities. The initial database seed loads the cinema rooms and their corresponding 
physical seats. This module is responsible for querying available showtimes for a specific date and determining seat 
availability for each function.

* **Showtime:** `id` (UUID), `movie_id` (UUID), `room_id` (UUID), `starts_at` (Timestamp), `price` (Decimal).
* **Room:** `id` (UUID), `name` (String), `capacity` (Integer).
* **Seat:** `id` (UUID), `room_id` (UUID), `row_label` (String), `number` (Integer).

## Module: Reservation
The core of the system and the most business-critical module. It manages `Booking` and `BookingSeat`. Overbooking 
prevention is strictly handled using **Pessimistic Locking** at the Seat level: when a user attempts to make a 
reservation, a `SELECT ... FOR UPDATE` is executed on the involved seats within a database transaction. This module 
publishes domain events (e.g., `BookingConfirmed`, `BookingCancelled`) so that the `Notifications` module can listen 
asynchronously without tight coupling.

* **Booking:** `id` (UUID), `user_id` (UUID), `showtime_id` (UUID), `status` (Enum), `total_amount` (Decimal), 
`created_at` (Timestamp).
* **BookingSeat:** `booking_id` (UUID), seat_id (UUID).
* **BookingStatus:** Enum containing `PENDING`, `CONFIRMED`, `CANCELLED`.

## Module: Storage
Acts as an infrastructure adapter for MinIO (or any S3-compatible storage). It exposes an `ImageStorageFacade` with 
three main operations: `upload`, `delete`, and `getPresignedUrl`. The `Catalog` module consumes this facade with zero 
knowledge of the underlying MinIO implementation.

## Module: Reporting
A read-only module restricted to administrators. It consumes the internal ports of the `Reservation` and`Scheduling` 
modules to aggregate data and generate cinema occupancy and revenue reports.

## Module: Notifications
_(Planned for a future iteration)_. Will listen to domain events published by the `Reservation` module to trigger 
asynchronous email or push notifications.