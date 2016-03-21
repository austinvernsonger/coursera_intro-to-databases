# XML Schema (XSD)

- Extensive language
- Like DTDs, can specify elements, attributes, nesting, ordering, # of occurences
- Allows data types, keys, (typed) pointers, etc.
- Unlike DTDs, is written in XML

## Key Features

1. Typed values
2. Key declarations
    - in DTDs, `ID`s were globally unique values that could be used to identify specific elements
3. References (`keyref`)
    - similar to pointers but a little more powerful
4. Occurrence constraints
    - `minOccurs="0"`: 0 instances at minimum (not required)
    - `maxOccurs="unbounded"`: no upper limits

---

# Example 

### [`Bookstore-XSD.xml`](./data/Bookstore-XSD.xml) with [`Bookstore.xsd`](./data/Bookstore.xsd)

- Instead of using `IDREF` attributes to refer from books to authors, we now back our back having an author's sub-element with the two authors underneath and then those authors themselves have what are effectively *pointers to the identifiers* for the authors
- The XSD is in a separate file from the actual XML data

```xml
<?xml version="1.0" ?>
<!-- Bookstore using XML Schema (Bookstore.xsd)             -->
<!-- Notice / try changes:                                  -->
<!--   Price is integer (search 'Price')                    -->
<!--     Make it not an integer                             -->
<!--   Key declarations (search 'key ')                     -->
<!--     Change JU to HG                                    -->
<!--     Change second ISBN to HG                           -->
<!--   References (search 'keyref')                         -->
<!--     Change first authIdent JU to foo                   -->
<!--     Change first authIdent JU to JW                    -->
<!--     Change BookRef to JW                               -->
<!--   Occurrence constraints (search 'occurs', default=1)  -->
<!--     Change to 0 authors                                -->
<!--     Change to 2 remarks                                -->

<Bookstore>
   <Book ISBN="ISBN-0-13-713526-2" Price="100">
      <Title>A First Course in Database Systems</Title>
      <Authors>
         <Auth authIdent="JU" />
         <Auth authIdent="JW" />
      </Authors>
   </Book>
   <Book ISBN="ISBN-0-13-815504-6" Price="85">
      <Title>Database Systems: The Complete Book</Title>
      <Authors>
         <Auth authIdent="HG" />
         <Auth authIdent="JU" />
         <Auth authIdent="JW" />
      </Authors>
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
