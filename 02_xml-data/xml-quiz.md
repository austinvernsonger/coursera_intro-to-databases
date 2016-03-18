# Multiple Choice (6 points)


1. Provide a well-formed XML that satisfies the following conditions:
    - It has a root element "tasklist"
    - The root element has 3 "task" subelements
    - Each of the "task" subelements has an attribute named "name"
    - The values of the "name" attributes for the 3 tasks are "eat", "drink", and "play"

2. An XML document contains the following portion:
    
    ```xml
    ...
         <INFO>
             <ADDR>101 Maple St.</ADDR>
             <PHONE>555-1212</PHONE>
             <PHONE>555-4567</PHONE>
         </INFO>
    ...
    ```
    
    Which of the following could be the `INFO` element specification in a DTD that the document matches?

3. An XML document contains the following portion:
    
    ```xml
    <EMP name = "Kermit">
        <ADDR>123 Sesame St.</ADDR>
        <PHONE type = "cell">555-1212</PHONE>
    </EMP>
    ```

    Which of the following could NOT be part of a DTD that the document matches? Note that there can be multiple `ATTLIST` declarations for a single element type; do not assume the only attributes allowed for an element type are the ones shown in the answer choice. 

4. Here is a DTD:

    ```xml
    <!DOCTYPE A [
        <!ELEMENT A (B+, C)>
        <!ELEMENT B (#PCDATA)>
        <!ELEMENT C (B?, D)>
        <!ELEMENT D (#PCDATA)>
    ]>
    ```

    Which of the following sequences of opening and closing tags matches this DTD? Note: In actual XML, opening and closing tags would be enclosed in angle brackets, and some elements might have text subelements. This quiz focuses on the element sequencing and interleaving specified by the DTD. 

5. Here is an XML DTD:

    ```xml
    <!DOCTYPE meal [
        <!ELEMENT meal (person*,food*,eats*)>
        <!ELEMENT person EMPTY>
        <!ELEMENT food EMPTY>
        <!ELEMENT eats EMPTY>
        <!ATTLIST person name ID #REQUIRED>
        <!ATTLIST food name ID #REQUIRED>
        <!ATTLIST eats diner IDREF #REQUIRED dish IDREF #REQUIRED>
    ]>
    ```

    Which of the following documents match the DTD?

    - 

        ```xml
        <meal>
          <person name="Alice"/>
          <food name="salad"/>
          <eats diner="Alice" dish="salad"/>
          <person name="Bob"/>
          <food name="salad"/>
          <eats diner="Bob" dish="salad"/>
          <person name="Carol"/>
          <food name="sandwich"/>
          <eats diner="Carol" dish="sandwich"/>
        </meal>
        ```
    - 
        
        ```xml
        <meal>
          <person name="Alice"/>
          <person name="Bob"/>
          <person name="Carol"/>
          <person name="Dave"/>
          <food name="salad"/>
          <food name="turkey"/>
          <food name="sandwich"/>
          <eats diner="Alice" dish="turkey"/>
          <eats diner="Bob" dish="salad"/>
          <eats diner="turkey" dish="Dave"/>
        </meal>
        ```
    - 
        
        ```xml
        <meal>
          <person name="Alice"/>
          <person name="Bob"/>
          <food name="salad"/>
          <eats diner="Alice" dish="food"/>
          <eats diner="Bob" dish="food"/>
        </meal>
        ```

6. Study the following XML Schema specification:
    
    ```xml
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:element name="person">
        <xs:complexType>
          <xs:sequence>
            <xs:element name="fname" type="xs:string"/>
            <xs:element name="initial" type="xs:string"
                minOccurs="0"/>
            <xs:element name="lname" type="xs:string"/>
            <xs:element name="address" type="xs:string"
                maxOccurs="2"/>
            <xs:choice>
              <xs:element name="major" type="xs:string"/>
              <xs:element name="minor" type="xs:string"
                  minOccurs="2" maxOccurs="2"/>
            </xs:choice>
          </xs:sequence>
        </xs:complexType>
      </xs:element>
    </xs:schema> 
    ```
    
    Provide a XML that is valid according to the XML Schema specification.

---

# [View Solutions](./xml-quiz-solutions.md)
