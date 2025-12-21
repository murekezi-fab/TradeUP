TradeUp — Smart Product Exchange & Top-Up Marketplace
Project Overview

This is a multi-phase individual capstone project centered on Oracle Database design, PL/SQL development, and Business Intelligence (BI) implementation.
The project delivers a production-ready marketplace database that supports product purchasing, product exchange, and top-up payments, enabling customers to acquire higher-value items by trading existing products and paying the price difference.

Course: Database Development with PL/SQL (INSY 8311)
Institution: Adventist University of Central Africa (AUCA)

1. Problem Statement (Phase I)

Traditional e-commerce platforms only support direct buying and selling, which excludes customers who cannot afford the full price of desired products. At the same time, many usable products are discarded instead of being reused.

This limitation reduces affordability, slows inventory movement, and discourages sustainable product reuse.

1.1 Solution and Innovation

TradeUp introduces a hybrid marketplace model that allows customers to:

Exchange their existing products

Automatically calculate product value differences

Pay only the required top-up amount

The innovation lies in the automated exchange valuation logic, implemented using PL/SQL procedures, functions, and triggers, enabling transparent, traceable, and flexible transactions.

Key Objectives

Improve product affordability through exchange + top-up

Promote sustainable reuse of goods

Increase seller inventory turnover

Ensure secure and auditable transactions

Provide analytics for business decision-making

Technical Approach

The system uses PL/SQL stored procedures, packages, and triggers to manage product exchanges, order processing, payment handling, and auditing in near real-time.

TradeUP ER diagram

<img width="784" height="1168" alt="image" src="https://github.com/user-attachments/assets/571e987f-ae8c-4b73-9960-e290d0ec0205" />

1.2 Database Schema Summary

The TradeUp system is built on a relational database structure consisting of six core tables:

Table Name	Purpose	Key Attributes
USERS	Stores platform users and roles	User_ID (PK), User_Type
PRODUCTS	Stores product listings and ownership	Product_ID (PK), Owner_ID (FK)
ORDERS	Manages purchases and exchanges	Order_ID (PK), Order_Type
ORDER_ITEMS	Links products to orders	Order_Item_ID (PK), Order_ID (FK)
EXCHANGE_REQUESTS	Manages exchange logic and top-ups	Exchange_ID (PK), Topup_Amount
PAYMENTS	Stores payment and top-up records	Payment_ID (PK), Amount
2. Phase II – Business Process Modeling (UML & BPMN)

This phase models the core business workflow of the TradeUp platform using BPMN and UML diagrams, illustrating how product exchanges and purchases flow through the system.

2.1 BPMN Diagram – Product Purchase & Exchange Workflow

The BPMN diagram represents:

Customer authentication

Product browsing

Purchase or exchange selection

Automated valuation and top-up calculation

Payment processing

Order confirmation

(BPMN Diagram included in repository)

2.2 Explanation

Customers browse products and choose either a direct purchase or an exchange option.
For exchanges, the system evaluates the customer’s old product value, calculates the required top-up amount, and records the transaction. Payments are processed and stored, and all actions are logged for auditing.

The BPMN diagram shows interactions between customers, sellers, and the TradeUp system, while the UML activity diagram details internal system logic supporting MIS objectives such as affordability, sustainability, and transaction transparency.

3. Phase III – Logical Database Design (ERD + Data Dictionary + 3NF)
3.1 ER Diagram (Logical Model)

Key relationships in the TradeUp ERD:

Entity A	Relationship	Entity B	Cardinality	Notes
USERS	1 → Many	PRODUCTS	One user owns many products	Owner_ID FK
USERS	1 → Many	ORDERS	One user places many orders	User_ID FK
ORDERS	1 → Many	ORDER_ITEMS	One order contains many products	Order_ID FK
ORDERS	1 → 1	PAYMENTS	Each order has one payment	Order_ID FK
ORDERS	1 → 1	EXCHANGE_REQUESTS	Exchange orders only	Order_ID FK
3.2 Data Dictionary (Sample)
USERS
Attribute	Type	Constraints
User_ID	NUMBER(10)	PK, NOT NULL
Username	VARCHAR2(50)	UNIQUE, NOT NULL
Email	VARCHAR2(100)	UNIQUE
User_Type	VARCHAR2(20)	CHECK (Customer, Seller, Admin)
Created_At	DATE	DEFAULT SYSDATE
PRODUCTS
Attribute	Type	Constraints
Product_ID	NUMBER(10)	PK
Name	VARCHAR2(100)	NOT NULL
Price	NUMBER(10,2)	CHECK > 0
Condition	VARCHAR2(20)	CHECK(New, Used)
Owner_ID	NUMBER(10)	FK
3.3 Normalization Check (3NF)
Table	3NF Status
USERS	Pass
PRODUCTS	Pass
ORDERS	Pass
ORDER_ITEMS	Pass
EXCHANGE_REQUESTS	Pass
PAYMENTS	Pass

Conclusion: All tables satisfy Third Normal Form (3NF).

3.4 Assumptions

One exchange request belongs to one order

Product valuation logic is handled in PL/SQL

Payments include both full purchases and top-ups

Users may act as both buyers and sellers

Exchange records are automatically audited

4. Database Creation (Phase IV)
4.1 Pluggable Database Setup

PDB Name:
mon_<StudentID>_fabrice_tradeup_db

Executed as SYSDBA:

CREATE PLUGGABLE DATABASE mon_XXXX_fabrice_tradeup_db
ADMIN USER tradeup_admin IDENTIFIED BY fabr
ROLES = (DBA);


The PDB is opened and connected via Oracle SQL Developer, where all remaining phases are implemented.

4.2 Tablespace & User Configuration

Dedicated tablespaces for data, index, and temporary storage were created with AUTOEXTEND enabled.
Application user tradeup_app was granted appropriate privileges.

5. Table Implementation & Data Insertion (Phase V)
Achievements

Triggers creation

<img width="601" height="401" alt="image" src="https://github.com/user-attachments/assets/a33bd84e-e057-4f3e-8f25-3faaa6646941" />


BPM Diagram

<img width="724" height="1080" alt="image" src="https://github.com/user-attachments/assets/f33c60fe-c29d-4482-bfa1-f0c97ec4fac6" />
