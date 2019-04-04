# Configuration Guide <br/> Sample Beacons Application

Configuration structure used by this module follows the 
[standard configuration](https://github.com/pip-services/pip-services/blob/master/usage/Configuration.md) 
structure.

Configuration of Microservice depends on PIP Services and an additional information about how to configure them can be found below:
* <a href="https://github.com/pip-services/pip-services-commons-dotnet/doc/DConfiguration.ms">Pip Commons</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-components-dotnet/doc/DConfiguration.ms">Pip Components</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-container-dotnet/doc/DConfiguration.ms">Pip Container</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-data-dotnet/doc/DConfiguration.ms">Pip Data</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-rpc-dotnet/doc/DConfiguration.ms">Pip MongoDb</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-mongodb-dotnet/doc/DConfiguration.ms">Pip Rpc</a>

All used PIP Services and their configuration should be declared config.yml file.
Example **config.yml** file:
```
# Console logger
- descriptor: "pip-services3-commons:logger:console:default:1.0"
  level: "trace"

# Performance counters that posts values to log
- descriptor: "pip-services3-commons:counters:log:default:1.0"
  level: "trace"

# Default in-memory persistence
- descriptor: "beacons:persistence:memory:default:1.0"

# Default controller
- descriptor: "beacons:controller:default:default:1.0"

# Common HTTP endpoint
- descriptor: "pip-services3:endpoint:http:default:1.0"
  connection:
    protocol: "http"
    host: "0.0.0.0"
    port: {{{HTTP_PORT}}}{{^HTTP_PORT}}8080{{/HTTP_PORT}}

# HTTP service version 1.0
- descriptor: "beacons:service:http:default:1.0"

# Heartbeat service
- descriptor: "pip-services3:heartbeat-service:http:default:1.0"
  route: heartbeat

# Status service
- descriptor: "pip-services3:status-service:http:default:1.0"
  route: status
```

To enable mongodb support please declare environment varibales MONGO_ENABLED, MONGO_COLLECTION, MONGO_DB, MONGO_USER and MONGO_PASS variables:

```bash
export MONGO_ENABLED=True
export MONGO_COLLECTION=BeaconsCollection
export MONGO_DB=BeaconsDB
export MONGO_USER=SomeUser
export MONGO_PASS=SomeUserPassword
```

To enable elastic search please add or uncomment following line and declare ELASTIC_SEARCH_SERVICE_URI environment variable:

```bash
export ELASTIC_SEARCH_SERVICE_URI=https://CLUSTER_ID.REGION.PLATFORM.found.io:9243
```

Example **config.yml** file:
```
# Elastic search logger vesion 1.0
 - descriptor: "pip-services:logger:elasticsearch:default:1.0"
   connection:
     uri: {{ELASTIC_SEARCH_SERVICE_URI}}{{^ELASTIC_SEARCH_SERVICE_URI}}http://localhost:9200{{/ELASTIC_SEARCH_SERVICE_URI}}

```

To enable prometheus support please add or uncomment following line:

Example **config.yml** file:
```
# Prometheus accounts service
- descriptor: "pip-services:metrics-service:prometheus:default:1.0"
```

