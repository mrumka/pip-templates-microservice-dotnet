This template has dependencies to the: 
* <a href="https://github.com/pip-services/pip-services-commons-dotnet">Pip Commons</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-components-dotnet">Pip Components</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-container-dotnet">Pip Container</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-data-dotnet">Pip Data</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-rpc-dotnet">Pip MongoDb</a>
* <a href="http://github.com/pip-services3-dotnet/pip-services3-mongodb-dotnet">Pip Rpc</a>


Check it latest source code directly from github repository
```bash
git clone git@github.com:pip-templates/pip-templates-microservice-dotnet.git
```

Install
```bash
git clone git@github.com:pip-templates/pip-templates-microservice-dotnet.git
```

# Development and Testing Guide <br/> Settings Microservice

This document provides high-level instructions on how to build and test the microservice.

* [Environment Setup](#setup)
* [Installing](#install)
* [Building](#build)
* [Testing](#test)
* [Contributing](#contrib) 


Add config.yml file to the root of the microservice folder and set configuration parameters. As the starting point you can use example configuration from config.example.yml file.


## <a name="setup"></a> Environment Setup

This is a .Net Core Framework project and you have to install .Net Core SDK.
You can download them from official .Net Core SDK website: https://dotnet.microsoft.com/download

After node is installed you can use Visual Studio or keep use command line.
You can download Visual Studio Community edition from official website: https://visualstudio.microsoft.com/vs/community/ or Visual Studio for Mac from https://visualstudio.microsoft.com/vs/mac/ 

After .Net Core Framework is installed you can check it by running the following command:
```bash
dotnet --version
```

To work with GitHub code repository you need to install Git from: https://git-scm.com/downloads

If you are planning to develop and test using persistent storages other than flat memoru or files
you may need to install database servers:
- Download and install MongoDB database from https://www.mongodb.org/downloads

## <a name="install"></a> Installing

After your environment is ready you can check out microservice source code from the Github repository:
```bash
git clone git@github.com:pip-templates/pip-templates-microservice-dotnet.git
```

If you worked with the microservice before you can check out latest changes and update the dependencies:
```bash
# Update source code updates from github
git pull
```

## <a name="build"></a> Building from Command Line

Check all configuration options. Specifically, pay attention to connection options
for database and dependent microservices. For more information check [Configuration Guide](Configuration.md) 

**Step 1.** Compile source code
This microservice is written in C# language.
So, if you make changes to the source code you need to compile it before running or committing to github.
The process will output compiled files into /bin folder of each project in the solution.

```bash
dotnet build ./pip-samples-beacons.sln
```
**Step 2.** Run compiled binaries
After successful compulation all running binaries located in the Process/bin folder. 
Use ./src as a working directory or copy **config.yml** to apropriate directory. 

```bash
cd ./src
dotnet ./Process/bin/Debug/netcoreapp2.1/run.dll
```

## <a name="build"></a> Building from Vusua Studio

**Step 1.** Open pip-samples-beacons.sln in the Visual Studio.

**Step 2.** Check that Process project selected as default project

**Step 3.** Click Run -> Run With -> Custom Configuration and set the Run in the directory with using full path to the solution src directory.

or

**Step 3.** Copy microservice **config.yml** file from ./config/config.yml to the ./src/config/config.yml folder and set configuration parameters if needed.

**Step 4.** Click Run -> Start Without Debigging menu

## <a name="test"></a> Testing from Command Line

Command to run unit tests:
```bash
dotnet test ./test/Client.Test/Client.Test.csproj
dotnet test ./test/Service.Test/Service.Test.csproj
```

## <a name="test"></a> Testing with Visual Studio

Open pip-samples-beacons.sln in the Visual Studio.

Choose Run Project from popup/context menu by click on Client.Test or Service.Test project

## <a name="contrib"></a> Contributing

Developers interested in contributing should read the following instructions:

- [How to Contribute](http://www.pipservices.org/contribute/)
- [Guidelines](http://www.pipservices.org/contribute/guidelines)
- [Styleguide](http://www.pipservices.org/contribute/styleguide)
- [ChangeLog](CHANGELOG.md)

> Please do **not** ask general questions in an issue. Issues are only to report bugs, request
  enhancements, or request new features. For general questions and discussions, use the
  [Contributors Forum](http://www.pipservices.org/forums/forum/contributors/).

It is important to note that for each release, the [ChangeLog](CHANGELOG.md) is a resource that will
itemize all:

- Bug Fixes
- New Features
- Breaking Changes