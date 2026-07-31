# Amazon E-Commerce Database Design

### DBMS Assignment: Requirements, ER Diagram and Relational Schema

**Prepared by:** Vasanthakumar 
**Register Number:** AADS25031 
**Programme:** B.sc AI&DS
**Institution:** AMET UNIVERSITY

---

## Project Overview

This project presents a basic database design for an Amazon-style e-commerce platform. It identifies the main entities, their attributes, primary keys, foreign keys, and relationships. The Entity Relationship Diagram was designed using StarUML and converted into a relational schema.

This is a simplified academic model. It does not represent Amazon's actual internal database.

---

## Assignment Tasks

### Task I: Software Requirements Specification
The functional and non-functional requirements of the e-commerce platform were identified. The system supports customer accounts, products, carts, orders, payments, order tracking, and product reviews.

### Task II: Database Requirements
The required entities, attributes, primary keys, foreign keys, and relationships were identified.

### Task III: ER Diagram and Relational Schema
The ER diagram was created in StarUML using Crow's Foot notation. The completed diagram was then converted into a relational schema.

---

## Software Requirements Specification

### 1. Functional Requirements
* **User Account Management:** Users can register, login, logout, and manage profile details.
* **Product Management:** Users can view products, search items, and filter based on categories, price, and ratings.
* **Cart and Order System:** Users can add items to cart, remove items, update quantity, and place orders.
* **Payment System:** Supports multiple payment methods such as UPI, cards, net banking, and cash on delivery.
* **Order Tracking:** Users can track their orders and receive delivery updates.
* **Review and Rating:** Customers can provide ratings and reviews for products.

### 2. Non-Functional Requirements
* **Performance:** The system should load quickly and handle large numbers of users simultaneously.
* **Security:** Ensures secure transactions and protects user data using encryption.
* **Scalability:** The system should be able to handle growth in users and transactions.
* **Reliability:** The system should be available 24/7 with minimal downtime.
* **Usability:** The interface should be user-friendly and accessible on all devices.
* **Availability:** The system should always be accessible to users globally.

---

## Main Entities & Attributes

1. **USER:** Stores user details (`user_id`, `name`, `email`, `password`).
2. **PRODUCT:** Stores product catalog data (`product_id`, `title`, `price`, `stock`).
3. **CART:** Links a user to their active cart (`cart_id`, `user_id`).
4. **CART_ITEM:** Contains individual products inside a cart (`cart_item_id`, `cart_id`, `product_id`, `quantity`).
5. **ORDERS:** Holds order transaction details (`order_id`, `user_id`, `order_date`, `total_amount`).
6. **ORDER_ITEM:** Contains items purchased within an order (`order_item_id`, `order_id`, `product_id`, `quantity`, `price`).
7. **PAYMENT:** Records transaction payment method and status (`payment_id`, `order_id`, `payment_method`, `status`).
8. **REVIEW:** Stores customer reviews and ratings (`review_id`, `user_id`, `product_id`, `rating`, `comment`).

---

## Entity Relationship (ER) Diagram

The ER diagram was modeled in StarUML using Crow's Foot Notation to represent primary keys, foreign keys, and cardinalities:

![Figure 1: ER Diagram of Amazon E-Commerce Platform](./er-diagram.png)

---

## Relational Schema

Below is the normalized relational database schema converted from the ER diagram:

> **Key:** **`Bold & Underlined`** = Primary Key (PK) | *Italics* = Foreign Key (FK)

* **USER** (**`user_id`**, name, email, password)
* **PRODUCT** (**`product_id`**, title, price, stock)
* **CART** (**`cart_id`**, *user_id*)
* **CART_ITEM** (**`cart_item_id`**, *cart_id*, *product_id*, quantity)
* **ORDERS** (**`order_id`**, *user_id*, order_date, total_amount)
* **ORDER_ITEM** (**`order_item_id`**, *order_id*, *product_id*, quantity, price)
* **PAYMENT** (**`payment_id`**, *order_id*, payment_method, status)
* **REVIEW** (**`review_id`**, *user_id*, *product_id*, rating, comment)

---

## SQL Table Creation Script

```sql
CREATE TABLE USER (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);

CREATE TABLE PRODUCT (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(150) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0
);

CREATE TABLE CART (
    cart_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT UNIQUE,
    FOREIGN KEY (user_id) REFERENCES USER(user_id)
);

CREATE TABLE CART_ITEM (
    cart_item_id INT PRIMARY KEY AUTO_INCREMENT,
    cart_id INT,
    product_id INT,
    quantity INT DEFAULT 1,
    FOREIGN KEY (cart_id) REFERENCES CART(cart_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id)
);

CREATE TABLE ORDERS (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (user_id) REFERENCES USER(user_id)
);

CREATE TABLE ORDER_ITEM (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT DEFAULT 1,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES ORDERS(order_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id)
);

CREATE TABLE PAYMENT (
    payment_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT UNIQUE,
    payment_method VARCHAR(50) NOT NULL,
    status VARCHAR(30) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES ORDERS(order_id)
);

CREATE TABLE REVIEW (
    review_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    product_id INT,
    rating INT,
    comment TEXT,
    FOREIGN KEY (user_id) REFERENCES USER(user_id),
    FOREIGN KEY (product_id) REFERENCES PRODUCT(product_id)
);

Here is a clean, formal conclusion paragraph tailored specifically for your assignment. You can copy and paste this directly into your GitHub `README.md` or assignment report:

---

### Conclusion

> The designed database system effectively models the core architectural requirements of an Amazon-style e-commerce platform. By defining primary entities, establishing clean relational cardinalities, and converting the ER diagram into a 3NF normalized relational schema, the design prevents data redundancy and ensures strong data integrity. This structural foundation successfully supports key functional operations—including user management, product cataloging, order fulfillment, payment processing, and customer reviews—while maintaining the scalability and reliability required for real-world enterprise deployment.
> 
>
