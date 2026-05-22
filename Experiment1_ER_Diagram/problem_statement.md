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

<img width="888" height="325" alt="image" src="https://github.com/user-attachments/assets/f568bfb0-b48a-41fb-bbe7-1ba714c8a4d1" />


### Entities and Attributes

| Entity     | Attributes (PK, FK)                                                              | Notes                         |
| ---------- | -------------------------------------------------------------------------------- | ----------------------------- |
| Member     | **Member_ID (PK)**, Name, Membership_Type, Start_Date                            | Stores details of gym members |
| Program    | **Program_ID (PK)**, Program_Name, Duration                                      | Example: Yoga, Zumba          |
| Trainer    | **Trainer_ID (PK)**, Trainer_Name, Specialization                                | Trainer information           |
| Session    | **Session_ID (PK)**, Session_Date, Session_Time, Trainer_ID (FK), Member_ID (FK) | Personal training session     |
| Attendance | **Attendance_ID (PK)**, Session_ID (FK), Member_ID (FK), Status                  | Tracks attendance             |
| Payment    | **Payment_ID (PK)**, Member_ID (FK), Amount, Payment_Date, Payment_Type          | Membership or session payment |


### Relationships and Constraints

| Relationship         | Cardinality  | Participation     | Notes                                |
| -------------------- | ------------ | ----------------- | ------------------------------------ |
| Member – Program     | Many to Many | Partial           | Members can join multiple programs   |
| Program – Trainer    | Many to Many | Total for Program | A program may have multiple trainers |
| Member – Session     | One to Many  | Partial           | Member can book many sessions        |
| Trainer – Session    | One to Many  | Total             | Trainer conducts sessions            |
| Session – Attendance | One to Many  | Total             | Attendance recorded per session      |
| Member – Payment     | One to Many  | Partial           | Member makes payments                |


### Assumptions

* A member can enroll in multiple fitness programs.

* Each program may have more than one trainer.

* Personal training sessions are optional.

* Payments include both membership and personal session fees.

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

<img width="758" height="314" alt="image" src="https://github.com/user-attachments/assets/290e8582-72bb-4e32-a773-aaa77e6327ca" />


### Entities and Attributes

| Entity  | Attributes (PK, FK)                                                    | Notes                          |
| ------- | ---------------------------------------------------------------------- | ------------------------------ |
| Member  | **Member_ID (PK)**, Name, Address, Phone                               | Library member                 |
| Book    | **Book_ID (PK)**, Title, Author, Category                              | Book information               |
| Loan    | **Loan_ID (PK)**, Member_ID (FK), Book_ID (FK), Loan_Date, Return_Date | Borrowing record               |
| Event   | **Event_ID (PK)**, Event_Name, Event_Date                              | Cultural events                |
| Speaker | **Speaker_ID (PK)**, Name, Expertise                                   | Event speakers                 |
| Room    | **Room_ID (PK)**, Room_Name, Capacity                                  | Rooms used for events or study |
| Fine    | **Fine_ID (PK)**, Loan_ID (FK), Amount                                 | Overdue fine details           |

### Relationships and Constraints

| Relationship    | Cardinality  | Participation | Notes                               |
| --------------- | ------------ | ------------- | ----------------------------------- |
| Member – Loan   | One to Many  | Partial       | Member can borrow many books        |
| Book – Loan     | One to Many  | Partial       | Book can be borrowed multiple times |
| Member – Event  | Many to Many | Partial       | Members register for events         |
| Event – Speaker | Many to Many | Total         | Events may have multiple speakers   |
| Event – Room    | Many to One  | Total         | Event conducted in a room           |
| Loan – Fine     | One to One   | Partial       | Fine only if book returned late     |


### Assumptions

* A member can borrow multiple books at different times.

* Books can be borrowed by different members over time.

* Events may have multiple speakers.

* Fines are generated only if the return date exceeds the due date.

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

<img width="541" height="399" alt="image" src="https://github.com/user-attachments/assets/d046d67c-3647-4890-9845-fa8c2591ac73" />


### Entities and Attributes

| Entity      | Attributes (PK, FK)                                                 | Notes               |
| ----------- | ------------------------------------------------------------------- | ------------------- |
| Customer    | **Customer_ID (PK)**, Name, Phone                                   | Customer details    |
| Reservation | **Reservation_ID (PK)**, Customer_ID (FK), Date, Time, No_of_Guests | Table reservation   |
| Table       | **Table_ID (PK)**, Table_Number, Capacity                           | Restaurant table    |
| Order       | **Order_ID (PK)**, Reservation_ID (FK), Order_Time                  | Food order          |
| Dish        | **Dish_ID (PK)**, Dish_Name, Price, Category                        | Food items          |
| Bill        | **Bill_ID (PK)**, Reservation_ID (FK), Total_Amount, Service_Charge | Billing information |
| Waiter      | **Waiter_ID (PK)**, Name                                            | Waiter assigned     |


### Relationships and Constraints

| Relationship           | Cardinality  | Participation | Notes                               |
| ---------------------- | ------------ | ------------- | ----------------------------------- |
| Customer – Reservation | One to Many  | Partial       | Customer may reserve multiple times |
| Reservation – Table    | Many to One  | Total         | Reservation assigned to table       |
| Reservation – Order    | One to Many  | Total         | Multiple orders per reservation     |
| Order – Dish           | Many to Many | Total         | Order contains multiple dishes      |
| Reservation – Bill     | One to One   | Total         | One bill per reservation            |
| Waiter – Reservation   | One to Many  | Partial       | Waiter serves reservations          |


### Assumptions

* Walk-in customers are treated as reservations created at the time of arrival.

* Each reservation is assigned one table.

* An order may contain multiple dishes.

* Service charges are included in the bill.

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
