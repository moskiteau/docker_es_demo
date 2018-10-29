# docker_es_demo
Présentation technique de docker compose, elasticsearch, head, etc.

## Requirements

Adjuster vm mmax_map_count
```bash
# sysctl -w vm.max_map_count=262144
```

*Installer docker compose*
```bash
sudo apt-get install docker-compose
```

*Installer curl*
```bash
sudo apt-get install curl
```

*partir l'image docker*
* [head plugin](http://localhost:9100)

--------------------------------------------------------------------

## Elasticsearch

### Créer un index vide et indexer un documents
```bash
curl -XPUT -H "Content-Type: application/json" localhost:9200/movies_test
curl -XPUT -H "Content-Type: application/json" localhost:9200/movies_test/_doc/1 --data-binary @test_movie.json
curl -XGET -H "Content-Type: application/json" localhost:9200/movies_test/_doc/1
```

### Schema
voir le fichier schema

*Créer l'index movies*
```bash
curl -XPUT -H "Content-Type: application/json" localhost:9200/movies -d @schema.json
```

*Indexer les films*
```bash
curl -XPUT -H "Content-Type: application/json" localhost:9200/_bulk --data-binary @bulk.json
```

*Effacer tout*
```bash
curl -XDELETE -H "Content-Type: application/json" localhost:9200/movies_test
```

### Chercher

#### Par url et un query_string
* [Star wars](http://localhost:9200/movies/_search?q=star%20wars&pretty)
* [Star wars sur le titre](http://localhost:9200/movies/_search?q=title:star%20wars&pretty)
* [Star wars sur le titre et le directeur est Lucas](http://localhost:9200/movies/_search?q=title:star%20wars%20AND%20director:Lucas&pretty)


#### Recherche plus complexe
*star wars et lucas*
```bash
curl -XPOST -H "Content-Type: application/json" localhost:9200/movies/_search?pretty -d @search/search/01_bool_should.json
```

Voir les autres ficheirs json pour plus de requêtes...

### Agreggations
```bash
curl -XPOST -H "Content-Type: application/json" localhost:9200/movies/_search?pretty -d @search/aggregations/01_metric_years.json
```
