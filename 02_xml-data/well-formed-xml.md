# Extensible Markup Language (XML)

- Standard for data representation and exchange
- Document format similar to HTML
    - Tags describe content instead of formatting
- Also has a streaming format/standard
    - Typically for the use in programs for admitting and consuming XML

## Basic constructs

- Tagged elements (nested)
- Attributes
    - Each element may have within its opening tag a set of attributes
    - Consist of an attribute name, the equal sign, and then an attribute value
    - Any element can have any number of attributes as long as the attribute names are unique
- Text
    - If XML is thought of as a tree, the text (strings) are the leaf elements of the tree

## Example ([`Bookstore-noDTD.xml`](./Bookstore-noDTD.xml))

```xml
<?xml version="1.0" ?>
<!--Bookstore with no DTD-->

<Bookstore>
   <Book ISBN="ISBN-0-13-713526-2" Price="85" Edition="3rd">
      <Title>A First Course in Database Systems</Title>
      <Authors>
         <Author>
            <First_Name>Jeffrey</First_Name>
            <Last_Name>Ullman</Last_Name>
         </Author>
         <Author>
            <First_Name>Jennifer</First_Name>
            <Last_Name>Widom</Last_Name>
         </Author>
      </Authors>
   </Book>
   <Book ISBN="ISBN-0-13-815504-6" Price="100">
      <Remark>
      Buy this book bundled with "A First Course" - a great deal!
      </Remark>
      <Title>Database Systems: The Complete Book</Title>
      <Authors>
         <Author>
            <First_Name>Hector</First_Name>
            <Last_Name>Garcia-Molina</Last_Name>
         </Author>
         <Author>
            <First_Name>Jeffrey</First_Name>
            <Last_Name>Ullman</Last_Name>
         </Author>
         <Author>
            <First_Name>Jennifer</First_Name>
            <Last_Name>Widom</Last_Name>
         </Author>
      </Authors>
   </Book>
</Bookstore>
```

---

# Relational Model versus XML

## Structure

- Relational: *tables*
- XML: *hierarchical trees or graphs*

## Schema

- Relational: *fixed in advance*
    - add the data afterwards to conform to the schema
- XML: *flexible, self-describing*
    - the schema and the data are mixed together to some extent
    - tags on elements are telling you the kind of data you'll have, and you can have a lot of irregularity
    - many mechanisms for introducing schemas into XML but not required

## Queries

- Relational: *simple, nice languages*
- XML: *less simple*

## Ordering

- Relational: *None*
    - fundamentally, the data in a relationship database is a set of data without an ordering within that set
- XML: *Implied*
    - XML can be thought of as either a document model or a stream model
    - Either case, the nature of the XML being laid out in a document as we have here (or being in a stream) induces an order

## Implementation

- Relational: *Native*
    - has been around for at least 35 years
- XML: *Add-on*
    - most likely a layer over the relational database system
    - entering and querying data in XML will be translated into a relational implementation

---

# *Well-Formed* XML

## Basic structural requirements:

- Single root element
- Matched tags, proper nesting
- Unique attributes within elements

## XML Parser

- The parser will check the basic structure of a XML document
- If not well-formed, parser will send an error
- Else, the output is parsed XML, which is shown via several standards:
    - **DOM**: document-object model is a programmatic interface for traversing the tree implied by XML
    - **SAX**: more of a stream model for XML

## Displaying XML

Use ruled-basd language to translate to HTML, which we can then render in a browser

- **Cascading stylesheets (CSS)**
- **Extensible stylesheet language (XSL)**

### Process

1. Send XML document to CSS or XSL interpreter
2. Apply rules that will be used on that particular document
3. Get output as HTML document
4. Render HTML in browser

---


# Questions

1. You're creating a database to contain information about university records: students, courses, grades, etc. Should you use the relational model or XML?
    - The database has a simple structure fixed in advance, so it's amenable to the relational model.

2. You're creating a database to contain information for a university web site: news, academic announcements, admissions, events, research, etc. Should you use the relational model or XML?
    - The database has an unpredictable, complex, dynamic structure, so the flexibility of XML is warranted.

3. You're creating a database to contain information about family trees (ancestry). Should you use the relational model or XML?
    - The database has a fixed structure suggesting relational, but it's strictly hierarchical suggesting XML. Either may be suitable.
