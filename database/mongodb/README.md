# MongoDB

## NoSQL

- NoSQL is a non-relational db that uses key-value pairs to store and retrieve data. Unlike a relational db, which stores data in rows and columns
- It is Non-Relational db: A collection of unstructured and semi structured items which donot store data in tabular form.

### NoSQL Examples

- Key-Value (Redis, Riak)
  - Uses: Briskly changing data and high availability
- Column Based (Cassandra, HBase)
  - Uses: Read/Write extensions
- Document Database (MongoDB, Couchbase)
  - Uses: Working with occasionally changing consistent data
- Graph Databse (Neo4j, Big Data)
  - Uses: Spatial Data Storage

## What is MongoDB

- MongoDB is a NoSQL (Not only SQL) database that stores large volumes of data in the form of documents. MongoDB removes the concept of "rows" of conventional and relational data models by introducing "documents." This offers the developers the flexibility to work with evolving data models.

- Document Data Model: Collection of complex documents with arbitrary, nested data formats and varying "record" format.

## History of MongoDB

- 2007 - Founded by Dwight Merriman, Eliot Horowitz and Kevin Ryan – the team behind DoubleClick.
- 2007-08 - Developed as Platform as a Service (PaaS)
- 2009 - Introduced as Open Source database server
- 2017 - MondoDB listed on NASDAQ

## Why MongoDB is used?

- Open-Source Database
- Easy to Use: Robust, highly scalable and powerful way of storing data in comparison to traditional database models.
- Highly Flexible: Allows you to store and work on different data types in one document
- Advanced Security
- Powerful Query Language
- Reliable Indexing
- Flexible Schema: Flexible schema design that allows you to meet the ever-changing conditions characteristic of Big Data applications.
- High Performance: MongoDB offers incredible features like on-demand scaling, real-time resources, etc. to guarantee high performance of the applications.

## Key Features of MongoDB

- Aggregation
- GridFS
- Sharding
- Document Oriented
- Replication
- Schema Less Database
- Indexing
- Ad Hoc Qeuries
- High Performance

## How does MongoDB works?

- MongoDB stores data objects in collections and documents instead of the tables and rows used in traditional relational databases. Collections comprise sets of documents, which are equivalent to tables in a relational database. Documents consist of key-value pairs, which are the basic unit of data in MongoDB.

## Applications of MongoDB

- IoT (Internet of Things)
- Mobile Applications
- Real Time Analysis
- Personalization
- Catalog Mangement
- Content Mangement

## Data Modeling

### What is Data Modeling?

- Data Modeling is the process of determining how data is stored and what connection exists between various entities in our data.

### Why we use Data Modeling?

- Data modeling helps us to create a simplified and optimized logical databases that eliminates redundancy, reduces storage requirments and enables efficient retrieval.

### Data Models used in MongoDB

- Conceptual Data Modeling
- Logical Data Modeling
- Physical Data Modeling

### Types of Relationships in Data Models

- One to One
- One to Many
- Many to Many

### Types of Methods to Create a Data Model

- Embedded Data Models
- Reference Data Models

## What is MongoDB Operators?

- MongoDB query operators are simply keywords or special symbols that tell the interpreter how to process logical or mathematical operations.
- SYNTAX

```bash
db.name_of_collection.find ({
"Field _name": { $query_operator_name:
"value" }}).pretty()
```

### Types of Operators in MongoDB

- Query and Projection Operator
  - projection refers to picking only the data that is required rather than the entire document's data.
    - COMPARISON
    - LOGICAL
    - ARRAY
    - ELEMENT
    - BITWISE
    - EVALUATION
    - GEOSPATIAL
- Update Operator
  - updates the values of the fields of documents matching the specified condition
- Aggregation Pipeline Operator
  - As a result of processing the data records and documents, aggregation operations provide computed results.

## Installation [TODO]

## Uses

- Open terminal

```bash
mongosh
show dbs
```
