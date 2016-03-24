# Demo

- Constructs and syntactic correctness
- Flexibility of data model
- JSON Schema, validation

# Example

## [`Bookstore.json`](./data/Bookstore.json)

JSON data representing books and magazines

```json
{ "Books":
  [
    { "ISBN":"ISBN-0-13-713526-2",
      "Price":85,
      "Edition":3,
      "Title":"A First Course in Database Systems",
      "Authors":[ {"First_Name":"Jeffrey", "Last_Name":"Ullman"},
                  {"First_Name":"Jennifer", "Last_Name":"Widom"} ] }
    ,
    { "ISBN":"ISBN-0-13-815504-6",
      "Price":100,
      "Remark":"Buy this book bundled with 'A First Course' - a great deal!",
      "Title":"Database Systems:The Complete Book",
      "Authors":[ {"First_Name":"Hector", "Last_Name":"Garcia-Molina"},
                  {"First_Name":"Jeffrey", "Last_Name":"Ullman"},
                  {"First_Name":"Jennifer", "Last_Name":"Widom"} ] }
  ],
  "Magazines":
  [
    { "Title":"National Geographic",
      "Month":"January",
      "Year":2009 }
    ,
    { "Title":"Newsweek",
      "Month":"February",
      "Year":2009 }
  ]
}
```

## [`BookstoreSchema.json`](./data/BookstoreSchema.json)

- The structure of the schema file reflects the structure of the data file it's describing.
- The outermost constructs in the schema file are the outermost in the data file and as we nest, it parallels the nesting.
- In JSON Schema, `additionalProperties: true | false` determines whether said data are allowed to have any properties beyond those that are specified in the schema.
- Many parsers actually do enforce that labels or properties need to be unique within objects, even though technically syntatically correct JSON does allow multiple copies.
- Numeric boundaries for integer types: 

       "Price": {
           "type": integer,
           "minimum": min,
           "maximum": max
       }

- We can constrain strings using a pattern (similar to regex), and we can constrain any type by enumerating the values that are allowed 

       "Month": {
           "type": string,
           "enum": ["January", "February", "March", ... ]
       }


```json
{ "type":"object",
  "properties": {
     "Books": {
        "type":"array",
        "items": {
           "type":"object",
           "properties": {
              "ISBN": { "type":"string", "pattern":"ISBN*" },
              "Price": { "type":"integer",
                         "minimum":0, "maximum":200 },
              "Edition": { "type":"integer", "optional": true },
              "Remark": { "type":"string", "optional": true },
              "Title": { "type":"string" },
              "Authors": { 
                 "type":"array",
                 "minItems":1,
                 "maxItems":10,
                 "items": {
                    "type":"object",
                    "properties": {
                       "First_Name": { "type":"string" },
                       "Last_Name": { "type":"string" }}}}}}},
     "Magazines": {
        "type":"array",
        "items": {
           "type":"object",
           "properties": {
              "Title": { "type":"string" },
              "Month": { "type":"string",
                         "enum":["January","February"] },
              "Year": { "type":"integer" }}}}
}}
```
