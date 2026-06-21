# Football Ticket Booking System Database

## Overview

This project implements a Football Ticket Booking System database using SQL. The system manages football fans, ticket managers, football matches, and ticket booking transactions. It demonstrates database design concepts including table creation, constraints, relationships, data seeding, and SQL querying.

---

## Database Schema

The database consists of three tables:

### 1. Users

Stores information about registered users of the platform.

| Column       | Description                                |
| ------------ | ------------------------------------------ |
| user_id      | Unique identifier for each user            |
| full_name    | User's full name                           |
| email        | Unique email address                       |
| role         | User role (Football Fan or Ticket Manager) |
| phone_number | Contact phone number                       |

### 2. Matches

Stores information about football matches.

| Column              | Description                      |
| ------------------- | -------------------------------- |
| match_id            | Unique identifier for each match |
| fixture             | Teams participating in the match |
| tournament_category | Tournament name                  |
| base_ticket_price   | Base ticket price                |
| match_status        | Match availability status        |

### 3. Bookings

Stores ticket booking information.

| Column         | Description                |
| -------------- | -------------------------- |
| booking_id     | Unique booking identifier  |
| user_id        | Reference to Users table   |
| match_id       | Reference to Matches table |
| seat_number    | Assigned seat number       |
| payment_status | Payment status             |
| total_cost     | Total booking cost         |

---

## Entity Relationship Diagram (ERD)

### Relationships

- One User can have many Bookings.
- One Match can have many Bookings.
- Each Booking belongs to exactly one User.
- Each Booking belongs to exactly one Match.

```text
Users (1) --------< Bookings >-------- (1) Matches
```

---

## Constraints Implemented

### Users Table

- Primary Key: `user_id`
- Unique Constraint: `email`
- Check Constraint:
  - role must be:
    - Football Fan
    - Ticket Manager

### Matches Table

- Primary Key: `match_id`
- Check Constraints:
  - base_ticket_price >= 0
  - match_status must be one of:
    - Available
    - Selling Fast
    - Sold Out
    - Postponed

### Bookings Table

- Primary Key: `booking_id`
- Foreign Keys:
  - user_id → Users(user_id)
  - match_id → Matches(match_id)

- Check Constraints:
  - total_cost >= 0
  - payment_status must be one of:
    - Pending
    - Confirmed
    - Cancelled
    - Refunded
    - NULL

---

## Sample Data

The database is seeded with:

- 4 Users
- 5 Matches
- 5 Booking Records

This sample data is used to test the required SQL queries.

---

## SQL Queries Implemented

### Query 1

Retrieve all available Champions League matches.

### Query 2

Find users whose names start with "Tanvir" or contain "Haque".

### Query 3

Retrieve bookings with missing payment status using `COALESCE`.

### Query 4

Display booking details with user names and match fixtures using `INNER JOIN`.

### Query 5

Display all users and their bookings using `LEFT JOIN`, including users without bookings.

### Query 6

Find bookings with a total cost greater than the average booking cost.

### Query 7

Retrieve the top 2 most expensive matches while skipping the most expensive match using `OFFSET` and `LIMIT`.

---

## Technologies Used

- PostgreSQL
- SQL (DDL & DML)
- Relational Database Design
- ERD Modeling

---

## How to Run

1. Create a PostgreSQL database.
2. Open the provided `QUERY.sql` file.
3. Execute the script.
4. The script will:
   - Drop existing tables if they exist.
   - Create all required tables.
   - Apply constraints.
   - Insert sample data.
   - Execute all assignment queries.
