```
PUT /vehicles/car/1
{
  "make": "Benz",
  "color": "Black"
}
```

```
GET _cat/indices

GET vehicles/car/1
```

Documents are immutable. 

* put command overwrites existing doc, if doc is not present it will create a new one
* post merges the update with old record.

```
POST vehicles/car/1/_update
{
  "doc":{
    "make" : "Honda",
    "color" : "Black"
  }
}

```
* Following will give document missing exception

```
POST vehicles/car/3/_update
{
  "doc":{
    "make" : "Honda",
    "color" : "Black"
  }
}
```

* If we delete a record, ES will mark it as deleted but the space is not immediately freed. It does the purging but not immediately.
* To delete a document execute following command:

```
DELETE vehicles/car/1

{
  "_index" : "vehicles",
  "_type" : "car",
  "_id" : "1",
  "_version" : 9,
  "result" : "deleted",
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 9,
  "_primary_term" : 1
}

```

* To delete an index use following command:
```
DELETE vehicles
{
  "acknowledged" : true
}
```

* To get structure of index

```
GET vehicles

{
  "vehicles" : {
    "aliases" : { },
    "mappings" : {
      "properties" : {
        "color" : {
          "type" : "text",
          "fields" : {
            "keyword" : {
              "type" : "keyword",
              "ignore_above" : 256
            }
          }
        },
        "make" : {
          "type" : "text",
          "fields" : {
            "keyword" : {
              "type" : "keyword",
              "ignore_above" : 256
            }
          }
        }
      }
    },
    "settings" : {
      "index" : {
        "routing" : {
          "allocation" : {
            "include" : {
              "_tier_preference" : "data_content"
            }
          }
        },
        "number_of_shards" : "1",
        "provided_name" : "vehicles",
        "creation_date" : "1627033117595",
        "number_of_replicas" : "1",
        "uuid" : "blFWeutVQb6aD83RAQedWg",
        "version" : {
          "created" : "7130499"
        }
      }
    }
  }
}
```

* We can't index multiple types of document into an index as mappings are rejected.
* Search based on specific condtion
```
GET vehicles/_search
{
  "query":{
    "term":{
      "make":"benz1"
    }
  }
}
```
