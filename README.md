# solrcloud
---
Dockerized Solrcloud development envionment for testing

## Setup
1. Git clone this repo
2. Git clone [yul-solr repo](https://github.com/yalelibrary/yul-solr.git)
3. cd is solrcloud directory
    ```bash
    cd solrcloud
    ```
4. Start solrcloud environment
    ```bash
    docker-compose up -d
    ```
5. Copy yul-solr configs to solr contianer
    ```bash
    docker-compose cp <path to solr configs> solr:/opt/
    
    # example: docker-compose cp ../yul-solr/quicksearch/solr/main/search solr:/opt/
    ```
6. Create solrcloud collection (core in standalone mode)
    ```bash
    docker-compose exec solr solr create -c quicksearch -d /opt/search -s2 -rf 2

    # -c quicksearch - collection name
    # -d /opt/search - path to solr config directory inside solr container
    # -s2            - create 2 shards
    # -rf 2          - create 2 shared replicas for backup 
    ```
7. Access solrcloud ui - get local solr port
    ```bash
    docker-compose ps solr

    # example output
    solrcloud-solr-1    "docker-entrypoint.s…"   solr                running             0.0.0.0:49153->8983/tcp, :::49153->8983/tcp
    solrcloud-solr-2    "docker-entrypoint.s…"   solr                running             0.0.0.0:49155->8983/tcp, :::49155->8983/tcp
    solrcloud-solr-3    "docker-entrypoint.s…"   solr                running             0.0.0.0:49154->8983/tcp, :::49154->8983/tcp
    ```
8. Open browser to one of the addresses and port number (ie. http://0.0.0.0:49153)

## Clean up
```bash
docker-compose down --volumes
```
