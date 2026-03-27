# Project Objetive

The primary objective of this system is to implement the backend business logic for a movie ticker reservation service.
The project aims to consolidate the design of relational data models, the management of complex relationships between
entities, concurrency control (to prevent overbooking when reserving seats), and execution of advanced queries.

---

## System Requirements

### 1. User Authentication and Authorization

* **Account Management:** The system must allow users to register and log in.
* **Roles:** There must be at least two roles: Administrator and Regular user.
* **Administrator Privileges:** The first administrator must be created using seed data (initial database data).
  * Only an administrator can promote another user to the administrator role.
  * Exclusive management of the movie catalog, showtimes, and system reports.
* **Regular User Privileges:** Ability to view showtimes and reserve seats.

### 2. Movie and Showtime Management (Administrators Only)
* **Catalog:** CRUD functionality (Create, Read, Update, Delete) for movies.
* **Movie Details:** Each record must contain the title, description, cover image (poster), and genre.
* **Schedule:** Movies must have assigned showtimes.

### 3. Reservation Management
* **Browsing:** Users must be able to view movies and their respective showtimes by filtering by a specific date.
* **Seat Selection:** The system must display available seats for a show and allow the user to select which ones they
wish to reserve.
* **Personal Management:** Users must be able to view their booking history and cancel bookings for future showings.
* **Reports (Administrators):** Administrators should have access to overall metrics, including the ability to view all
reservations, room occupancy, and revenue generated.

---

## User Stories

### Epic 1: User Management
* **US01:** As an anonymous user, I want to register on the platform so I can book movie tickets.
* **US02:** As a registered user, I want to log in with my credentials to access my account and my reservations.
* **US03:** As an administrator, I want to promote a regular user to the role of administrator to delegate system
management tasks.

### Epic 2: Catalog and Schedule Management
* **US04:** As an administrator, I want to add, edit, and delete movies to keep the catalog up to date.
* **US05:** As an administrator, I want to assign showtimes to movies to create the weekly schedule.

### Epic 3: Booking Process
* **US06:** As a user, I want to view the movies and showtimes available for a specific date to plan my outing.
* **US07:** As a user, I want to view the map of available and occupied seats for a showtime to choose where to sit.
* **US08:** As a user, I want to confirm the reservation of the selected seats to secure my spot at the showtime.

### Epic 4: Self-Service and Reports
* **US09:** As a user, I want to view a list of my active and past reservations to keep track of my tickets.
* **US10:** As a user, I want to cancel a reservation for a showing that has not yet taken place to release the seat if
I cannot attend.
* **US11:** As an administrator, I want to view a report of all reservations, the percentage of capacity, and revenue to
analyze the cinema's business performance.

---

## Technical and Design Considerations
To ensure the system's robustness, the implementation must take the following critical points into account:

* **Data Model:** Carefully design the entities (User, Role, Movie, Showtime, Seat, Reservation) and their 
relationships (1:N, N:M).
* **Database:** The use of a relational database engine such as PostgreSQL or MySQL is strongly recommended to ensure
referential integrity and ACID transactions.
* **Concurrency Management (Overbooking):** Implement transactional locking strategies (Pessimistic or Optimistic
Locking) in the database to ensure that two users cannot reserve the exact same seat at exactly the same time.
* **Security:** Properly implement authentication and role-based access control (RBAC) on all sensitive endpoints.

---

## Future Improvements

Once the core system is operational, the following iterations are planned to scale the platform:
* **Payment Gateway Integration:** Credit/debit card processing to collect payment for reservations in real time.
* **Automatic Notifications:** Sending transactional emails (or SMS) with the virtual ticket in QR format and reminders
prior to the show.
* **Multi-Theater Management:** Support for different sizes and layouts of movie theaters (e.g., 2D Theater, 3D Theater,
IMAX Theater).