# Introduction

- Database applications may be programmed via **frameworks** (i.e. Ruby on Rails, Django, etc.)
- DBMS may run in conjunction with **middleware** (i.e. application servers, web servers, etc.)
- Data-intensive applications may not use DBMS at all
    - Data is not always processed through query languages associated with database systems
    - Hadoop is a processing framework for running operations on data that's stored in files

# Features of a DBMS

Database Management System (DBMS) provides ...

> ... efficient, reliable, convenient, and safe multi-user storage of and acess to massive amounts of persistent data

- Massive:
    - Terabytes
    - DBMSs are designed to handle data that is residing outside of memory
- Persistent
    - Data in the database outlives the program that execute on that data
- Safe
    - Needs guarantee that managed data will stay in a consistent state
    - Failures come in all forms: hardwore, software, power, users, etc.
- Multi-user
    - Programs may allow different users to access data *concurrently*
    - ***Concurrency control*** a database mechanism that controls the way multiple users access the database; control actually occurs at the level of the data items in the database
    - Similar to *file system concurrency* or even *variable concurrency* except it's more centered around the data itself
- Convenient
    - Designed to make it easy to work with massive data
    - ***Physical Data Independence***: the way that data is actually stored and laid out on disk is independent of the way the programs think about the structure of the data
    - You could have a program that operates on a database and underneath there could be a complete change in the way the data is stored, yet the program itself would not have to be changed
    - ***High level query languages***: obey the notion called *declarative*, which is saying that in the query, you describe thwat you want out of the database but you don't need to describe the algorithm to get the data out
- Efficient
    - Has to perform thousands of queries or updates per second
- Reliable
    - 99.99999% uptime is the type of guarantee that DBMSs are making for their applications

---

# Key Concepts

## Data model

- Set or records: the data and the database is thought of as such in the relational data model
- XML documents: hierarchical structure of labeled values
- Graph data model: all data in the DB is in the form of nodes and edges

## Schema versus data

Like types and variables in a programming language

A schema ...
- sets up the structure of the database
- is typically set up at the beginning, and doesn't change very much where the data changes rapidly
- is normally set up with what's known as a ***data definition language***

## Data definition language (DDL)

- Sometimes people use higher level design tools that help them think about the design and then from there go to the data definitoin language
- Used in general to set up a schema or structure for a particular database
- Once the schema has been set up and data has been loaded, it's possible to start querying and modifying the data with what's known as ***data manipulation language***

## Data manipulation or query language (DML)

- Queries and modifies the database (duh)

---

# Key People

## DBMS Implementer

- Implements (builds) the database system itself

## Database designer

- Establishes the schema for a database
- If working on an application, the database designer has to figure out how to structure the data before the application is built
- Surprisingly difficult job when complex data is involved in an application

## Database application developer

- Builds the applications or programs that operate on the database
- Often interfacing between the eventual user and the data itself
- You can have a database with many different operating programs, i.e. a sales database where some applications are actually inserting the sales as they happen, while others are analyzing the sales
- Not necessary to have *one-to-one coupling* between programs and databases

## Database administrator

- Loads the data and keeps it running smoothly
- Very important job for large DB applications (highly paid)
- DBMS tend to have a number of tuning parameters associated with them, and getting those tuning parameters right can make a significant difference in the important performance of the database system
