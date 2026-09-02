# Namaste Node.js — Episode 12: RDBMS vs NoSQL

## Overview

Covers **RDBMS vs NoSQL, MongoDB's data model, schema flexibility, normalization, joins, scaling, and database selection.**

## 1. MongoDB Data Model

MongoDB is a **NoSQL document database**.

```text id="4m9q3a"
RDBMS        → MongoDB
Table        → Collection
Row          → Document
Column       → Field
```

A collection contains documents, and documents contain fields.

MongoDB documents have a **JSON-like structure**, making them comfortable to use with JavaScript applications.

## 2. Documents & Nested Data

Example:

```js id="g6n8tf"
{
  id: 1,
  firstName: "John",
  city: "Kochi",
  hobbies: ["coding", "music"]
}
```

Related data can be stored directly inside a document, such as arrays or nested objects.

A collection can contain many documents.

## 3. Why MongoDB Feels Natural in JavaScript

MongoDB uses a JSON-like document model, while JavaScript applications commonly work with **objects and JSON**.

```text id="7p5j0k"
JavaScript Object
       ↕
    JSON/API
       ↕
MongoDB Document
```

This makes moving application data between the API and database feel natural.

## 4. RDBMS vs NoSQL

| RDBMS                        | NoSQL / MongoDB                  |
| ---------------------------- | -------------------------------- |
| Tables                       | Collections                      |
| Rows                         | Documents                        |
| Columns                      | Fields                           |
| Predefined schema            | Flexible document structure      |
| Relationships + joins        | Can embed related data           |
| SQL                          | Database-specific query language |
| Schema changes need planning | Fields can be more flexible      |

## 5. Flexible Schema

RDBMS tables generally have a defined column structure.

MongoDB documents can have different fields when the application allows it.

```text id="bq8p3f"
Document A → id, name, city
Document B → id, name
```

Flexible schema **doesn't mean no structure**. Applications can still enforce required fields and data rules.

## 6. Normalization & Joins

RDBMS commonly separates related data into tables and connects them using **keys and joins**.

MongoDB can instead keep related data together:

```js id="n9v7s1"
{
  name: "John",
  hobbies: ["coding", "music"]
}
```

This doesn't mean MongoDB should never use relationships or separate data. **Design depends on the data and access patterns.**

## 7. Query Languages

* **RDBMS → SQL**
* **MongoDB → MQL (MongoDB Query Language)**
* **Neo4j → Cypher**

## 8. Scaling

**Vertical scaling:** Make one machine more powerful.

```text id="e8d4w2"
1 powerful machine
```

**Horizontal scaling:** Add more machines/nodes.

```text id="q3h8nf"
Machine → Machine → Machine
```

The episode presents NoSQL as well suited to distributed/horizontal scaling use cases, while traditional RDBMS systems have historically focused more on vertical scaling.

## 9. When to Use Which?

### RDBMS can fit well when:

* Data is strongly structured
* Transactions are important
* Complex relationships are central
* Relational queries are common

### NoSQL can fit well when:

* Data is document-shaped
* Flexible schemas are useful
* Large/distributed workloads matter
* Data models change rapidly
* Document-oriented access patterns are important

## 10. Database Choice

There is **no universal best database**.

Choose based on:

```text id="j2x6z4"
Data model
    ↓
Transactions
    ↓
Read/write patterns
    ↓
Scale & distribution
    ↓
System requirements
    ↓
Database choice
```

Large systems can use multiple databases or specialized technologies for different requirements.

> **Database selection is a system-design decision, not a popularity contest.**

## Interview Quick Revision

**What is MongoDB?**
A NoSQL document database.

**What is a collection?**
A group of MongoDB documents, roughly comparable to a table.

**What is a document?**
A MongoDB record containing fields, usually represented using BSON/JSON-like structure.

**What is a field?**
A property/value inside a document, roughly comparable to a column.

**What is flexible schema?**
Documents can have different fields when the application design allows it.

**Does MongoDB require normalization like RDBMS?**
Not always. Related data can sometimes be embedded inside documents.

**What is MQL?**
MongoDB Query Language.

**Vertical vs horizontal scaling?**
Vertical = stronger machine; Horizontal = more machines/nodes.

**When might RDBMS be preferred?**
Structured relational data and transaction-heavy workloads.

**When might NoSQL be preferred?**
Flexible, distributed, large-scale, or document-oriented workloads.

**Which database is always best?**
None. Choose according to the application's requirements and access patterns.

## One-Minute Interview Explanation

> **MongoDB is a NoSQL document database that organizes data into collections, documents, and fields. Its JSON-like structure fits naturally with JavaScript applications and allows related data to be embedded when appropriate. Compared with RDBMS, it provides a more flexible document schema and can fit distributed workloads. RDBMS is often strong for structured relational data and transactions, while NoSQL can suit flexible and document-oriented workloads. Ultimately, database choice depends on the application's data model, access patterns, transactions, scale, and system requirements.**
