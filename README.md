# 📚 Online Bookstore Database Management System

## 📌 Project Overview

The Online Bookstore Database Management System is a MySQL-based database project designed to efficiently manage books, customers, orders, order items, and admin information.

The main purpose of this project is to organize bookstore data, maintain relationships between different entities, perform efficient data retrieval, and ensure data integrity using relational database concepts.

The project was developed using MySQL and MySQL Workbench.

## 🎯 Objectives

- Manage book information efficiently.
- Store and manage customer details.
- Manage customer orders and order items.
- Maintain relationships between tables using Primary Keys and Foreign Keys.
- Perform data retrieval using SQL queries and JOIN operations.
- Use aggregate functions for data analysis.
- Implement stored procedures for reusable operations.
- Use transactions to maintain data consistency.
- Improve query performance using indexes.
- Implement basic database security using user privileges.

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| MySQL | Database Management System |
| MySQL Workbench | Database design, SQL execution and management |
| SQL | Data definition, manipulation and retrieval |
| GitHub | Project source code and documentation |

## 🗂️ Database Structure

The database contains five main tables:

### 1. Books

Stores information about books available in the bookstore.

**Columns:**
- `book_id` - Primary Key
- `title`
- `author`
- `price`
- `stock`
- `category`
- `publisher`

### 2. Customers

Stores customer information.

**Columns:**
- `customer_id` - Primary Key
- `name`
- `email`
- `phone`
- `address`
- `created_at`

### 3. Orders

Stores customer order information.

**Columns:**
- `order_id` - Primary Key
- `customer_id` - Foreign Key
- `order_date`
- `total_amount`
- `status`

### 4. Order_Items

Stores the books included in each order.

**Columns:**
- `order_item_id` - Primary Key
- `order_id` - Foreign Key
- `book_id` - Foreign Key
- `quantity`
- `subtotal`

### 5. Admins

Stores administrator account information.

**Columns:**
- `admin_id` - Primary Key
- `username` - Unique
- `password_hash`
- `role`

## 🔗 Table Relationships

The tables are connected using Primary Keys and Foreign Keys.

- `Customers.customer_id` → `Orders.customer_id`
- `Orders.order_id` → `Order_Items.order_id`
- `Books.book_id` → `Order_Items.book_id`

These relationships help maintain referential integrity and prevent invalid data relationships.

## 🔑 Database Concepts Used

### Primary Key

A Primary Key uniquely identifies each record in a table.

Example:

    customer_id INT PRIMARY KEY AUTO_INCREMENT

### Foreign Key

A Foreign Key creates a relationship between two tables and references the Primary Key of another table.

Example:

    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)

### Constraints

The project uses:

- PRIMARY KEY
- FOREIGN KEY
- NOT NULL
- UNIQUE
- DEFAULT
- AUTO_INCREMENT

## 🔍 SQL Operations

The project includes different SQL operations such as:

- SELECT
- INSERT
- UPDATE
- DELETE
- WHERE
- ORDER BY
- GROUP BY
- HAVING
- LIKE
- Aggregate Functions
- JOIN Operations

### Example: Books with Price Greater Than 10

    SELECT *
    FROM Books
    WHERE price > 10;

### Example: Count Books by Category

    SELECT category, COUNT(*)
    FROM Books
    GROUP BY category;

### Example: Average Book Price

    SELECT AVG(price)
    FROM Books;

## 🔗 JOIN Query

The project uses JOIN operations to retrieve information from multiple related tables.

    SELECT c.name, b.title, oi.quantity
    FROM Customers c
    JOIN Orders o
        ON c.customer_id = o.customer_id
    JOIN Order_Items oi
        ON o.order_id = oi.order_id
    JOIN Books b
        ON oi.book_id = b.book_id;

This query retrieves the customer name, book title, and quantity ordered.

## 📊 Aggregate Functions

The project uses aggregate functions for data analysis.

- `COUNT()` - Counts records
- `SUM()` - Calculates total values
- `AVG()` - Calculates average values
- `MAX()` - Finds the maximum value
- `MIN()` - Finds the minimum value

Example:

    SELECT SUM(stock)
    FROM Books;

## ⚙️ Stored Procedure

A stored procedure is used to retrieve all orders of a particular customer.

    DELIMITER //

    CREATE PROCEDURE GetCustomerOrders(IN p_customer_id INT)
    BEGIN
        SELECT 
            c.name AS customer_name,
            o.order_id,
            o.order_date,
            SUM(oi.subtotal) AS order_total
        FROM Customers c
        JOIN Orders o
            ON c.customer_id = o.customer_id
        JOIN Order_Items oi
            ON o.order_id = oi.order_id
        WHERE c.customer_id = p_customer_id
        GROUP BY c.name, o.order_id, o.order_date;
    END //

    DELIMITER ;

### Execute the Procedure

    CALL GetCustomerOrders(1);

## 💳 Transaction Management

Transactions are used to maintain data consistency.

    START TRANSACTION;

    UPDATE Books
    SET stock = stock - 1
    WHERE book_id = 1 AND stock > 0;

    COMMIT;

`COMMIT` permanently saves the changes.

`ROLLBACK` can be used to cancel uncommitted changes.

## 🚀 Indexing

Indexes are created to improve query performance.

    CREATE INDEX idx_orders_customer_id
    ON Orders(customer_id);

    CREATE INDEX idx_order_items_order_id
    ON Order_Items(order_id);

    CREATE INDEX idx_order_items_book_id
    ON Order_Items(book_id);

Indexes help the database retrieve frequently searched data faster.

## 🔐 Database Security

A separate database user is created with limited privileges.

    CREATE USER 'bookstore_user'@'localhost'
    IDENTIFIED BY 'Bookstore@123';

    GRANT SELECT, INSERT, UPDATE
    ON Books.*
    TO 'bookstore_user'@'localhost';

This follows the principle of giving users only the permissions they require.

## 📈 Key Features

- Book management
- Customer management
- Order management
- Order item management
- Admin management
- Relational database structure
- Primary and Foreign Key relationships
- SQL CRUD operations
- JOIN queries
- Aggregate functions
- GROUP BY and HAVING
- Stored procedures
- Transaction management
- Database indexing
- Basic database security

## ▶️ How to Run the Project

### Step 1: Install MySQL

Install MySQL Server and MySQL Workbench.

### Step 2: Open MySQL Workbench

Open MySQL Workbench and connect to the MySQL server.

### Step 3: Create the Database

    CREATE DATABASE Books;
    USE Books;

### Step 4: Create Tables

Execute the table creation queries for:

- Books
- Customers
- Orders
- Order_Items
- Admins

### Step 5: Insert Data

Insert the sample records into the tables.

### Step 6: Execute Queries

Run the SELECT, JOIN, aggregate, stored procedure, transaction, indexing, and security queries.

## 📁 Project Structure

    Online-Bookstore-Database/
    │
    ├── DUMP 2026 09 04.sql
    └── README.md

## 🧪 Testing and Verification

The database was tested using MySQL Workbench.

The following operations were verified:

- Database creation
- Table creation
- Data insertion
- Data retrieval
- Data updating
- JOIN operations
- Aggregate functions
- GROUP BY and HAVING
- Stored procedure execution
- Transaction operations
- Index creation
- User privilege management

## 🎓 Learning Outcomes

Through this project, I gained practical knowledge of:

- Relational database design
- SQL queries
- Primary and Foreign Keys
- Table relationships
- JOIN operations
- Aggregate functions
- Stored procedures
- Transactions
- Indexing
- Database security
- MySQL Workbench

## 📌 Conclusion

The Online Bookstore Database Management System provides a structured and efficient way to manage bookstore-related data. The project demonstrates important relational database concepts including table relationships, SQL queries, JOIN operations, stored procedures, transactions, indexing, and security.

This project helped me understand how a real-world bookstore database can be designed, implemented, and managed using MySQL.
