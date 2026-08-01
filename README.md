# 🛒 Amazon E-Commerce Database Design

![DBMS](https://img.shields.io/badge/DBMS-Project-blue?style=for-the-badge&logo=mysql)
![SQL](https://img.shields.io/badge/SQL-MySQL-orange?style=for-the-badge&logo=mysql)
![Normalization](https://img.shields.io/badge/Database-3NF%20Normalized-success?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

### 🎓 DBMS Academic Project

- **Prepared by:** Vasanthakumar  
- **Register Number:** `[Your Register Number]`  
- **Programme / Department:** `[Your Department/Degree, e.g., B.Sc. AI & DS]`  
- **Institution:** `[Your College / University Name]`  

---

## 📌 Project Overview

This repository features a complete relational database design for an **Amazon-style E-Commerce Platform** developed as part of the **Database Management Systems (DBMS)** coursework.

The database models core operational workflows including **User Management**, **Product Catalogs**, **Shopping Carts**, **Order Processing**, **Payments**, and **Customer Reviews**. Developed conceptually using **StarUML**, converted into a **3NF Relational Schema**, and fully implemented using **SQL Data Definition Language (DDL)**.

> ℹ️ **Note:** *This is an academic schema created for educational purposes and does not represent Amazon's proprietary enterprise architecture.*

---

## 📑 Table of Contents

- [📌 Project Overview](#-project-overview)
- [🎯 Objectives](#-objectives)
- [⚙️ Functional Requirements](#️-functional-requirements)
- [🔒 Non-Functional Requirements](#-non-functional-requirements)
- [🗂 Database Entities \& Schema Matrix](#-database-entities--schema-matrix)
- [📊 ER Diagram](#-er-diagram)
- [🔗 Relational Schema](#-relational-schema)
- [💻 SQL Schema Implementation](#-sql-schema-implementation)
- [📐 Database Normalization (3NF)](#-database-normalization-3nf)
- [🛠 Technologies Used](#-technologies-used)
- [🏁 Conclusion](#-conclusion)

---

## 🎯 Objectives

* **Conceptual Modeling:** Identify key business entities, relationships, attributes, primary keys, and foreign keys.
* **Diagrammatic Representation:** Build a clear Entity-Relationship (ER) Diagram using **Crow's Foot Notation** in StarUML.
* **Relational Mapping:** Convert the ER model into an optimized Relational Schema.
* **Database Implementation:** Write robust, production-ready SQL (DDL) scripts with foreign key cascading rules.
* **Data Integrity:** Eliminate redundant data and anomaly risks by adhering strictly to **Third Normal Form (3NF)** rules.

---

## ⚙️ Functional Requirements

### 1. 👤 User Management
- User registration, login authentication, and profile updates (`user_id`, `name`, `email`, `password`).

### 2. 📦 Product Catalog
- Product browsing with structured titles, unit pricing, and real-time inventory tracking (`stock`).

### 3. 🛒 Shopping Cart System
- Dynamic cart management enabling users to add, remove, or modify product quantities.

### 4. 🛍️ Order Management
- Order placement conversion from cart items, retaining historical unit prices and transaction totals.

### 5. 💳 Payment Processing
- Multi-mode payment support (UPI, Cards, Net Banking, COD) tracking explicit status states (`Pending`, `Completed`).

### 6. ⭐ Reviews & Ratings
- Verified customer feedback mechanism capturing numeric ratings and detailed product commentary.

---

## 🔒 Non-Functional Requirements

* **Performance:** Schema design optimized for quick query retrieval and join efficiency.
* **Data Integrity:** Enforced referential integrity using strict `FOREIGN KEY` constraints and `ON DELETE CASCADE`.
* **Scalability:** Modular structural footprint easily adaptable to new entity additions (e.g., Sellers, Shipping Tracking).
* **Security:** Structured fields capable of storing encrypted/hashed credentials.

---

## 🗂 Database Entities & Schema Matrix

| Entity | Primary Key (PK) | Foreign Keys (FK) | Description |
| :--- | :--- | :--- | :--- |
| **`USER`** | `user_id` | *None* | Customer registration details and login credentials |
| **`PRODUCT`** | `product_id` | *None* | Item details, pricing, and available stock levels |
| **`CART`** | `cart_id` | `user_id` | Active shopping cart assigned uniquely to a user |
| **`CART_ITEM`** | `cart_item_id` | `cart_id`, `product_id` | Specific product line-items contained in a shopping cart |
| **`ORDERS`** | `order_id` | `user_id` | Placed order records, execution timestamps, and total cost |
| **`ORDER_ITEM`** | `order_item_id` | `order_id`, `product_id` | Individual line-items and historical unit prices inside an order |
| **`PAYMENT`** | `payment_id` | `order_id` | Payment transaction records and execution status |
| **`REVIEW`** | `review_id` | `user_id`, `product_id` | Customer product ratings and written feedback |

---

## 📊 ER Diagram

The ER Diagram was modeled using **StarUML** with **Crow's Foot Notation** to visually define cardinality and relational bounds across all tables:

<p align="center">
  <img src="./er-diagram.jpg.jpg" alt="Amazon E-Commerce ER Diagram" width="100%">
</p>

### 🔄 Interactive Native Diagram View

```mermaid
erDiagram
    USER ||--o| CART : "has"
    USER ||--o{ ORDERS : "places"
    USER ||--o{ REVIEW : "writes"
    PRODUCT ||--o{ REVIEW : "receives"
    CART ||--o{ CART_ITEM : "contains"
    PRODUCT ||--o{ CART_ITEM : "added to"
    ORDERS ||--o| PAYMENT : "processed by"
    ORDERS ||--o{ ORDER_ITEM : "includes"
    PRODUCT ||--o{ ORDER_ITEM : "sold as"

    USER {
        int user_id PK
        string name
        string email
        string password
    }
    PRODUCT {
        int product_id PK
        string title
        decimal price
        int stock
    }
    CART {
        int cart_id PK
        int user_id FK
    }
    CART_ITEM {
        int cart_item_id PK
        int cart_id FK
        int product_id FK
        int quantity
    }
    ORDERS {
        int order_id PK
        int user_id FK
        datetime order_date
        decimal total_amount
    }
    ORDER_ITEM {
        int order_item_id PK
        int order_id FK
        int product_id FK
        int quantity
        decimal price
    }
    PAYMENT {
        int payment_id PK
        int order_id FK
        string payment_method
        string status
    }
    REVIEW {
        int review_id PK
        int user_id FK
        int product_id FK
        int rating
        string comment
    }
