[<< На главную](../README.md)

# Разное - как поднять opensearch+dashboard под виндой и не только

1. ставим [docker desktop](https://www.docker.com/products/docker-desktop/)
2. настраиваем `docker-compose.yml`
```yaml
version: '3'

services:
  opensearch-node1:
    image: opensearchproject/opensearch:latest #https://hub.docker.com/r/opensearchproject/opensearch
    container_name: opensearch-node1
    environment:
      - cluster.name=opensearch-cluster #dashboards завелся только с кластерным вариантом
      - node.name=opensearch-node1
      - discovery.seed_hosts=opensearch-node1
      - cluster.initial_master_nodes=opensearch-node1
      - bootstrap.memory_lock=true # along with the memlock settings below, disables swapping
    #  - "OPENSEARCH_JAVA_OPTS=-Xms512m -Xmx512m" # minimum and maximum Java heap size, recommend setting both to 50% of system RAM
    #- "DISABLE_SECURITY_PLUGIN=true" # Disables Security plugin
    ulimits:
      memlock:
        soft: -1
        hard: -1
      nofile:
        soft: 65536 # maximum number of open files for the OpenSearch user, set to at least 65536 on modern systems
        hard: 65536
    volumes:
      - opensearch-data1:/usr/share/opensearch/data
    ports:
      - 9200:9200
      - 9600:9600 # required for Performance Analyzer
    networks:
      - opensearch-net
  opensearch-dashboards:
    image: opensearchproject/opensearch-dashboards:latest #https://hub.docker.com/r/opensearchproject/opensearch-dashboards
    container_name: opensearch-dashboards
    ports:
      - 5601:5601
    expose:
      - "5601"
    environment:
      OPENSEARCH_HOSTS: https://opensearch-node1:9200
      #DISABLE_SECURITY_PLUGIN: true
    networks:
      - opensearch-net

volumes:
  opensearch-data1:

networks:
  opensearch-net:
```
3. команды:
- запуск `docker-compose up` или `docker-compose up -d`
- остановка `docker-compose stop`
- пересборка `docker-compose down` и `docker-compose up -d`
4. проверить работу opensearch 
- `curl -X GET "https://localhost:9200" -ku admin:admin` или открыть [https://localhost:9200/](https://localhost:9200/)
- `curl -X GET "https://localhost:9200/_cat/nodes?v" -ku admin:admin` или открыть [https://localhost:9200/_cat/nodes?v](https://localhost:9200/_cat/nodes?v)
- `curl -X GET "https://localhost:9200/_cat/plugins?v" -ku admin:admin` или открыть [https://localhost:9200/_cat/plugins?v](https://localhost:9200/_cat/plugins?v)
5. dashboard тут [http://localhost:5601/](http://localhost:5601/)
