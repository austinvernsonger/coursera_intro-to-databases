# Solutions to [XML Quiz](./xml-quiz.md)

1. **ANSWER**:

    ```xml
    <tasklist>
      <task name="eat"></task>
      <task name="drink"></task>
      <task name="play"></task>
    </tasklist>
    ```

    **EXPLANATION**:

    Well-formed XML must follow these rules (along with others):
    - There must be exactly one top level element.
    - All opening tags must be closed.
    - All elements are properly nested i.e., there are no interleaved elements.
    - Attribute values must be enclosed in single or double quotes.

2. **ANSWER**:

    ```xml
    <!ELEMENT INFO (NAME*,ADDR,PHONE+)> 
    ```
    
    **EXPLANATION**:
    
    In the XML snippet, the info element has one address subelement and two phone subelements, in that order. Thus, in the DTD the list of components for `INFO` must include `ADDR`, `ADDR*`, `ADDR+`, or `ADDR?` followed by `PHONE*` or `PHONE+`. Interspersed with these may be any elements that are not required to appear-- that is, any components with a `?` or `*`. Thus, we might also have components like `NAME*` or `MANAGER?` at any point in the list.

3. **ANSWER**:

    ```xml
    <!ATTLIST PHONE owner IDREF #REQUIRED> 
    ```
    
    **EXPLANATION**:
    
    The correct choices (i.e., the erroneous DTD snippets) are based on two rules:
    
    1. A `#REQUIRED` attribute must appear in every element.
    2. An attribute can have types `CDATA`, `ID`, or `IDREF(S)`, but not `#PCDATA`.

  The incorrect choices (i.e., the snippets that could appear in a DTD), are either optional attributes (#IMPLIED) or are required attributes of a proper type.

4. **ANSWER**:

    ```
    A B /B B /B C B /B D /D /C /A 
    ```

    **EXPLANATION**:

    According to the DTD, an A element has within it one or more B subelements, and then a C element. Within the C element is zero or one B elements followed by exactly one D element. In terms of regular expressions, the tag sequences we can see are:
    
    ```
    A (B /B)(B /B)* C (D /D | B /B D /D) /C /A.
    ```

    Some text may appear between each B-/B pair and each D-/D pair, but text may not appear elsewhere.

5. **ANSWER**:

    Only the second

    **EXPLANATION**:

    Focus on the ID and IDREF attributes: A valid document needs to have unique values across ID attributes. An IDREF attribute can refer to any existing ID attribute value.

6. **ANSWER**:

    ```xml
    <person>
      <fname>John</fname>
      <initial>Q</initial>
      <lname>Public</lname>
      <address>123 Public Avenue, Seattle, WA 98001</address>
      <major>Computer Science</major>
    </person> 
    ```

    **EXPLANATION**:

    This question deals with the `xs:element`, `xs:sequence`, and `xs:choice` elements in XML Schema. In order for XML to be valid according to the specified schema:
    - The elements contained in a sequence must appear in exactly the same order as specified in the `xs:sequence`.
    - Exactly one of the elements contained in an `xs:choice` must appear.
    - If an element specifies a `minOccurs` attribute, the XML must contain at least that many instances of the element.
    - If an element specifies a `maxOccurs` attribute, the XML must not contain more than that many instances of the element.
    - If `minOccurs` and `maxOccurs` are not specified, their default value is 1.
    - Elements not defined as a part of a sequence or choice cannot occur inside the corresponding `xs:sequence` and `xs:choice`.
    
  The given schema specifies the following constraints:
    - The "fname", "initial", "lname", and "address" elements must occur in that sequence.
    - The "initial" element is optional due to its `minOccurs` value being 0.
    - The "address" element can occur either 1 or 2 times due to its `maxOccurs` value being 2.
    - After the "address" element, either exactly one "major" element or exactly 2 "minor" elements can occur, but not both.
    - Elements not defined as a part of this schema specification are not allowed to occur as a part of the "person" element.
    
  Here is an example of valid XML for this schema:

    ```xml
    <person>
      <fname>John</fname>
      <initial>Q</initial>
      <lname>Public</lname>
      <address>123 Public Avenue</address>
      <address>Seattle, WA 98001</address>
      <major>Computer Science</major>
    </person> 
    ```
