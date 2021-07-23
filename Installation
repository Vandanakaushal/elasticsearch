* Download Java
* Download elastic
* Download kibana
* To bring up elastic, go to elastic search dir and execute bin/elasticsearch
* To check if elastic search is running execute following command:
vankaush@VANKAUSH-M-N1C7:~$ curl http://localhost:9200/
```
{
  "name" : "VANKAUSH-M-N1C7",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "ksPLXoSgQc2K9VxmpG0PJg",
  "version" : {
    "number" : "7.13.4",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "c5f60e894ca0c61cdbae4f5a686d9f08bcefc942",
    "build_date" : "2021-07-14T18:33:36.673943207Z",
    "build_snapshot" : false,
    "lucene_version" : "8.8.2",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```
* Before running kibana, go to kibana folder->config->kibana.yaml and edit the this file. Basically uncomment the following line, thiw way kibana will be connected to
this elastic search's instance.
elasticsearch.hosts: ["http://localhost:9200"]
* Run kibana
bin/kibana
* You will get kibana url from the logs which you can paste in UI and go to dev tools.
* Kibana can only run if elastic search is running. if we turn off elastic search then kibana will also not work. We cannot even enter any username password.

