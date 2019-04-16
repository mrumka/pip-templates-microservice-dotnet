# Deployment Guide <br/> Settings Microservice

Tags microservice can be used in different deployment scenarios.

* [Standalone Process](#process)

## <a name="process"></a> Standalone Process

The simplest way to deploy the microservice is to run it as a standalone process. 
This microservice is implemented in .Net Core and requires installation of .Net Core Framework. 
You can get it from the official site at https://dotnet.microsoft.com/download

**Step 1.** Download microservices by following [instructions](Download.md)

**Step 2.** Add **config.json** file to the root of the microservice folder and set configuration parameters. 
See [Configuration Guide](Configuration.md) for details.

**Step 3.** Start the microservice using the commands:

Compile and run source code 
```bash
dotnet build ./pip-samples-beacons.sln
cd ./src
dotnet ./Process/bin/Debug/netcoreapp2.1/run.dll
```

## <a name="docker"></a> Docker Container

**Step 1.** Install [Docker Desctop](https://www.docker.com/)

**Step 2.** Install [PowerShell]. One of the ways is using brew package installer:

```bash
brew cask install powershell
```

**Step 3.**  Pull docker image, deploy project and compile source code
```bash
pwsh build.ps1
```

**Step 4.**  Run with in-memory persistent
```bash
pwsh run.ps1
```

To enable MongoDB support please declare environment varibales MONGO_ENABLED, MONGO_COLLECTION, MONGO_DB, MONGO_USER and MONGO_PASS variables:

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

To enable prometheus support please add or uncomment following line:

 Example **config.yml** file:
```
# Prometheus accounts service
- descriptor: "pip-services:metrics-service:prometheus:default:1.0"
```

You can use the microservice by calling seneca commands directly as described in [Seneca Protocol](SenecaProtocolV1.md)
or by using [SettingsSenecaClient](https://github.com/pip-services-infrastructure/pip-clients-settings-node/NodeClientApiV1.md/#client_seneca)