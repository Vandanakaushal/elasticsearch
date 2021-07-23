* In production we should first define index, corresponding settings and mappings and then put data in index.

```
PUT customers
{
  "settings": {
    "number_of_replicas": 1,
    "number_of_shards": 5
  },
  "mappings": {}
}
```

```
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "customers"
}
```

* Put mappings

From ES 6.0 we can only have one type of mapping per index, like here we have just for online customers. Analyzer is just used for text.

```
PUT /customers
{
  "mappings": {
      "properties": {
        "gender" : {
          "type" : "text",
          "analyzer" : "standard"
        },
        "age" : {
          "type" : "float"
        },
        "is_new" : {
          "type" : "boolean"
        },
        "name" : {
          "type" : "text",
          "analyzer" : "standard"
        }
      }
  },
  "settings": {
    "number_of_shards": 2,
    "number_of_replicas": 1
  }
}

{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "customers"
}

```

* Put data into index
```
  PUT customers/_doc/1
{
  "gender" : "Female",
  "age" : 23,
  "is_new" : false,
  "name" : "Vandana"
}

GET customers

```

* Set dynamic property to strict, so that any field which doesn't have the mapping defined will not be written

```
PUT customers/_mapping
{
  "dynamic" : "strict"
}
{
  "acknowledged" : true
}
```

* Standard analyzer, it lowercases the letters. If nothing is specified standard analyzer is used by default.
```
POST _analyze
{
  "analyzer": "standard",
  "text": ["The fox is Great."]
}

{
  "tokens" : [
    {
      "token" : "the",
      "start_offset" : 0,
      "end_offset" : 3,
      "type" : "<ALPHANUM>",
      "position" : 0
    },
    {
      "token" : "fox",
      "start_offset" : 4,
      "end_offset" : 7,
      "type" : "<ALPHANUM>",
      "position" : 1
    },
    {
      "token" : "is",
      "start_offset" : 8,
      "end_offset" : 10,
      "type" : "<ALPHANUM>",
      "position" : 2
    },
    {
      "token" : "great",
      "start_offset" : 11,
      "end_offset" : 16,
      "type" : "<ALPHANUM>",
      "position" : 3
    }
  ]
}

```
The standard analyzer consists of:

## Tokenizer
* Standard Tokenizer
## Token Filters
* Lower Case Token Filter
* Stop Token Filter (disabled by default)
