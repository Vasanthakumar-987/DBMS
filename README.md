# 🛒 Amazon E-Commerce Database Design

![DBMS](https://img.shields.io/badge/DBMS-Project-blue)
![SQL](https://img.shields.io/badge/SQL-MySQL-orange)
![Normalization](https://img.shields.io/badge/Database-3NF-success)

## 📌 Project Overview

This project presents the database design of an Amazon-style E-Commerce platform developed as part of a **Database Management Systems (DBMS)** assignment.

The system models the core functionalities of an online shopping platform including:

- User Management
- Product Management
- Shopping Cart
- Orders
- Payments
- Reviews

The database was designed using **ER Modeling**, converted into a **Relational Schema**, and implemented using **SQL (DDL)**.

---

# 📑 Table of Contents

- Project Overview
- Objectives
- Functional Requirements
- Non-Functional Requirements
- Database Design
- ER Diagram
- Relational Schema
- SQL Implementation
- Database Normalization
- Conclusion

---

# 🎯 Objectives

- Design an E-Commerce database.
- Identify entities and relationships.
- Create an ER Diagram.
- Convert the ER model into Relational Schema.
- Implement the schema using SQL.
- Apply Third Normal Form (3NF).

---

# ⚙ Functional Requirements

### User Management

- Register
- Login
- Manage Profile

### Product Management

- View Products
- Search Products
- Filter Products

### Shopping Cart

- Add Product
- Remove Product
- Update Quantity

### Order Management

- Place Order
- View Order History
- Track Delivery

### Payment

- UPI
- Debit/Credit Card
- Net Banking
- Cash on Delivery

### Reviews

- Give Ratings
- Write Reviews

---

# 🔒 Non-Functional Requirements

- High Performance
- Secure Transactions
- Scalability
- Reliability
- High Availability
- User-Friendly Interface

---

# 🗂 Database Entities

| Entity | Description |
|----------|-------------|
| USER | Stores customer information |
| PRODUCT | Stores product details |
| CART | Stores user's shopping cart |
| CART_ITEM | Products inside cart |
| ORDERS | Stores customer orders |
| ORDER_ITEM | Products inside each order |
| PAYMENT | Payment information |
| REVIEW | Product ratings and comments |

---

# 🗄 Database Schema

| Table | Primary Key | Foreign Keys |
|--------|------------|--------------|
| USER | user_id | - |
| PRODUCT | product_id | - |
| CART | cart_id | user_id |
| CART_ITEM | cart_item_id | cart_id, product_id |
| ORDERS | order_id | user_id |
| ORDER_ITEM | order_item_id | order_id, product_id |
| PAYMENT | payment_id | order_id |
| REVIEW | review_id | user_id, product_id |

---

# 📊 ER Diagram

> Place your StarUML ER Diagram here.

```
ER-Diagram.png
```

![ER Diagram](ER-Diagram.png)

---

# 🔗 Relational Schema

```
USER(user_id, name, email, password)

PRODUCT(product_id, title, price, stock)

CART(cart_id, user_id)

CART_ITEM(cart_item_id, cart_id, product_id, quantity)

ORDERS(order_id, user_id, order_date, total_amount)

ORDER_ITEM(order_item_id, order_id, product_id, quantity, price)

PAYMENT(payment_id, order_id, payment_method, status)

REVIEW(review_id, user_id, product_id, rating, comment)
```

---

# 💻 SQL Implementation

```sql
CREATE TABLE USER (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);
```

Continue with the remaining SQL tables inside **amazon_database.sql**.

---

# ✅ Database Normalization

The database follows **Third Normal Form (3NF)**.

- No repeating groups
- No partial dependency
- No transitive dependency

This ensures:

- Data Integrity
- Reduced Redundancy
- Efficient Updates

---

# 🛠 Technologies Used

- MySQL
- SQL
- StarUML
- Markdown
- GitHub

---

# 📷 Project Preview

| ER Diagram | SQL |
|------------|-----|
| Add Screenshot | Add Screenshot |

---

# 📌 Conclusion

This project demonstrates the design of a normalized relational database for an Amazon-style E-Commerce platform.

The database supports customer management, product catalog, shopping cart, order processing, payments, and reviews while maintaining data integrity through proper normalization.

---

## 👨‍💻 Author

**Name:** Your Name

**Register Number:** Your Register Number

**Department:** Your Department

**College:** Your College
