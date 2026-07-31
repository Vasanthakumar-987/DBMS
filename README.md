# 🛒 Amazon E-Commerce Database Design

![DBMS](https://img.shields.io/badge/DBMS-Project-blue)
![SQL](https://img.shields.io/badge/SQL-MySQL-orange)
![Normalization](https://img.shields.io/badge/Database-3NF-success)

### DBMS Assignment: Requirements, ER Diagram and Relational Schema

**Prepared by:** Vasanthakumar 
**Register Number:** [Your Register Number]  
**Programme / Department:** [Your Department/Degree, e.g., B.Sc. AI & DS]  
**Institution:** [Your College / University Name]  

---

## 📌 Project Overview

This project presents a structured database design for an Amazon-style E-Commerce platform developed as part of the **Database Management Systems (DBMS)** coursework.

The system models core online shopping functionalities, including User Management, Product Catalogs, Shopping Carts, Order Processing, Payments, and Customer Reviews. The conceptual design was created using **StarUML**, converted into a **3NF Relational Schema**, and fully defined using **SQL (DDL)**.

*Note: This is an academic database model created for learning purposes and does not represent Amazon's actual enterprise database.*

---

## 📑 Table of Contents

- [Objectives](#-objectives)
- [Functional Requirements](#-functional-requirements)
- [Non-Functional Requirements](#-non-functional-requirements)
- [Database Entities & Schema Matrix](#-database-entities--schema-matrix)
- [ER Diagram](#-er-diagram)
- [Relational Schema](#-relational-schema)
- [SQL Schema Implementation](#-sql-schema-implementation)
- [Database Normalization](#-database-normalization)
- [Technologies Used](#-technologies-used)
- [Conclusion](#-conclusion)

---

## 🎯 Objectives

- Design an efficient relational database for an e-commerce ecosystem.
- Identify key system entities, attributes, primary keys, and foreign keys.
- Create an Entity-Relationship (ER) Diagram using Crow's Foot notation in StarUML.
- Convert the conceptual ER model into a normalized Relational Schema.
- Implement the complete schema using SQL Data Definition Language (DDL).
- Ensure data integrity and eliminate redundancy by applying Third Normal Form (3NF).

---

## ⚙ Functional Requirements

### 1. User Management
- Customer Registration & Login Authentication.
- User Profile management (Name, Email, Password).

### 2. Product Management
- Browse product catalog with titles, pricing, and stock levels.
- Search and filter products efficiently.

### 3. Shopping Cart
- Manage customer carts (Add products, remove items, update quantities).

### 4. Order Management
- Checkout cart items to place orders.
- Record order placement dates and total transaction amounts.

### 5. Payment System
- Support multiple payment modes (UPI, Credit/Debit Cards, Net Banking, COD).
- Track transaction status (e.g., Pending, Completed).

### 6. Review & Rating
- Submit ratings and detailed text comments on purchased products.

---

## 🔒 Non-Functional Requirements

- **High Performance:** Optimized schema for low-latency query execution.
- **Data Security:** Protected user password storage and structured constraints.
- **Scalability:** Flexible relational layout to easily extend with new features.
- **Reliability:** Strict foreign key integrity constraints to prevent orphaned records.
- **High Availability:** Lightweight layout designed for quick recovery and continuous uptime.
- **Usability:** Intuitive entity architecture mapping directly to real-world workflows.

---

## 🗂 Database Entities & Schema Matrix

| Entity | Primary Key (PK) | Foreign Keys (FK) | Description |
| :--- | :--- | :--- | :--- |
| **USER** | `user_id` | *None* | Stores customer registration and credential details |
| **PRODUCT** | `product_id` | *None* | Stores item catalog, pricing, and available stock |
| **CART** | `cart_id` | `user_id` | Links a unique shopping cart to a customer |
| **CART_ITEM** | `cart_item_id` | `cart_id`, `product_id` | Holds specific quantities of items added to a cart |
| **ORDERS** | `order_id` | `user_id` | Tracks order dates, buyer IDs, and total costs |
| **ORDER_ITEM** | `order_item_id` | `order_id`, `product_id` | Stores individual line-items inside an order |
| **PAYMENT** | `payment_id` | `order_id` | Records payment methods and transaction status |
| **REVIEW** | `review_id` | `user_id`, `product_id` | Stores user ratings and product feedback |

---

## 📊 ER Diagram

The ER diagram was modeled in StarUML using **Crow's Foot Notation** to represent primary keys, foreign keys, and cardinalities:

![ER Diagram](./er-diagram.png)

---

## 🔗 Relational Schema

Below is the normalized relational database schema derived from the ER diagram:

> **Key:** **`Bold & Underlined`** = Primary Key (PK) | *Italics* = Foreign Key (FK)

- **USER** (**`user_id`**, name, email, password)
- **PRODUCT** (**`product_id`**, title, price, stock)
- **CART** (**`cart_id`**, *user_id*)
- **CART_ITEM** (**`cart_item_id`**, *cart_id*, *product_id*, quantity)
- **ORDERS** (**`order_id`**, *user_id*, order_date, total_amount)
- **ORDER_ITEM** (**`order_item_id`**, *order_id*, *product_id*, quantity, price)
- **PAYMENT** (**`payment_id`**, *order_id*, payment_method, status)
- **REVIEW** (**`review_id`**, *user_id*, *product_id*, rating, comment)

---

## 💻 SQL Schema Implementation

Complete DDL Script to instantiate the database schema:

```sql
-- 1. Create USER Table
CREATE TABLE USER (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);

-- 2. Create PRODUCT Table
CREATE TABLE PRODUCT (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(150) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0
);

-- 3. Create CART Table
CREATE TABLE CART (
    cart_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT UNIQUE,
    FOREIGN KEY (user_id) REFERENCES USER(user_id) ON DELETE CASCADE
);

-- 4. Create CART_ITEM Table
CREATE TABLE CART_ITEM (
    cart_item_id INT PRIMARY KEY AUTO_INCREMENT,
    cart_id INT,
    product_id INT,
    quantity INT DEFAULT 1,
    FOREIGN KEY (cart_id) REFERENCES CART(cart_id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id) ON DELETE CASCADE
);

-- 5. Create ORDERS Table
CREATE TABLE ORDERS (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (user_id) REFERENCES USER(user_id) ON DELETE CASCADE
);

-- 6. Create ORDER_ITEM Table
CREATE TABLE ORDER_ITEM (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT DEFAULT 1,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES ORDERS(order_id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id) ON DELETE CASCADE
);

-- 7. Create PAYMENT Table
CREATE TABLE PAYMENT (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT UNIQUE,
    payment_method VARCHAR(50) NOT NULL,
    status VARCHAR(30) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES ORDERS(order_id) ON DELETE CASCADE
);

-- 8. Create REVIEW Table
CREATE TABLE REVIEW (
    review_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    product_id INT,
    rating INT,
    comment TEXT,
    FOREIGN KEY (user_id) REFERENCES USER(user_id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id) ON DELETE CASCADE
);
