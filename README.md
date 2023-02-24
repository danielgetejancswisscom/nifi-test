# docker-compose
Fully persistent Env. for Nifi, NifiRegistry and Redis.

## Persisting Nifi:
Background: Nifi stores information in the `conf` directory which is not mounted on startup. Therefore this one-time steps are needed: 

1. execute docker-compose
2. copy `conf` directory from container to local machine  
   `> docker cp {Container ID}:/opt/nifi/nifi-current/conf ./nifi/`
3. Stop containers
4. Uncomment line in docker-compose
5. Start containers again with `docker-compose up --force-recreate`

More information here if needed:
https://medium.com/geekculture/host-a-fully-persisted-apache-nifi-service-with-docker-ffaa6a5f54a3

## Connection Nifi -> Nifi-Registry

in Nifi Controller Settings, Registry Clients, +
Properties: 
   url: http://nifi-registry:18080

## Versioning Flows Nifi-Registry & Git
same procedure as in Persisting Nifi

1. execute docker-compose
2. copy `conf` directory from container to local machine  
   `> docker cp {Container ID}:/opt/nifi-registry/nifi-registry-current/conf ./nifi_registry`
3. Stop containers
4. Uncomment line in docker-compose -> nifi registry!
5. Start containers again with `docker-compose up --force-recreate`

Now the direct