# Car Dealership Database — Design & Development

A relational database for a car dealership that manages **sales**, **service tickets**, **customers**, and **GDPR-aware personal data**.  
Core deliverables include the **ERD**, **Data Dictionary**, **Test Plan**, and **SQL scripts** (table creation, data load, stored procedures, MI views, and GDPR delete logic).

---

## 1) Project Assets

- **ERD & Data Dictionary**: Conceptual + logical design, table attributes, PK/FK, and relationships.  
- **Test Plan**: FK violation tests and expected vs actual results.  
- **SQL**: **Create tables, insert data, stored procedures, MI views, GDPR transaction logic**.


## 2) ERD Overview (High-level)

**Main entities & relationships**

## ERD Cardinalities (Table)

| #  | Relationship                       | Cardinality            | Read as                           |
|----|------------------------------------|------------------------|-----------------------------------|
| 1  | Customer — Invoice                 | One-to-Many (1:N)      | Customer (1) → Invoices (N)       |
| 2  | Employee — Invoice                 | One-to-Many (1:N)      | Employee (1) → Invoices (N)       |
| 3  | Car — Invoice                      | One-to-Many (1:N)      | Car (1) → Invoices (N)            |
| 4  | Customer — TicketSystem            | One-to-Many (1:N)      | Customer (1) → Tickets (N)        |
| 5  | Employee — TicketSystem            | One-to-Many (1:N)      | Employee (1) → Tickets (N)        |
| 6  | Car — TicketSystem                 | One-to-Many (1:N)      | Car (1) → Tickets (N)             |
| 7  | Model — Car                        | One-to-Many (1:N)      | Model (1) → Cars (N)              |
| 8  | Make — Car                         | One-to-Many (1:N)      | Make (1) → Cars (N)               |
| 9  | Customer — CustPersonalDetails     | One-to-One (1:1)       | Customer (1) ↔ CustPersonalDetails (1) |
| 10 | TicketSystem — Parts               | Many-to-Many (M:N)     | Tickets (M) ↔ Parts (N)           |




<img width="1031" height="619" alt="image" src="https://github.com/user-attachments/assets/2c0c7804-730d-4556-ab04-6305d246bf67" />


---

## 3) **Test Plan**:
<img width="738" height="530" alt="image" src="https://github.com/user-attachments/assets/79d4257a-7a75-4719-9966-f1e42ef50618" />



## 4) Getting Started with SQL Server

1. Create a SQL Server database (e.g., `CarDealership`).
2. Run `sql/01_create_tables.sql` then `sql/02_insert_seed_data.sql`.
3. (Optional) Run `sql/03_stored_procedures.sql` and `sql/04_views.sql`.
4. Validate with `sql/05_test_queries.sql` and the **Test Plan**.

---

## 5) Key SQL — Examples From This Project

### a) DDL (Data Definition Language)
Create core tables with PK/FK relationships.



1.






<img width="226" height="406" alt="image" src="https://github.com/user-attachments/assets/a472c3a5-a429-4428-ac9b-b802248f28ae" />








2.





<img width="231" height="256" alt="image" src="https://github.com/user-attachments/assets/87d5daaa-e91c-4635-8aa6-a383fea05e13" />







3.




<img width="210" height="177" alt="image" src="https://github.com/user-attachments/assets/622306f7-98eb-4876-94bd-a81773be875f" />







4.




<img width="269" height="233" alt="image" src="https://github.com/user-attachments/assets/10c2ec72-2be6-4d81-ad70-084cc5c46cdf" />





### b) DQL (Data Query Language)
Example of insert seed data 

<img width="512" height="350" alt="image" src="https://github.com/user-attachments/assets/1bbdefc3-5141-417e-9d66-3b79c1101573" />


### c) DML (Data Manipulation Language)
Selects,joins and reporting views


<img width="265" height="406" alt="image" src="https://github.com/user-attachments/assets/811f83c0-1904-43b0-b5b0-a874dbf8f5cf" />


### d) TCL (Transaction Control Language)
GDPR-aware delete that keeps business-critical data but removes personal data; uses explicit transaction with TRY…CATCH.


<img width="326" height="480" alt="image" src="https://github.com/user-attachments/assets/9fff3655-71db-4a8e-b2cb-61d408c80875" />

### e) DCL (Data Control Language) 
example of grant read access on reporting views(SQL code)-

CREATE ROLE reporting_reader;

GRANT SELECT ON OBJECT::dbo.MI_Extract TO reporting_reader;

-- EXEC sp_addrolemember 'reporting_reader', 'YourLoginOrUser';

