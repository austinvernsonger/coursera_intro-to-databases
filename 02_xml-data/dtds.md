# *Valid* XML

Has to adhere to the basic structural requirements as well-formed XML, but it also adheres to ***content-specific specification***

- **Document Type Descriptor (DTD)**
- **XML Schema Description (XSD)**

## Parsing Valid XML

1. Send XML document to a validating XML parser
2. Add additional input to the process (a specification); either a DTD or an XSD
3. If structural requirements not met; output error about the lack of good form
4. If content specific specifications not met; output invalid error

---

# Document Type Descriptor (DTD)

- Grammar-like language for specifying elements, attributes, nesting, ordering, # of occurences
- Also allows special attribute types such as `ID` and `IDREF(S)`
    - effectively allows one to specify pointers within a document, although these *pointers are untyped*

---

# DTD/XSD versus none (well-formed)

### Pros

- Programs can assume structure
    - programs can be simpler because they don't have to do a lot of error checking on data
- CSS/XSL 
- Specification language for conveying what XML might need to look like
    - i.e. data exchange using XML => companies can use the DTD as a specification for what the XML needs to look like when it arrives at the program it's going to operate on
- Documentation
    - Use one of the specifications to document what the data itself looks like
- Essentially enjoys benefits of strongly typed data as opposed to loosely-typed data

### Cons

- Flexibility
    - DTD makes XML data have to conform to a specification
    - Allows ease of change in data formats without running into errors
- DTDs can potentially be messy
    - especially for *irregular* documents
- XSDs can potentially become VERY messy
    - it's possible to have a document where the specification is much, much larger than the document itself
- Essentially enjoys benefits of nil typing

---

# Examples 

## [`Bookstore-DTD.xml`](./Bookstore-DTD.xml)

Notice a few things:

- The DTD is specified before the XML in the same file. However, it is also possible to specify DTDs in separate files.
- The first grammar-like construct `(Book | Magazine)*` are a little bit like regular expressions
    - `(Book | Magazine)` means that a bookstore element has a sub-element (any number of elements) that is/are called `Book` or `Magazne`
    - `*` means zero or more instances
- `CDATA`: type of data, in this case a string
- `#REQUIRED`: has to be present; `#IMPLIED`: doesn't have to be present
- `#PCDATA` is when you have a leaf that consists of text data in the XML tree
- `(Author+)`: one or more instances of author sub-elements

```xml
<?xml version="1.0" ?>
<!-- Bookstore with DTD                    -->
<!-- Try changes:                          -->
<!--   Make Edition required               -->
<!--   Swap order of First_Name, Last_Name -->
<!--   Add empty Remark                    -->
<!--   Add Magazine, omit closing tag      -->

<!DOCTYPE Bookstore [
   <!ELEMENT Bookstore (Book | Magazine)*>
   <!ELEMENT Book (Title, Authors, Remark?)>
   <!ATTLIST Book ISBN CDATA #REQUIRED
                  Price CDATA #REQUIRED
                  Edition CDATA #IMPLIED>
   <!ELEMENT Magazine (Title)>
   <!ATTLIST Magazine Month CDATA #REQUIRED Year CDATA #REQUIRED>
   <!ELEMENT Title (#PCDATA)>
   <!ELEMENT Authors (Author+)>
   <!ELEMENT Remark (#PCDATA)>
   <!ELEMENT Author (First_Name, Last_Name)>
   <!ELEMENT First_Name (#PCDATA)>
   <!ELEMENT Last_Name (#PCDATA)>
]>

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
      <Remark>
         Buy this book bundled with "A First Course" - a great deal!
      </Remark>
   </Book>
</Bookstore>
```

## [`Bookstore-IDREFs.xml`](./Bookstore-IDREFs.xml)

As before, the DTD is specified before the XML in the same file.

Notice a few things:

- Instead of having authors as subelements of book elements, have authors listed separately, and then effectively point from books to the authors of the books
- Add `Ident` attribute to authors, give a string value to that attribute that we're going to use effectively for the pointers in the book
- Authors is an `IDREF` attribute where its value can refer to one or more strings that are `ID` attributes
- `(# PCDATA | BookRef)` is the type of construct that can be used to mix strings and sub-elements within an element
- `ID` attributes need to all be unique
- A singular `IDREF` requires that the string has to have exactly one `ID` value
- Plural `IDREF`s require `ID` values to be separated by spaces

```xml
<?xml version="1.0" ?>
<!-- Bookstore using ID/IDREFs      -->
<!-- Try changes:                   -->
<!--   Ident JU to HG               -->
<!--   BookRef to HG                -->
<!--   Add second BookRef in Remark -->

<!DOCTYPE Bookstore [
   <!ELEMENT Bookstore (Book*, Author*)>
   <!ELEMENT Book (Title, Remark?)>
   <!ATTLIST Book ISBN ID #REQUIRED
                  Price CDATA #REQUIRED
                  Authors IDREFS #REQUIRED>
   <!ELEMENT Title (#PCDATA)>
   <!ELEMENT Remark (#PCDATA | BookRef)*>
   <!ELEMENT BookRef EMPTY>
   <!ATTLIST BookRef book IDREF #REQUIRED>
   <!ELEMENT Author (First_Name, Last_Name)>
   <!ATTLIST Author Ident ID #REQUIRED>
   <!ELEMENT First_Name (#PCDATA)>
   <!ELEMENT Last_Name (#PCDATA)>
]>

<Bookstore>
   <Book ISBN="ISBN-0-13-713526-2" Price="100" Authors="JU JW">
      <Title>A First Course in Database Systems</Title>
   </Book>
   <Book ISBN="ISBN-0-13-815504-6" Price="85" Authors="HG JU JW">
      <Title>Database Systems: The Complete Book</Title>
      <Remark>
         Amazon.com says: Buy this book bundled with
         <BookRef book="ISBN-0-13-713526-2" /> - a great deal!
      </Remark>
    </Book>
    <Author Ident="HG">
      <First_Name>Hector</First_Name>
      <Last_Name>Garcia-Molina</Last_Name>
   </Author>
   <Author Ident="JU">
      <First_Name>Jeffrey</First_Name>
      <Last_Name>Ullman</Last_Name>
   </Author>
   <Author Ident="JW">
      <First_Name>Jennifer</First_Name>
      <Last_Name>Widom</Last_Name>
   </Author>
</Bookstore>
```

## Command-line validity checking

Use `xmllint` for *linting* (error-checking):

```sh
$ xmllint --valid --noout Bookstore-DTD.xml    # missing data in #REQUIRED field

Bookstore-DTD.xml:59: element Book: validity error : Database Systems: The Complete Book does not carry attribute Edition
    </Book>
           ^
$ xmllint --valid --noout Bookstore-DTD.xml    # no closing tags

Bookstore-DTD.xml:64: parser error: Premature end of ...

```

If it doesn't return anything, there are no errors, and you should be proud.

---

