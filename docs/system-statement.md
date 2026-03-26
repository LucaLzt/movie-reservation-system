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

## Future Improvements

Once the core system is operational, the following iterations are planned to scale the platform:
* **Payment Gateway Integration:** Credit/debit card processing to collect payment for reservations in real time.
* **Automatic Notifications:** Sending transactional emails (or SMS) with the virtual ticket in QR format and reminders
prior to the show.
* **Multi-Theater Management:** Support for different sizes and layouts of movie theaters (e.g., 2D Theater, 3D Theater,
IMAX Theater).