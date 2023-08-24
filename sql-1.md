# Database and the relational model

## Agenda
* What is a database?
* Why do we use DBMS?
* What are the different types of databases?
* What is a relational database?

## Key terms
### Data
> **Information** or facts and statistics collected together for reference or analysis.

> **Information** that has been translated into a form that is efficient for movement or processing

Examples
* Runs scored by Virat Kohli
* Temperature in Bangalore
* Your food orders from Swiggy
* Students in a class

### Database
> an organized collection of **inter-related** data that models some aspect of the real-world

> a set of **related** data and the way it is organized

Examples
* Scorecards of all cricket matches
* Weather conditions of all cities in the world
* All orders placed on Swiggy
* Students, mentors and batches

### Database Management System
> software system that enables users to define, create, maintain and control access to the database

>  the software that manages a database

Examples
* MySQL
* PostgreSQL
* MongoDB
* Oracle
  
### Relational Database
> An approach to managing data using a structure and language consistent with first-order predicate logic, first described where all data is represented in terms of tuples, grouped into relations. A database organized in terms of the relational model is a relational database.

### Non-relational Database
> A non-relational database is a database that does not use the tabular schema of rows and columns found in most traditional database systems. Instead, non-relational databases use a storage model that is optimized for the specific requirements of the type of data being stored

> Non-relational databases (often called NoSQL databases) are different from traditional relational databases in that they store their data in a non-tabular form. Instead, non-relational databases might be based on data structures like documents. A document can be highly detailed while containing a range of different types of information in different formats

# Brute Force - Files

Let us say it is 1960, and you haven't heard of databases.
Scaler is early on the scene, and they want to store the following data points
* Student (name, age, address, phone, email, etc.)
* Mentor (name, age, address, phone, email, etc.)
* Batch (name, mentor, start date, type, etc.)

What is the simplest way we can store this data?

**Files**
* Store each entity as a separate CSV file
  * students.csv
  * mentors.csv
  * batches.csv

### Sample students.csv
```csv
Name,Email,Phone,Age,Address
Tantia Tope,tantia@rani.bai,123456789,20,Jhansi
Kilvish,kil@vi.sh,987654321,21,Andhera
John Watson,i.am@sherlock.ed,123456789,30,221B Baker Street
```

or 

| Name        | Email            | Phone     | Age | Address           |
| ----------- | ---------------- | --------- | --- | ----------------- |
| Tantia Tope | tantia@rani.bai  | 123456789 | 20  | Jhansi            |
| Kilvish     | kil@vi.sh        | 987654321 | 21  | Andhera           |
| John Watson | i.am@sherlock.ed | 123456789 | 30  | 221B Baker Street |

Recap
* Store each entity as a separate CSV file
* The first row of each file is the header
* Header contains the attributes of the entity
* Each row except the header contains the data of the entity
* To read a record, the file needs to be parsed every time

### Issues - Can we use files for a real application?
* Not scalable - Inefficient
  * Worst case complexity is O(n)
  * We need to read the file every time we want to search for a user
  * We need to go through the file every time we want to search for a user
* Data integrity
  * What if there are duplicates in the file?
  * What happens if we replace the age of a student with a garbage value?
  * What happens if we delete a mentor that is part of a batch?
* Concurrency
  * What if two users update and save the file at the same time? Which value is saved?
* Security
  * Anyone with access to file system be able to read the file and even update it.
* Fault tolerance
  * What happens if computer crashes while you are updating the file?

### Types of DBMS
* Relational
* Non-relational (NoSQL)
  * Columnar
    * > stores data tables by column rather than by row for more efficient access to data when only querying a subset of columns
    * MariaDB, InfluxDB
  * Graph-based
    * > graph structures with nodes, edges, and properties to represent and store information
    * Neo4j
  * Key-value
    * > uses a simple key-value method to store data where a key serves as a unique identifier. 
    * DynamoDB, Redis, etc.
  * Document-oriented
    * Extension of key-value database that stores data in a more complex structure which allows for optimisations for querying and storing data.
    * MongoDB, CouchDB, etc.
  * Time series
    * > to store and retrieve data records that are part of a “time series,” which is a set of data points that are associated with timestamps. The timestamps provide a critical context for each of the data points in how they are related to others.
    * InfluxDB, TimeScaleDB, Prometheus, etc.

--- 
### Relational DBMS

Using a database in an application leads to extra or boilerplate code. You might see the same piece of code across applications. To reduce this duplication and standardise the code, various data models were proposed.

The most popular being the relational model.
> The relational model (RM) is an approach to managing data using a structure and language consistent with first-order predicate logic, where all data is represented in terms of tuples, grouped into relations

> This relational model has three key points
> * Store database in simple data structures (relations).
> * Access data through high-level language.
> * Physical storage left up to implementation.

### Relational Model

Main features of the relational model are:
* **Relations** - Tables -Represent data as a collection of relations or tables
* **Attributes** - Columns - Each entry in a relation can describe multiple values that are grouped as an attribute 
* **Tuples** - Rows - Represent individual data points across multiple attributes


![Relational Database](https://upload.wikimedia.org/wikipedia/commons/8/8d/Relational_model_concepts.png)

* **Degree** - Number of attributes in a relation 
  * > Student (name, age, address, phone, email)
  * Degree - 5
* **Cardinality** - Number of tuples
  * Look at our users file above
  * It has three rows and hence **cardinality is 3**

#### Properties
* **Uniqueness**
  * Each tuple is unique
  * Each attribute is unique
* **Unordered**
  * Tuples are not ordered
  * Attributes are not ordered
* **Uniform data type** - Every value in a column is of the same data type
* **Atomicity** -  Each attribute in each tuple within a relation should consist of a single value and not allow multivalued structures of the kind.