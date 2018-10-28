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

--------------------------------------------------------------------

## Elasticsearch

### Schema
voir le fichier schema

*Créer l'index movies*
```bash
curl -XPUT -H "Content-Type: application/json" localhost:9200/movies -d @schema.json
```

*Indexer les datas*
```bash
curl -XPUT -H "Content-Type: application/json" localhost:9200/_bulk --data-binary @bulk.json
```

