# Multiple Choice


1. Why is this NOT a valid JSON object?

    ```json
    { "name": "Smiley",
      "age": 20,
      "phone": { "888-123-4567", "888-765-4321" },
      "email": "smiley@xyz.com",
      "happy": true }
    ```

2. Why is this NOT a valid JSON array?

    ```json
    [ 1, 2, "dog", "cat", true, false, [1, "dog", null], {} ]
    ```

3. Consider the following JSON Schema specification:

    ```json
    {
      "type": "object",
      "properties":
        { "ItemID": { "type":"string", "pattern":"Item*" },
          "ItemName": { "type":"string" },
          "Price": { "type":"integer", "minimum":10, "maximum":100 },
          "Sellers": { "type":"array", "maxItems":3,
                       "items": { "type":"string" }},
          "Ratings": { "type":"array",
                       "items":
                          { "type": "object",
                            "properties": {"Rater":
                                           {"type": "string", "optional": true},
                                           "Score":
                                           {"type": "integer", "minimum":1,
                                            "maxiumum":5}}}},
          "AvgRating": { "type":"number", "optional":true },
          "FreeShipping": {"type":"boolean" }
        }
    } 
    ```

    Provide the JSON data that is valid according to the JSON Schema specification above.

4. Consider the following JSON data:

    ```json
    { "A": [1,1,2,2], "B": {"C":3, "D":4}, "E":[5,6,true], "F": {"G": [null,7]} }
    ```

    Why could the following NOT be included as part of a JSON Schema specification that is satisfied by the JSON data above? Assume that every letter ("A", "B", "C", ...) appears in the JSON Schema specification exactly once.

    ```json
    "G": {"type":"array", "items": {"type":"integer"}}
    ```

---

# [View Solutions](./json-quiz-solutions.md)
