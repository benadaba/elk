ELK ( Elastic Logtash Kibana)
ElasticSearch, Filebeat & Kibanna

### ElasticSearch:
https://www.elastic.co/
- Elasticsearch is used for storing, searching and analysing large volumes of data in realtime. 
- it is a distributed , RESTFUL search and analytic engine
- It is built on top of Apache Lucene and provides distributed , scalable , architecture

docker image: 
```
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.16.3
```

```
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.16.3
```


### Filebeat:
https://www.elastic.co/beats/filebeat
docker run -d --name filebeat -v /home/mobaxterm/MyDocuments/datapandas/logs_files/filebeat.yml:/usr/share/filebeat/filebeat.yml docker.elastic.co/beats/filebeat:7.16.3

```
docker run -d --name filebeat --link elasticsearch:elasticsearch -v  /home/mobaxterm/MyDocuments/datapandas/logs_files/filebeat.yml:/usr/share/filebeat/filebeat.yml docker.elastic.co/beats/filebeat:7.16.3

```


- lightweight shipper for forwarding and centralizing log data
-Its part ofthe Elastic stack ( formerly known as ELK stack)
- Filebeat can tail log files, parse and filter logs and send them to Elasticsearch or Logstash for further processing
Whether you’re collecting from security devices, cloud, containers, hosts, or OT, 
Filebeat helps you keep the simple things simple by offering a lightweight way to forward and centralize logs 
and files.

configuration file.
filebeat.yml
```
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /home/mobaxterm/MyDocuments/datapandas/logs_files/*.log
setup.ilm.enabled: false
setup.template.overwrite: true
output.elasticsearch:
  hosts: ["localhost:9200"]

setup.template:
  name: 'foo'
  pattern: 'foo-*'
  enabled: false

```

### Kibana:
https://www.elastic.co/kibana

```
docker run -d --name kibana -p 5601:5601 docker.elastic.co/kibana/kibana:7.16.3
```

```
docker run -d --name kibana --link elasticsearch:elasticsearch -p 5601:5601 docker.elastic.co/kibana/kibana:7.16.3
```

- kibaa is a data visualization and exploration tool for Elasticsearch 
- It provides a web interface for searching , and analysing, and visualising data stored in Elasticsearch
- create dashboards, visualizations and reports based on data.

http://localhost:5601



3 ways of setting ELK up. 
Docker links

docker compose
k8s
