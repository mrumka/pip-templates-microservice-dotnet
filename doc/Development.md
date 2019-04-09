# Development and Testing Guide <br/> Beacons Microservice

This document provides high-level instructions on how to build and test the microservice.

* [Environment Setup](#setup)
* [Installing](#install)
* [Building](#build)
* [Testing](#test)
* [Contributing](#contrib) 

## <a name="setup"></a> Environment Setup

This is a .NET Core project and you have to install .NET Core SDK tools. 
You can download them from official website: https://dotnet.microsoft.com/download 

After node is installed you can check it by running the following command:
```bash
dotnet --version
```

To work with GitHub code repository you need to install Git from: https://git-scm.com/downloads

If you are planning to develop and test using persistent storages other than flat files
you may need to install database servers:
- Download and install MongoDB database from https://www.mongodb.org/downloads

## <a name="install"></a> Installing

After your environment is ready you can check out microservice source code from the Github repository:
```bash
git clone https://github.com/pip-templates/pip-templates-microservice-dotnet.git
```

Then go to the project folder and install dependent modules:

```bash
# Install dependencies
dotnet restore
```

If you worked with the microservice before you can check out latest changes and update the dependencies:
```bash
# Update source code updates from github
git pull
```

## <a name="build"></a> Building

This microservice is written in C# language, so, if you make changes to the source code you need to compile 
it before running or committing to github. The process will output compiled library files into /obj folder.

```bash
dotnet build
```

## <a name="test"></a> Testing

Command to run unit tests:
```bash
dotnet test
```

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