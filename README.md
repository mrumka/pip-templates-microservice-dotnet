# Pip Sample Beacons Application

A simple Pip Sample Beacons Application that serves two purposes:
- It can be used as the template when creating new projects
- It is a reference for building and publishing custom microservices

The microservice contains list of beacons where each becaon have basic information and absolute location.

The microservice currently supports the following deployment options:
* Deployment platforms: Standalone Process, Docker
* External APIs: HTTP/REST
* Persistence: Memory, Flat Files, MongoDB
* Logging, Maintaining

<a name="links"></a> Quick Links:
* [Download Links](doc/Downloads.md)
* [Development Guide](doc/Development.md)
* [Configuration Guide](doc/Configuration.md)
* [Deployment Guide](doc/Deployment.md)
* Client SDKs
  - [.Net Core SDK](https://github.com/pip-services-infrastructure/pip-clients-settings-dotnet)
* Communication Protocols
  - [HTTP Version 1](doc/HttpProtocolV1.md)  
  
 ## Microservice Interface

Logical contract of the microservice is presented below and define in Interface project. For physical implementation (HTTP/REST, Lambda, etc.),
please, refer to documentation of the specific protocol.

```c#
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
    
    public class CenterObjectV1
    {
        public string Type { get; set; }
        public double[] Coordinates { get; set; }
    }
    
    public interface IBeaconsClientV1
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

## Run from Docker

**Step 1.** Install [Docker Desctop](https://www.docker.com/)

**Step 2.** Execute following command to download Docker image with predefined microservice and run
```bash
git docker run pip-templates-microservice-dotnet
```
More information about how to configure microservice and run in docker container can be found in [Deployment Guide](doc/Deployment.md)

## Run from source code

Prerequisite:
* Download and install [.Net Core SDK](https://dotnet.microsoft.com/download).
* Download and install [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/) or [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/).

**Step 1.** Check it out latest source code directly from github repository
```bash
git clone git@github.com:pip-templates/pip-templates-microservice-dotnet.git
```

**Step 2.** Compile source code 
```bash
dotnet build ./pip-samples-beacons.sln
```

**Step 3** Run compuled binaries
```bash
cd ./src
dotnet ./Process/bin/Debug/netcoreapp2.1/run.dll
```

## Use

Add beacons
```bash
curl --header "Content-Type: application/json" --request POST --data "{\"correlationId\":\"d42fd72c-02d2-4944-8631-4d94bc5fd75f\",\"beacon\":{\"id\":\"1\", \"site_id\":\"Site1\", \"type\":\"tracker\",\"udi\":\"12345\", \"label\":\"basic tracker\", \"radius\":4.0, \"center\": {\"type\": \"absolute\", \"coordinates\": [123.0,456.0,789.0]}}}" http://localhost:8080/v1/beacons/create_beacon

curl --header "Content-Type: application/json" --request POST --data "{\"correlationId\":\"d42fd72c-02d2-4944-8631-4d94bc5fd75f\",\"beacon\":{\"id\":\"2\", \"site_id\":\"Site2\", \"type\":\"tracker\",\"udi\":\"12345\", \"label\":\"basic tracker\", \"radius\":4.0, \"center\": {\"type\": \"absolute\", \"coordinates\": [123.0,456.0,789.0]}}}" http://localhost:8080/v1/beacons/create_beacon
```
Get all beacons
```bash
curl --header "Content-Type: application/json" --data "{\"correlationId\":\"d42fd72c-02d2-4944-8631-4d94bc5fd75f\",\"filter\":null,\"paging\":null}" --request POST localhost:8080/v1/beacons/get_beacons
```
Update beacon
```bash
curl --header "Content-Type: application/json" --request POST --data "{\"correlationId\":\"d42fd72c-02d2-4944-8631-4d94bc5fd75f\",\"beacon\":{\"id\":\"2\", \"site_id\":\"New Site2\", \"type\":\"tracker\",\"udi\":\"12345\", \"label\":\"basic tracker\", \"radius\":4.0, \"center\": {\"type\": \"absolute\", \"coordinates\": [123.0,456.0,789.0]}}}" http://localhost:8080/v1/beacons/update_beacon
```
Get beacon
```bash
curl --header "Content-Type: application/json" --data "{\"correlationId\":\"d42fd72c-02d2-4944-8631-4d94bc5fd75f\",\"beacon_id\":\"2\"}" --request POST localhost:8080/v1/beacons/get_beacon_by_id
```
Delete beacon
```bash
curl --header "Content-Type: application/json" --data "{\"correlationId\":\"d42fd72c-02d2-4944-8631-4d94bc5fd75f\",\"beacon_id\":\"2\"}" --request POST localhost:8080/v1/beacons/delete_beacon_by_id
```

## Acknowledgements

This microservice was created and currently maintained by *Sergey Seroukhov*, *Sergey Merkuriev*, *Egor Nuzhnykh*.
