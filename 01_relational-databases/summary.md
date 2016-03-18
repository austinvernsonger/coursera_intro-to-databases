### Atomic types

It's typical for relational databases to have just just atomic types in their attributes, but many database systems do also support structured types inside attributes.

### Enumerated domain

Most relational databases have a concept of enumerated domain. For example, the attribute `state` might be an enumerated domain for the 50 abbreviations for states.

### Schema

Schema of a database is the structure of the relation. It includes the name of the relation and the attributes of the relation and the types of those attributes.

### Instance

The instance is the actual contents of the table at a given point in time.

Typically, you set up a schema in advance, then the instances of the data will change over time.

### NULL

Null values are used to denote that a particular value is maybe unknown or undefined.

Null values are useful but one has to be very careful in a database sytem when running queries over relations that have null values. For example, `attribute == value OR attribute != value` won't include values that are `NULL`.

### Key

A key is an attribute of a relation where every value for that attribute is unique. Every tuple is going to have a unique ID. For example, a student ID number in a student relation may very well be a key (since each student usually has a unique ID).

Why it's important to have attributes that are identified as keys:

- If you want to run a query to get a specific tuple out of the database, you would do so by asking for that tuple by its key.
- Database systems, for efficiency, tend to build special index structures or store the database in a particular way so it's very fast to find a tuple based on its key
- If one relation in a relational database wants to refer to tuples of another, there's no concept of pointer in relational databases. Therefore, the first relation will typically refer to a tuple in the second relation by its unique key.

### Steps in creating and using a (relational) database

1. Design schema; create using DDL (data definition language)
2. "Bulk load" initial data
    - fairly common for database to be initially loaded from data that comes from outside source
3. Repeat: execute queries and modifications

### Ad-hoc queries in high-level language

**ad hoc** = posing queries that one didn't think of in advance; unnecessary to write long programs for specific queries

Rather, the language can be used to pose a query as you think about what you want to ask.

- Some easy to pose; some a bit harder
- Some easy for DBMS to execute efficiently; some harder (not correlated with above)
- "Query language" also used to modify data

#### Example

- All students with GPA >3.7 applying to Stanford and MIT only
- All engineering departments in CA with &lt; 500 applicants
- College with highest average accept rate over last 5 years

### Queries return relations (*compositional, closed*)

When you get back the same type of object that you query, that's known as ***closure*** of the language

***Compositionality*** is the abillity to run a query over the result of our previous query.


### Query Languages

- ***Relational Algebra***: formal
    - Statement: *IDs of students with GPA > 3.7 applying to Stanford*
    - Expression: ![\pi_{ID} = \sigma_{(GPA > 3.7) \wedge (cName = "Stanford")} = (student \bowtie Apply)](http://www.sciweavers.org/tex2img.php?eq=%24%24%5Cpi_%7BID%7D%20%3D%20%5Csigma_%7B%5Cleft%5B%20%28GPA%20%3E%203.7%29%20%5Cwedge%20%28cName%20%3D%20%22Stanford%22%29%20%5Cright%5D%7D%20%3D%20%28student%20%5Cbowtie%20Apply%29%24%24&bc=White&fc=Black&im=png&fs=12&ff=fourier&edit=0)

- ***SQL***: actual/implemented
```
Select Student.ID
From Student, Apply
Where Student.ID=Apply.ID
And GPA>3.7 and college='Stanford'
```
