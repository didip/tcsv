# Typed CSV (.tcsv)

## Objectives

`.tcsv` explores the idea of data-exchange format that is simpler, streamable, more compact, easier to read, gzip friendlier than JSON.


## Examples

### On The Wire
```
id|go:int|py:types.IntType,username|go:string|py:types.StringType,is_awesome|go:bool|py:types.BooleanType,awesome_score|go:float64|py:types.FloatType,description|go:string|py:types.StringType,created|go:time.Time|py:datetime.datetime,powers|go:[]string|py:types.ListType,milestones|go:map[string]int|py:types.DictType
1,goku,true,9001.0,"The most powerful alien, in the universe.","2006-01-02T15:04:05",["super saiyan","infinite level up", "main character"],{"death": 2}
2,vegeta,,9000.999,"The 2nd most powerful alien, in the universe.","2006-01-02T15:04:05",["super saiyan","infinite level up"],{"death": 2}
```

### Go Struct
```go
type User struct {
    ID           int            `tcsv:"id"`
    Username     string         `tcsv:"username"`
    IsAwesome    bool           `tcsv:"is_awesome"`
    AwesomeScore float64        `tcsv:"awesome_score"`
    Description  string         `tcsv:"description"`
    Created      time.Time      `tcsv:"created"`
    Powers       []string       `tcsv:"powers"`
    Milestones   map[string]int `tcsv:"milestones"`
}
```

### Javascript Object

Javascript does not need type information.

The parser will do it's best to represent data, any missing values will be interpreted as `null`.

```javascript
[
    {
        "id": 1,
        "username": "goku",
        "is_awesome": true,
        "awesome_score": 9001.0,
        "description": "The most powerful alien, in the universe.",
        "created": new Date('2006-01-02T15:04:05'),
        "powers": ["super saiyan","infinite level up", "main character"],
        "milestones": {"death": 2}
    },
    {
        "id": 2,
        "username": "vegeta",
        "is_awesome": null,
        "awesome_score": 9000.999,
        "description": "The 2nd most powerful alien, in the universe.",
        "created": new Date('2006-01-02T15:04:05'),
        "powers": ["super saiyan","infinite level up"],
        "milestones": {"death": 2}
    }
]
```

## Specifications

### Header
```
type:   <language-file-extension>:<language-type>
field:  <name>|type|type|...
fields: field,field,...
```

### Values

1. Follow regular `.csv` parsing rules.

2. `[1,2,3]` denotes `array`, `list`, `slice`, or similar concept.

3. `{"key": "value"}` denotes `map`, `hash`, `dict`, or similar concept.

4. Datetime is represented as string ISO 8601.

5. Empty value denotes `nil`, `null`, `None`, or similar concept.


## Limitations

* Nested objects.
