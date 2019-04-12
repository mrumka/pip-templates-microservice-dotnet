# Configuration Guide <br/> Sample Beacons Application

Configuration structure used by this module follows the 
[standard configuration](https://github.com/pip-services/pip-services/blob/master/usage/Configuration.md) 
structure.

Configuration of Microservice depends on PIP Services and an additional information about how to configure them can be found below:
* <a href="https://github.com/pip-services/pip-services-commons-dotnet/doc/Configuration.ms">Pip Commons</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-components-dotnet/master/doc/Configuration.ms">Pip Components</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-container-dotnet/master/doc/Configuration.ms">Pip Container</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-data-dotnet/master/doc/Configuration.ms">Pip Data</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-mongodb-dotnet/master/doc/Configuration.ms">Pip MongoDb</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-rpc-dotnet/master/doc/Configuration.ms">Pip Rpc</a>

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
    port: 8080

# HTTP service version 1.0
- descriptor: "beacons:service:http:default:1.0"

# Heartbeat service
- descriptor: "pip-services3:heartbeat-service:http:default:1.0"
  route: heartbeat

# Status service
- descriptor: "pip-services3:status-service:http:default:1.0"
  route: status
```
Where 
* protocol - .Net Framework supports only http
* host - the IP Address or DNS name of the system in the Network
* port - the IP Port of the service within the System


To enable mongodb support in-memory persistence should be disabled and should be declared following configuration:

```bash
# MongoDB Persistence
- descriptor: "beacons:persistence:mongodb:default:1.0"
  collection: beacons
  connection:
    uri: {{MONGO_SERVICE_URI}}
    host: localhost
    port: 27017
    database: app
  credential:
    username: SomeUser
    password: SomeUserPassword
```

Where
* collection - Mongo DB collection name
* uri - ...
* host - the IP Address or DNS name of the MongoDB server in the Network
* port - the IP Port MongoDB server on the target System
* database - the MongoDB database name
* username - the user name uses to access the database
* password - the password uses to access the database

To enable elastic search should be added or uncommented following lconfiguration:

Example **config.yml** file:
```
# Elastic search logger vesion 1.0
 - descriptor: "pip-services:logger:elasticsearch:default:1.0"
   connection:
     uri: http://localhost:9200

```

Where uri is Elactic Search connection string


To enable prometheus support should be added or uncommented following line:

Example **config.yml** file:
```
# Prometheus accounts service
- descriptor: "pip-services:metrics-service:prometheus:default:1.0"
```

