📘 Database Fundamentals, SQL vs NoSQL, and MongoDB (Understanding-First Notes)
💡 What Was The Goal Of This Episode?

Before learning MongoDB, Akshay wanted to answer a very important question:

Why do databases exist in the first place?

Many beginners jump directly into MongoDB commands without understanding:

What a database is
Why databases exist
Why there are so many databases
Why MongoDB was created
Why companies don't use just one database

This episode builds that foundation.

📘 What Is A Database?

Most people answer:

A database is a place where data is stored.

Akshay explains that this answer is incomplete.

A better answer is:

A database is an organized collection of data.

The important word is:

Organized

Imagine you have:

Akshay
Rahul
12345
Delhi
Apple
Football

This is data.

But it is not organized.

Now imagine:

Name: Akshay
City: Delhi
Phone: 12345

Now the data has structure.

This organized form is what databases are designed to maintain.

📘 Why Can't We Just Store Everything In Files?

Imagine building Facebook.

You have:

Millions of users
Millions of posts
Millions of comments

If everything is stored inside normal files:

users.txt
posts.txt
comments.txt

Finding information becomes extremely difficult.

Example:

Suppose you want:

Find all comments written by Akshay.

Searching manually through huge files would be very slow.

Databases solve this problem.

They help:

Store data
Find data
Update data
Delete data

efficiently.

📘 What Is DBMS?

One of the most important concepts from the episode.

Many people confuse:

Database

and

DBMS

They are not the same thing.

Database

The actual stored data.

Example:

User Data
Post Data
Comment Data
DBMS

DBMS stands for:

Database Management System

A DBMS is software that manages the database.

Examples:

MongoDB
MySQL
PostgreSQL
Real Life Example

Imagine a library.

The books are:

Database

The librarian is:

DBMS

You don't directly manage thousands of books yourself.

The librarian:

organizes books
finds books
adds books
removes books

Similarly:

MongoDB, MySQL and PostgreSQL manage data for us.

📘 Why Do We Need A DBMS?

Suppose a user signs up:

Name: Sudheer
City: Thrissur

Without a DBMS:

You would need to manually:

store the data
organize the data
search the data
update the data

This becomes impossible at scale.

A DBMS handles all of this automatically.

📘 Are All Databases The Same?

No.

This is one of the biggest lessons from the episode.

Many beginners think:

Which database is the best?

Wrong question.

A better question is:

Which database is best for my problem?

Different databases solve different problems.

📘 Why Are There So Many Databases?

Akshay compares this with Data Structures.

Think about:

Arrays
Linked Lists
Trees
Graphs

Do we use only arrays?

No.

Because different problems require different structures.

The same idea applies to databases.

Different databases exist because different applications have different needs.

📘 Major Types Of Databases

Akshay briefly introduces:

Relational Databases

Examples:

MySQL
PostgreSQL
NoSQL Databases

Example:

MongoDB
In-Memory Databases

Example:

Redis

Used heavily for caching.

Graph Databases

Example:

Neo4j

Used when relationships are extremely important.

📘 What Is Redis?

Akshay briefly mentions Redis.

Redis stores data in memory.

Memory is much faster than disk.

Because of this:

Redis is often used as a cache.

Example:

Instead of hitting MongoDB repeatedly:

User Request
     ↓
Redis
     ↓
MongoDB (if needed)

This improves speed.

📘 Do Big Companies Use Only One Database?

No.

This is a very important point.

People often ask:

Which database does Google use?

or

Which database does Amazon use?

Large companies use many databases.

Different teams may use different technologies.

Different products may use different databases.

Database choice depends on the problem being solved.

📘 What Is RDBMS?

RDBMS stands for:

Relational Database Management System

Examples:

MySQL
PostgreSQL

These databases store data in tables.

📘 A Little History

Akshay briefly talks about:

Edgar F. Codd

Edgar F. Codd

He introduced the relational database model.

He also proposed the famous:

Codd's Rules

which helped define what a relational database should be.

📘 MySQL History

Created by:

Michael Widenius

Interesting fact:

His daughter was named:

My

which is where:

MySQL

got its name.

📘 MariaDB

Later a fork called:

MariaDB

was created.

📘 PostgreSQL History

Akshay also briefly talks about PostgreSQL's origins and how it evolved from earlier database research projects.

The main goal isn't memorizing the history.

The goal is understanding:

These technologies were created to solve real-world problems.

📘 What Is SQL?

SQL stands for:

Structured Query Language

SQL is the language used to communicate with relational databases.

Think of SQL as:

The language you use to ask the database questions.

Examples:

SELECT *
FROM users;
INSERT INTO users
UPDATE users
DELETE users

These commands allow us to interact with the database.

📘 What Is NoSQL?

Akshay explains two meanings.

Meaning 1
Non SQL
Meaning 2
Not Only SQL

The community generally prefers:

Not Only SQL

because NoSQL databases are not against SQL.

They simply use a different approach.

📘 Why Did NoSQL Become Popular?

As applications became larger:

Social Media
Big Data
Real-Time Systems

developers needed more flexibility.

This helped NoSQL databases grow rapidly.

📘 Why MongoDB Became Popular?

One of the most important sections.

MongoDB became popular because:

1. Flexible

Changing structure is easier.

2. Developer Friendly

Developers can work faster.

3. JavaScript Friendly

This is the biggest reason for Node.js developers.

MongoDB data looks very similar to JavaScript objects.

📘 Why Is It Called MongoDB?

Mongo comes from:

Humongous

meaning:

Huge
Large Scale

MongoDB was designed for large-scale data systems.

📘 What Is A Collection?

Now Akshay starts comparing RDBMS and MongoDB.

In MySQL:

You have:

Tables

In MongoDB:

You have:

Collections

A collection is simply a group of related documents.

Think:

Users Collection
Products Collection
Orders Collection
📘 What Is A Document?

This is one of the most important MongoDB concepts.

A document is one record.

Example:

{
  firstName: "Akshay",
  city: "Delhi",
  hobbies: ["Teaching", "JavaScript"]
}

This entire object is called a:

Document

A collection contains many documents.

📘 Why Documents Feel Natural To JavaScript Developers

Look at this:

{
  firstName: "Akshay",
  city: "Delhi"
}

Doesn't it look exactly like a JavaScript object?

That's why Node.js developers love MongoDB.

The data structure already feels familiar.

Akshay specifically highlights this advantage.

📘 How Is MongoDB Different From MySQL?

Suppose we want to store:

Name
City
Hobbies

In a relational database, hobbies are often separated into another table and connected using relationships.

In MongoDB:

You can directly store:

{
 hobbies: [
   "Coding",
   "Reading"
 ]
}

inside the same document.

This feels much more natural to many developers.

📘 What Is Data Normalization?

Akshay only gives a high-level introduction.

In relational databases:

Data is often split into multiple tables.

Why?

To reduce duplication and maintain consistency.

This process is called:

Normalization

He mentions that MongoDB often avoids heavy normalization and instead allows related data to be stored together.

📘 Why Do Relational Databases Need Joins?

Suppose:

Users are stored in one table.

Hobbies are stored in another table.

To combine them:

The database performs a:

Join

MongoDB often reduces the need for joins by allowing nested data.

📘 Fixed Schema vs Flexible Schema

One of the biggest practical differences.

RDBMS

Schema changes are possible.

But they require more planning.

MongoDB

Adding new fields is generally easier.

This flexibility is one reason developers like MongoDB.

📘 SQL vs MQL

Relational databases use:

SQL

MongoDB uses:

MQL

which stands for:

Mongo Query Language

📘 Which Database Is Better?

Akshay repeatedly says:

Wrong question.

The correct question is:

Which database fits the problem?

Examples he gives:

Banking Systems

Often fit relational databases very well because transactions are extremely important.

Real-Time Systems
Big Data Systems
Distributed Systems

MongoDB and other NoSQL databases are often attractive options here.

📘 Uber Example

Akshay talks about working at Uber.

One lesson:

Large companies sometimes create their own database technologies for their unique requirements.

Because eventually:

Scale Creates Unique Problems

and those problems sometimes require custom solutions.

🎯 Interview Questions
What is a Database?
What is a DBMS?
Difference between Database and DBMS?
Why do we need databases?
What is RDBMS?
What is SQL?
What is NoSQL?
Why did MongoDB become popular?
What is a Collection?
What is a Document?
What is Normalization?
What is a Join?
Difference between MySQL and MongoDB?
What is MQL?
Why is MongoDB popular among Node.js developers?
Why do companies use multiple databases?
⭐ Episode Rating

9.5/10

This is not a coding episode.

It is a mindset-building episode that helps you understand why databases exist and why MongoDB was created.
