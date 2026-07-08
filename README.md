# 🏠 Airbnb Database Management System

A PostgreSQL-based relational database system that models the core functionalities of an Airbnb-like platform. The project covers the full database design lifecycle — **ER modeling, functional dependency analysis, BCNF-level normalization, relational schema design, and SQL implementation** — to manage users, properties, bookings, payments, reviews, and cancellations.

![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-336791?logo=postgresql&logoColor=white)
![SQL](https://img.shields.io/badge/Language-SQL-blue)
![Normalization](https://img.shields.io/badge/Normalization-BCNF-success)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📑 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Entities](#database-entities)
- [ER Diagram](#er-diagram)
- [Relational Schema](#relational-schema)
- [Functional Dependencies & Normalization](#functional-dependencies--normalization)
- [How to Run](#how-to-run)
- [Modules](#modules)
- [Key Database Concepts](#key-database-concepts)
- [Authors](#authors)
- [License](#license)

---

<a id="features"></a>
## ✨ Features

- User, Guest, Host, and Admin management (role-based via generalization/specialization)
- Property & Listing management
- Booking and Cancellation management
- Payment processing
- Review & Rating system
- Amenity management (many-to-many via `Listing_Amenity`)
- Complete ER modeling with entity relationships and constraints
- Functional Dependency (FD) analysis for every relation
- Formal **BCNF verification** for all 12 tables
- Complex SQL queries using Joins, Subqueries, and Aggregate Functions
- Views and Triggers for business logic enforcement

---

<a id="tech-stack"></a>
## 🛠️ Tech Stack

- **Database:** PostgreSQL
- **Language:** SQL (DDL, DML, DQL)
- **Design:** ER Modeling, Relational Algebra, Normalization Theory

---

<a id="project-structure"></a>
## 📂 Project Structure

```text
Airbnb-Database-System/
│
├── README.md
├── ER-Diagram.pdf
├── Relational-Schema.pdf
├── Normalization-BCNF.pdf        # FD analysis + BCNF proof for all tables
│
└── SQL/
    ├── schema.sql                # DDL: table creation, keys, constraints
    ├── insert.sql                # Sample data population
    └── queries.sql               # Joins, aggregates, views, triggers
```

---

<a id="database-entities"></a>
## 🗂️ Database Entities

| Entity | Description |
|---|---|
| **User** | Base entity holding common attributes for every platform user |
| **Host** | Specialization of User — lists properties |
| **Guest** | Specialization of User — books stays |
| **Admin** | Specialization of User — manages platform operations |
| **Property** | Physical property owned/listed by a Host |
| **Listing** | Bookable listing tied to a Property (price, availability, rules) |
| **Amenity** | Reusable amenity master list (WiFi, Pool, Parking, etc.) |
| **Listing_Amenity** | Bridge table resolving the Listing ↔ Amenity many-to-many relationship |
| **Booking** | A Guest's reservation of a Listing |
| **Payment** | Payment transaction linked to a Booking |
| **Review** | Guest rating/feedback linked to a Booking and Listing |
| **Cancellation** | Cancellation record linked to a Booking |

---

<a id="er-diagram"></a>
## 🖼️ ER Diagram

The complete ER Diagram — including entities, relationships, cardinalities, and the User generalization/specialization hierarchy (Host, Guest, Admin) — is available in:

📄 [`ER-Diagram.pdf`](./ER-Diagram.pdf)

---

<a id="relational-schema"></a>
## 🏗️ Relational Schema

The full relational schema, with primary keys, foreign keys, and constraints for all 12 tables, is available in:

📄 [`Relational-Schema.pdf`](./Relational-Schema.pdf)

---

<a id="functional-dependencies--normalization"></a>
## 🧮 Functional Dependencies & Normalization

Every relation in this schema was analyzed for functional dependencies and formally checked against **Boyce-Codd Normal Form (BCNF)**. The full working — minimal FD sets and per-table BCNF proofs — is documented in **[`Normalization-BCNF.pdf`](./Normalization-BCNF.pdf)**.

### Summary of Findings

| Table | Candidate Key(s) | BCNF Status |
|---|---|---|
| User | `{user_id}` | ✅ In BCNF |
| Host | `{user_id}` | ✅ In BCNF |
| Guest | `{user_id}` | ✅ In BCNF |
| Admin | `{user_id}` | ✅ In BCNF |
| Property | `{property_id}` | ✅ In BCNF |
| Listing | `{listing_id}` | ✅ In BCNF |
| Amenity | `{amenity_id}` | ✅ In BCNF |
| Listing_Amenity | `{listing_id, amenity_id}` | ✅ In BCNF |
| Booking | `{booking_id}` | ✅ In BCNF |
| Payment | `{payment_id}` | ✅ In BCNF |
| Review | `{review_id}` | ✅ In BCNF |
| Cancellation | `{cancellation_id}` | ✅ In BCNF |

**Conclusion:** Every non-trivial functional dependency in the schema has a candidate key (superkey) on its left-hand side. No partial or transitive dependencies exist on any non-prime attribute, and `Listing_Amenity` — the only composite-key relation — has no non-key attributes at all. The entire schema is therefore **already in BCNF**, requiring no further decomposition.

> 💡 See [`Normalization-BCNF.pdf`](./Normalization-BCNF.pdf) for the complete list of functional dependencies per table and the detailed candidate-key/BCNF-check/verdict breakdown used to reach this conclusion.

---

<a id="how-to-run"></a>
## 🚀 How to Run

1. **Create the schema** in PostgreSQL:
   ```sql
   CREATE SCHEMA Airbnb_system;
   SET search_path TO Airbnb_system;
   ```

2. **Execute the SQL files in order:**
   ```bash
   psql -U your_username -d your_database -f SQL/schema.sql
   psql -U your_username -d your_database -f SQL/insert.sql
   psql -U your_username -d your_database -f SQL/queries.sql
   ```

3. Explore the sample queries in `queries.sql` to see joins, aggregates, views, and triggers in action.

---

<a id="modules"></a>
## 📊 Modules

- User Management
- Property Management
- Listing Management
- Booking Management
- Payment Management
- Review Management
- Cancellation Management
- Amenity Management

---

<a id="key-database-concepts"></a>
## 🧩 Key Database Concepts

- ER Modeling & Generalization/Specialization
- Functional Dependency Analysis
- Normalization up to BCNF
- Primary Keys & Foreign Keys
- Entity Relationships & Cardinalities
- Constraints (PK, FK, UNIQUE, NOT NULL)
- SQL Joins & Subqueries
- Aggregate Functions
- Views
- Triggers

---

<a id="authors"></a>
## 👨‍💻 Authors

**Kishan Savani**
DA-IICT | B.Tech ICT

---

<a id="license"></a>
## 📄 License

This project is developed for educational purposes.
