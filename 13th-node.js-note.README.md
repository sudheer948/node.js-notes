# Namaste Node.js — Episode 13: MongoDB Practical Setup & Node.js Connection

## Overview

Covers **MongoDB Atlas, Compass, npm, MongoDB Driver, Node.js connection, CRUD, cursors, and documentation.**

## 1. MongoDB Setup

MongoDB is a **NoSQL document database**:

```text
Database → Collection → Documents → Fields
```

Two approaches:

* **Self-managed** → Install and manage MongoDB yourself.
* **Managed** → Use MongoDB Atlas to manage infrastructure.

## 2. MongoDB Atlas

**Atlas** is MongoDB's managed cloud service.

Basic setup:

```text
Create Account
    ↓
Create M0 Cluster
    ↓
Choose Region
    ↓
Create Database User
    ↓
Get Connection URI
    ↓
Connect Node.js / Compass
```

M0 is the free cluster used for learning/small workloads.

> **Never expose a connection URI containing credentials in public GitHub code.**

## 3. MongoDB Compass

**Compass** is MongoDB's GUI for viewing databases, collections, and documents.

```text
Atlas → Connection URI → Compass → Inspect Data
```

Application database operations will still be performed through code.

## 4. npm & MongoDB Driver

Node.js core modules like `fs` are built into Node.js.

The MongoDB driver is an **external npm package**:

```bash
npm install mongodb
```

It allows Node.js to communicate with MongoDB.

`node_modules` contains dependencies and should be added to `.gitignore`:

```text
node_modules
```

Keep `package.json` and `package-lock.json` in Git.

## 5. Documentation > Memorization

Don't memorize library APIs.

```text
Check installed version
        ↓
Read official docs
        ↓
Understand parameters/returns
        ↓
Adapt examples
```

Documentation is the source of truth for the library's current API.

## 6. Connect Node.js to MongoDB

Basic connection flow:

```js
const { MongoClient } = require("mongodb");

const client = new MongoClient(uri);

await client.connect();

const db = client.db("hello world");
const collection = db.collection("user");
```

```text
MongoClient
    ↓
connect()
    ↓
db()
    ↓
collection()
    ↓
Database Operations
```

The connection is asynchronous, so `async/await` is used.

## 7. Reading Documents

```js
const result = await collection.find({}).toArray();
```

* `{}` → matches all documents
* `find()` → returns a **cursor**
* `toArray()` → converts results to an array

Filtering:

```js
collection.find({ firstName: "Deepika" }).toArray();
```

## 8. Insert Documents

```js
await collection.insertOne({ name: "John" });

await collection.insertMany([
  { name: "John" },
  { name: "Jane" }
]);
```

* `insertOne()` → one document
* `insertMany()` → multiple documents
* MongoDB generates an `ObjectId` if no ID is provided.

## 9. CRUD

```text
C → Create → insertOne / insertMany
R → Read   → find / findOne
U → Update
D → Delete
```

Practice all four operations using the official documentation.

## 10. countDocuments()

```js
const count = await collection.countDocuments({});
```

Counts documents matching a filter.

Be careful when repeatedly running code that inserts documents — every run can add another document.

## 11. MongoDB Driver vs Mongoose

**MongoDB Driver**
→ Direct Node.js library for communicating with MongoDB.

**Mongoose**
→ Higher-level library that provides more structure and convenience.

The course teaches the native driver first to build a foundation, while the later project uses **Mongoose**.

## Interview Quick Revision

**What is MongoDB Atlas?**
MongoDB's managed cloud database service.

**What is Compass?**
GUI for connecting to and inspecting MongoDB data.

**What does MongoClient do?**
Connects Node.js to MongoDB.

**What does `find()` return?**
A cursor.

**`insertOne()` vs `insertMany()`?**
One document vs multiple documents.

**What is CRUD?**
Create, Read, Update, Delete.

**Why use documentation?**
APIs and versions change; documentation provides the correct current usage.

**Why learn the native driver before Mongoose?**
It helps understand the underlying MongoDB interaction.

## Quick Revision

```text
MongoDB → NoSQL document database
Atlas → Managed MongoDB cloud service
M0 → Free learning cluster
Compass → MongoDB GUI

npm install mongodb
        ↓
MongoClient
        ↓
connect()
        ↓
db()
        ↓
collection()

find() → Cursor
toArray() → Array
insertOne() → One
insertMany() → Multiple
countDocuments() → Count
CRUD → Create, Read, Update, Delete
```

> **Main takeaway: Don't memorize MongoDB code. Learn to read documentation, connect to the database, use the API, troubleshoot, and practice.**
