# Installation

## CKAN

[Original instruction](http://docs.ckan.org/en/latest/maintaining/installing/install-from-docker-compose.html)

1. Build docker image:

```
cd sys/containers/ckan
sh make
```

2. Start CKAN

```
cd sys/containers/ckan
docker-compose up
```

3. Setup users

```docker exec -it ckan /usr/local/bin/ckan-paster --plugin=ckan sysadmin -c /etc/ckan/production.ini add mint```

## GraphDB

1. Build graphdb

```
cd sys/containers/graphdb
sh make
```

## Karma

```
cd sys/containers/karma
sh make
```