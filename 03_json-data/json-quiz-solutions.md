# Solutions to [JSON Quiz](./json-quiz.md)

1. **EXPLANATION**:

    In JSON objects, all labels (property names) must be quoted, and all label-value pairs must be separated by commas. Values in label-value pairs can be numbers, quoted strings, true, false, null, objects, or arrays. Objects and arrays may be empty.

2. **EXPLANATION**:

   A JSON array is a comma-separated, [] enclosed list of JSON values. Values can be numbers, quoted strings, true, false, null, objects, or arrays. Objects and arrays may be empty. Objects must be a set of label-value pairs.

3. **ANSWER**:

    ```json
    { "ItemID": "Item123",
      "ItemName": "desk",
      "Price": 50,
      "Sellers": ["Amy","Ben"],
      "Ratings": [{"Rater":"Amy", "Score":5}, {"Score":1},
                  {"Rater":"Carl", "Score":4}],
      "AvgRating": 10.0,
      "FreeShipping": true }
    ```

    **EXPLANATION**:
    
    ON data that is valid according to the JSON Schema specification must have: an itemID that is a string beginning with "Item"; a Price that is an integer between 10 and 100; an array of between 0 and 3 Sellers; an array of 0 or more Ratings, each of which is either a Rater-Score pair, or just a Score, where scores are integers between 1 and 5; a FreeShipping designation of either true or false. (AvgShipping, a real number, is optional.)

4. **EXPLANATION**:

    The following JSON Schema specification is valid for the given data:
    
    ```json
    { "type": "object",
      "properties": {
        "A": {"type":"array", "minItems":4,
              "maxItems":4, "items":{"type":"integer"}},
        "B": {"type":"object",
              "properties": {"C": {"type":"integer"}, "D": {"type":"integer"}}},
        "E": {"type":"array", "items": {"type":["integer","boolean"]}},
        "F": {"type":"object",
              "properties": {"G": {"type":"array",
                                   "items": {"type":["null","integer"]}}}}
      }
    }
    ```
    
    Changing the minimum and/or maximum number of items in "A" is valid as long as four items are permitted. Alternative types may be added (e.g., replacing "integer" with ["integer","string"]) without violating validity.
