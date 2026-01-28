# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="544" height="186" alt="image" src="https://github.com/user-attachments/assets/ed3e6913-458d-4007-bda4-d024d52f5b5e" />


### Entities and Attributes

| **Entity**     | **Attributes (PK, FK)**                                                 | **Notes**                 |
| -------------- | ----------------------------------------------------------------------- | ------------------------- |
| **Member**     | MemberID **(PK)**, Name, MembershipType, StartDate                      | Gym members               |
| **Trainer**    | TrainerID **(PK)**, Name, Specialization                                | Gym trainers              |
| **Program**    | ProgramID **(PK)**, ProgramName, Schedule                               | Yoga, Zumba, etc.         |
| **Session**    | SessionID **(PK)**, Date, Time, MemberID **(FK)**, TrainerID **(FK)**   | Personal training         |
| **Attendance** | AttendanceID **(PK)**, SessionID **(FK)**, Status                       | Present / Absent          |
| **Payment**    | PaymentID **(PK)**, Amount, Date, MemberID **(FK)**, SessionID **(FK)** | Membership / session fees |


### Relationships and Constraints

| Relationship       | Cardinality | Participation | Notes                         |
| ------------------ | ----------- | ------------- | ----------------------------- |
| Member–Program     | M:N         | Partial       | Member may join many programs |
| Trainer–Program    | M:N         | Total         | Program needs trainers        |
| Member–Session     | 1:M         | Partial       | Optional sessions             |
| Session–Attendance | 1:M         | Total         | Attendance mandatory          |
| Member–Payment     | 1:M         | Total         | Payments tracked              |

### Assumptions
A member can exist without joining a program

Payments can be for membership or sessions

Attendance recorded only for booked sessions
---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="715" height="201" alt="image" src="https://github.com/user-attachments/assets/d30fedc9-6192-487b-8b49-cc36ccf080de" />


### Entities and Attributes

| Entity  | Attributes (PK, FK)                                                       | Notes              |
| ------- | ------------------------------------------------------------------------- | ------------------ |
| Member  | MemberID **(PK)**, Name, Contact                                          | Library members    |
| Book    | BookID **(PK)**, Title, Author, Category                                  | Library books      |
| Loan    | LoanID **(PK)**, LoanDate, ReturnDate, MemberID **(FK)**, BookID **(FK)** | Borrow record      |
| Event   | EventID **(PK)**, EventName, Date                                         | Cultural events    |
| Speaker | SpeakerID **(PK)**, Name                                                  | Authors / speakers |
| Room    | RoomID **(PK)**, Capacity                                                 | Rooms              |
| Fine    | FineID **(PK)**, Amount, LoanID **(FK)**                                  | Late return fines  |


### Relationships and Constraints
| Relationship  | Cardinality | Participation | Notes               |
| ------------- | ----------- | ------------- | ------------------- |
| Member–Book   | M:N         | Partial       | Borrowing optional  |
| Member–Event  | M:N         | Partial       | Event registration  |
| Event–Speaker | M:N         | Total         | Event needs speaker |
| Event–Room    | 1:1         | Total         | Mandatory room      |
| Loan–Fine     | 1:0..1      | Partial       | Only if overdue     |

### Assumptions
A book can be borrowed by only one member at a time

Fine applies only after due date

One room per event

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="591" height="257" alt="image" src="https://github.com/user-attachments/assets/720dd728-fa4f-4e1a-9b2c-84b7c24c6bb9" />


### Entities and Attributes
| Entity      | Attributes (PK, FK)                                             | Notes                    |
| ----------- | --------------------------------------------------------------- | ------------------------ |
| Customer    | CustomerID **(PK)**, Name, Phone                                | Walk-in or reserved      |
| Reservation | ReservationID **(PK)**, Date, Time, Guests, CustomerID **(FK)** | Booking details          |
| Table       | TableID **(PK)**, Capacity                                      | Dining tables            |
| Order       | OrderID **(PK)**, ReservationID **(FK)**                        | Food orders              |
| Dish        | DishID **(PK)**, DishName, Price, CategoryID **(FK)**           | Menu items               |
| Category    | CategoryID **(PK)**, CategoryName                               | Starter / Main / Dessert |
| Bill        | BillID **(PK)**, TotalAmount, ReservationID **(FK)**            | Final bill               |
| Waiter      | WaiterID **(PK)**, Name                                         | Staff                    |



### Relationships and Constraints

| Relationship         | Cardinality | Participation | Notes                  |
| -------------------- | ----------- | ------------- | ---------------------- |
| Customer–Reservation | 1:M         | Partial       | Walk-ins allowed       |
| Reservation–Table    | M:1         | Total         | Table required         |
| Reservation–Order    | 1:M         | Partial       | Orders optional        |
| Order–Dish           | M:N         | Total         | Multiple dishes        |
| Dish–Category        | M:1         | Total         | Every dish categorized |
| Reservation–Bill     | 1:1         | Total         | Mandatory billing      |
| Waiter–Reservation   | 1:M         | Partial       | Assigned waiter        |

### Assumptions
One bill per reservation

Walk-in customers create immediate reservations

A waiter can handle multiple reservations

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
