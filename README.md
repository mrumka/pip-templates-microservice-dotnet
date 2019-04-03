# Pip Sample Beacons Application

A simple Pip Sample Beacons application that serves two purposes:
- It is used as the default app template when creating new projects
- It is a reference for building and publishing custom PIP Templates

This template has dependencies to the: 
* <a href="https://github.com/pip-services/pip-services-commons-dotnet">Pip Commons</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-components-dotnet">Pip Components</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-container-dotnet">Pip Container</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-data-dotnet">Pip Data</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-rpc-dotnet">Pip MongoDb</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-mongodb-dotnet">Pip Rpc</a>

The microservice currently supports the following deployment options:
* Deployment platforms: Standalone Process, Seneca
* External APIs: HTTP/REST, Seneca
* Persistence: Flat Files, MongoDB


<a name="links"></a> Quick Links:
* [Download Links](doc/Downloads.md)
* [Development Guide](doc/Development.md)
* [Configuration Guide](doc/Configuration.md)
* [Deployment Guide](doc/Deployment.md)
* Client SDKs
  - [Node.js SDK](https://github.com/pip-services-infrastructure/pip-clients-settings-dotnet)
* Communication Protocols
  - [HTTP Version 1](doc/HttpProtocolV1.md)
  - [Seneca Version 1](doc/SenecaProtocolV1.md)
  
  
 ## Contract

Logical contract of the microservice is presented below and define in Interface project. For physical implementation (HTTP/REST, Thrift, Seneca, Lambda, etc.),
please, refer to documentation of the specific protocol.

```dotnet
    public class BeaconV1 : IStringIdentifiable
    {
        public string Id { get; set; }
        public string SiteId { get; set; }
        public string Type { get; set; }
        public string Udi { get; set; }
        public string Label { get; set; }
        public CenterObjectV1 Center { get; set; }
        public double Radius { get; set; }
    }
    
    [DataContract]
    public class CenterObjectV1
    {
        public string Type { get; set; }
        public double[] Coordinates { get; set; }
    }
    
    public interface IBeaconsController
    {
        Task<DataPage<BeaconV1>> GetBeaconsAsync(string correlationId, FilterParams filter, PagingParams paging);
        Task<BeaconV1> GetBeaconByIdAsync(string correlationId, string id);
        Task<BeaconV1> GetBeaconByUdiAsync(string correlationId, string udi);
        Task<CenterObjectV1> CalculatePositionAsync(string correlationId, string siteId, string[] udis);
        Task<BeaconV1> CreateBeaconAsync(string correlationId, BeaconV1 beacon);
        Task<BeaconV1> UpdateBeaconAsync(string correlationId, BeaconV1 beacon);
        Task<BeaconV1> DeleteBeaconByIdAsync(string correlationId, string id);
    }
```

## Download

Right now the only way to get the microservice is to check it out directly from github repository
```bash
git clone git@github.com:pip-templates/pip-templates-microservice-dotnet.git
```

Pip.Service team is working to implement packaging and make stable releases available for your 
as zip downloadable archieves.

## Run

Add **config.yml** file to the root of the microservice folder and set configuration parameters.
As the starting point you can use example configuration from **config.example.yml** file. 

Example of microservice configuration
```yaml
# Console logger
- descriptor: "pip-services3-commons:logger:console:default:1.0"
  level: "trace"
  
# Performance counters that posts values to log
- descriptor: "pip-services3-commons:counters:log:default:1.0"
  level: "trace"

# # Elastic search logger vesion 1.0
# - descriptor: "pip-services:logger:elasticsearch:default:1.0"
#   connection:
#     uri: {{ELASTIC_SEARCH_SERVICE_URI}}{{^ELASTIC_SEARCH_SERVICE_URI}}http://localhost:9200{{/ELASTIC_SEARCH_SERVICE_URI}}

{{#if MONGO_ENABLED}}
# MongoDB Persistence
- descriptor: "beacons:persistence:mongodb:default:1.0"
  collection: {{MONGO_COLLECTION}}{{^MONGO_COLLECTION}}beacons{{/MONGO_COLLECTION}}
  connection:
    uri: {{MONGO_SERVICE_URI}}
    host: {{MONGO_SERVICE_HOST}}{{^MONGO_SERVICE_HOST}}localhost{{/MONGO_SERVICE_HOST}}
    port: {{MONGO_SERVICE_PORT}}{{^MONGO_SERVICE_PORT}}27017{{/MONGO_SERVICE_PORT}}
    database: {{MONGO_DB}}{{^MONGO_DB}}app{{/MONGO_DB}}
  credential:
    username: {{MONGO_USER}}
    password: {{MONGO_PASS}}
{{/if}}

{{^MOCK_ENABLED}}{{^MONGO_ENABLED}}
# Default in-memory persistence
- descriptor: "beacons:persistence:memory:default:1.0"
{{/MONGO_ENABLED}}{{/MOCK_ENABLED}}

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

# Prometheus accounts service
#- descriptor: "pip-services:metrics-service:prometheus:default:1.0"
```

For more information on the microservice configuration see [Configuration Guide](Configuration.md).

Start the microservice using the command:
```bash
node run
```

## Use

The easiest way to work with the microservice is to use client SDK. 
The complete list of available client SDKs for different languages is listed in the [Quick Links](#links)

* Change Microservice Contract and reflect changes dependent classes.


## Acknowledgements

This microservice was created and currently maintained by *Sergey Seroukhov*.
