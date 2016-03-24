# JavaScript Object Notation (JSON)

- Like XML, can be thought of as a data model
- Standard for "serializing" data objects, usually in files
    - *serializing*: taking objects that are in a program and writing them in a serial fashion
- Human-readable, useful for data interchange
- An alternative to the relational data model that is more appropriate for semi-structured data
- No longer tied to JavaScript
- Parsers available for many languages

## Base constructs (recursive)

- Base values: number, string, boolean
- Objects: sets of label-value pairs (enclosed in `{}`)
- Arrays: list of values (enclosed in `[]`)

---

# Relational Model versus JSON

## Structure

- Relational: *tables*
- JSON: *sets, arrays*
    - can be nested recursively

## Schema

- Relational: *fixed in advance*
    - add the data afterwards to conform to the schema
- JSON: *no schema required*
    - schema and data are kind of mixed together (just like XML)
    - often referred to as ***self-describing data***, where the schema elements are within the data itself

## Queries

- Relational: *simple, nice languages*
- JSON: *nothing widely used*
    - typically read into a program and manipulated programmatically
    - there exists a JSON path language, JSON Query (jaql)

## Ordering

- Relational: *None*
    - fundamentally, the data in a relationship database is a set of data without an ordering within that set
- JSON: *arrays* (ordered)

## Implementation

- Relational: *Native*
    - has been around for at least 35 years
- JSON: *coupled with programming languages* (no standalone systems)
    - used in NoSQL videos as a format for reading and writing data
    - some NoSQL systems are ***document management systems***, where the documents themselves may contain JSON data and then the systems will have special features for manipulating the JSON in the document that is stored by the system

---

# XML versus JSON

## Verbosity

XML > JSON:

- largely due to closing tags in XML

## Complexity

XML > JSON:

- a lot of extra stuff in XML
- takes more time to read an entire XML specification than to read JSON

## Validity

- XML: document-type descriptors (DTDs), XML schema descriptors (XSD)
- JSON: JSON schema
    - a way to specify structure and tests conformation
    - not widely used (as of Feb. 2012)

## Programming Interface

- XML: potentially clunky
    - ***impedance mismatch***: attributes and sub-elements of an XML model don't typically match the model of data inside a programming language
    - discussed heavily in the field of database systems (one of the original criticisms of relational database systems)
- JSON: more direct mapping
    - i.e. Python dictionaries are very similar to JSON

## Querying

- XML widely used: 
    - XPath
    - XQuery
    - XSLT
- JSON:
    - JSON Path (proposal)
    - JSON Query
    - JAQL

---

# Syntatically valid JSON

## Basic structural requirements

- Sets of label-value pairs
- Arrays of values
- Base values from predefined types

## Process

1. Send JSON file to parser
2. Parser determines whether there are syntactic errors or not
3. If so, parse and manipulated via programming language

# Semantically valid JSON

## Basic structural requirements

Additionally checks whether data conforms to specified schema

- if we use JSON schema, we put specification in a separate file
- send to validator (additional step before checking syntactic errors)

---

# Questions

1. You're creating a database to contain information about students in a class (name and ID), and class projects done in pairs (two students and a project title). Should you use the relational model or JSON?

    **ANSWER**: Relational

    **EXPLANATION**: The database has a fixed structure that lends itself to tables (one table for student information and one for project information) and convenient queries in a relational language.

2. You're creating a database to contain information about students in a class (name and ID), and class projects. Projects may include any combination of students; they have a title and optional additional information such as materials, approvals, and milestones. Should you use the relational model or JSON?

    **ANSWER**: JSON

    **EXPLANATION**: The database has a complex, irregular, and possibly dynamic structure, so the flexibility of JSON is warranted.

3. You're creating a database to contain a set of sensor measurements from a two-dimensional grid. Each measurement is a time-sequence of readings, and each reading contains ten labeled values. Should you use the relational model or JSON?

    **ANSWER**: Either one is appropriate

    **EXPLANATION**: The database has a fixed structure suggesting relational, but its nested array, list, and label-value structure suggests JSON. Either may be suitable.
