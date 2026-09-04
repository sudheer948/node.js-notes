# Namaste Node.js — Episode 13

## MongoDB Practical Setup & Node.js Connection

This episode covers setting up MongoDB, connecting it with Node.js, and performing basic database operations using the MongoDB Node.js Driver.

### Topics Covered

* MongoDB & NoSQL basics
* MongoDB Atlas
* MongoDB Compass
* MongoDB Node.js Driver
* npm package installation
* Connecting Node.js to MongoDB
* Databases, collections & documents
* `MongoClient`
* `find()` & `findOne()`
* MongoDB cursors
* `insertOne()` & `insertMany()`
* `countDocuments()`
* CRUD operations
* MongoDB Driver vs Mongoose
* Using official documentation

### Basic Flow

```text
MongoDB Atlas
     ↓
Connection URI
     ↓
MongoClient
     ↓
Database
     ↓
Collection
     ↓
CRUD Operations
```

### Installation

```bash
npm install mongodb
```

### Basic Connection

```js
const { MongoClient } = require("mongodb");

const client = new MongoClient(uri);

await client.connect();

const db = client.db("database");
const collection = db.collection("users");
```

### Common Operations

```js
// Read
await collection.find({}).toArray();

// Insert
await collection.insertOne({ name: "John" });

// Insert multiple
await collection.insertMany([
  { name: "John" },
  { name: "Jane" }
]);

// Count
await collection.countDocuments({});
```

### Important Concepts

* **Atlas** → Managed MongoDB cloud service
* **Compass** → MongoDB GUI
* **MongoClient** → Connects Node.js to MongoDB
* **Collection** → Group of documents
* **Document** → MongoDB record
* **Cursor** → Result returned by `find()`
* **CRUD** → Create, Read, Update, Delete
* **Mongoose** → Higher-level ODM built on MongoDB

### Security

Never commit MongoDB credentials or connection strings containing passwords to GitHub.

Use environment variables such as:

```env
MONGODB_URI=your_connection_string
```

### Key Takeaway

> Learn the MongoDB fundamentals, understand the Node.js driver, practice CRUD operations, and use the official documentation instead of memorizing APIs.
