# Kerberos Docker Container

This container setup a single instance of MIT Kerberos Server

## Getting started

Create a docker-compose.yml file like this one:
```
version: '3.6'

services:
    kerberos: 
        image: jairsjunior/kerberos-docker
        ports:
            - 88:88
        hostname: kerberos
        container_name: kerberos
        environment: 
            - REALM=KERBEROS.KERBEROS-DOCKER_DEFAULT
            - DOMAIN_REALM=kerberos.kerberos-docker_default
            - KERB_MASTER_KEY=masterkey
            - KERB_ADMIN_USER=admin
            - KERB_ADMIN_PASS=admin
            - SEARCH_DOMAINS=search.consul kerberos.kerberos-docker_default
        volumes: 
            - ./kerberos-data:/volumes/kerberos
            - ./kerberos-keytabs:/volumes/keytabs
            - ./kerberos-users:/volumes/users
```

## Automatic Create Users

At volume folder `kerberos-users` you can add a users.csv file that will create all the users
on that file if the keytab file aren't exists.

users.csv file example
```
kafka,broker.kafka-kerberos_default,kafka_broker
kafka,zookeeper.kafka-kerberos_default,kafka_client1
kafka,schema-registry.kafka-kerberos_default,kafka_schema-registry
kafka,rest-proxy.kafka-kerberos_default,kafka_rest-proxy
```

## Copyright

Based on [sequenceiq/docker-kerberos](https://github.com/sequenceiq/docker-kerberos) image