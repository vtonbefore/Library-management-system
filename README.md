# Library-management-system
# Library Management System Database

## Project Description
This is a complete MySQL database for a Library Management System. It includes all necessary tables, relationships, and constraints to manage library operations including book cataloging, member management, loans, reservations, and fines.

## Features
- Member management with membership status tracking
- Comprehensive book catalog with author and publisher information
- Loan tracking with due dates and return status
- Fine calculation system for overdue books
- Reservation system for high-demand books
- Staff management for library personnel

## ER Diagram
![ER Diagram](er_diagram.png)  
[Link to ERD](#) <!-- Replace with your actual link -->

## Setup Instructions

1. **Prerequisites**:
   - MySQL Server installed
   - MySQL Workbench or similar client (optional)

2. **Installation**:
   - Clone this repository
   - Run the SQL script in your MySQL environment:
     ```
     mysql -u username -p < library_management.sql
     ```

3. **Usage**:
   - Connect to the database using your preferred MySQL client
   - Execute queries against the database

## Sample Queries

```sql
-- Find all books currently on loan
SELECT b.title, m.first_name, m.last_name, l.due_date 
FROM loans l
JOIN books b ON l.book_id = b.book_id
JOIN members m ON l.member_id = m.member_id
WHERE l.status = 'On Loan';

-- Calculate total fines for a member
SELECT m.first_name, m.last_name, SUM(f.amount) as total_fines
FROM fines f
JOIN loans l ON f.loan_id = l.loan_id
JOIN members m ON l.member_id = m.member_id
WHERE f.status = 'Pending'
GROUP BY m.member_id;
