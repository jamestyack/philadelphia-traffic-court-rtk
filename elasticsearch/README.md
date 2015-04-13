ELK Stack analysis config
===

These are starter scripts that allow a user to:

* Create a suggested Elasticsearch mapping template that allows data search, aggregations (and visualizations in Kibana 4).
* Support for fast auto indexing in Elasticsearch using Logstash.

### Requirements
* Search/discovery index [Elasticsearch](https://www.elastic.co/products/elasticsearch)  
* Data pipeline processor [Logstash](https://www.elastic.co/products/logstash)
* Data visualizer (optional) [Kibana](https://www.elastic.co/products/kibana)

Install all the above tools and ensure the bin directories are on the path. Start up Elasticsearch.

### Instructions
* Create the ES mapping template using json inside ```logstash-traffic_mapping_template.json```.  This ensures that any index created dynamically by logstash will have the appropraite settings and data types. The following curl command creates a template mapping (see http://www.elastic.co/guide/en/elasticsearch/reference/current/indices-templates.html for more details)

```
curl -XPUT localhost:9200/_template/template_1 -d '
<contents of logstash-traffic_mapping_template.json here>
'
```
* Update the logstash.conf file with appropriate path to the directory where the *.tsv files you want to index are located. Also, check that all the other settings are correct (e.g. cluster name, URIs etc for Elasticsearch)
* Run ```logstash -f <path_to>/logstash.conf```

The files should index in the background. When you start up Kibana, point to the logstash-* index. Full Kibana docs online at https://www.elastic.co/products/kibana and explore the UI at http://localhost:5601
