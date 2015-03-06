# Static ElasticSearch Cluster

This demo shows how to create an ElasticSearch cluster with tree nodes using Docker Compose.

You need to install [Docker and Docker Compose](https://docs.docker.com/compose/#installation-and-set-up) first

## Create the cluster
To create the cluster after cloning this repository:
```
docker-compose up -d
```
This command creates tree docker containers with an ElasticSearch instance inside each.

You can check the containers status using the command:
```
docker-compose ps
```

You can also check the cluster health by asking ElasticSearch: [http://localhost:9201/_cluster/health](http://localhost:9201/_cluster/health)

## Install head plugin
If you want to install the head plugin, you need to execute the following command:
```
docker-compose run --rm e1 /elasticsearch/bin/plugin -i mobz/elasticsearch-head
```

You can now check the cluster health with the head plugin: [http://localhost:9201/_plugin/head/](http://localhost:9201/_plugin/head/)

## Loading some data
You can load data inside the cluster using the Bulk API and the sample dataset:
```
curl -XPOST 'localhost:9201/bank/account/_bulk?pretty' --data-binary @dataset/accounts.json
```
The sample dataset used has been found on [ElasticSearch site](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/_exploring_your_data.html)

## Stoping and starting nodes
You can now stop and start some nodes to see how the cluster reacts:
```
docker-compose stop e2
```

