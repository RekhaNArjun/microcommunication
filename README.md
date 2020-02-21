![Screenshot of the Web Frontend](assets/Screenshot.png)

# Micro-service Intercommunication Demo

[![Docker](https://img.shields.io/badge/Docker%20Hub-microcommunication--api-blue.svg?logo=docker)](https://hub.docker.com/r/robinmanuelthiel/microcommunication-api/) [![Docker](https://img.shields.io/badge/Docker%20Hub-microcommunication--web-blue.svg?logo=docker)](https://hub.docker.com/r/robinmanuelthiel/microcommunication-web/)
![GitHub Actions status](https://github.com/robinmanuelthiel/microcommunication/workflows/.github/workflows/docker.yml/badge.svg) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=robinmanuelthiel_microcommunication&metric=alert_status)](https://sonarcloud.io/dashboard?id=robinmanuelthiel_microcommunication)

This is a small demo project to quickly setup a mix of containerized micro-services that communicate with each other within the network. This demo is intended to provide a playground for orchestrators!

The project consists of

- An API Backend, written in .NET Core, exposes port `8080`
- A Web Frontend, written in Angular, exposes port `80`

## Make it run

### Prerequisites

- [.NET Core 2 SDK](https://dotnet.microsoft.com/download)
- [Angular CLI](https://cli.angular.io/)
- [Docker](https://www.docker.com/products/docker-desktop)

The easiest way to run and debug the microservices on you development machine is [Visual Studio Code](https://code.visualstudio.com/). Just open the folder and select the _Launch Microservices_ Debug configuration.

![Screenshot of Visual Studio Code](assets/LaunchInVsCode.png)

## Environment variables

You need to set some environment variables to configure the services and their discovery.

`MicroCommunication.Api`:

- `ApiKey=test123` *Optional: The key, that the API allows for authorization*
- `MongoDbConnectionString=mongo://...` *Optional: The connection string for a Mongo DB to store the history in*
- `RedisCacheConnectionString=...` *Optional: The connection string for a Redis Cache to sync SignalR Hubs*
- `Cors` *Optional: The domain of your web app to add to the CORS*

`MicroCommunication.Web`:

- `API_URL=http://localhost:8080` *Where to find the API*
- `API_KEY=test123` *Which key to use when calling the API*

## Orchestrators

This Demo project is intended to be tested within container orchestrators. For the various different orchestrators out there, you can find configuration files for multiple different ones in the repository.

> **Windows Containers:** If you want to run on Windows, feel free to use the Windows versions of these containers instead by using the `*.windows.*` files, where available.

### Docker Compose

```bash
docker-compose -f env/docker-compose/docker-compose.yaml up
```

### Kubernetes

```bash
kubectl create -f env/kubernetes/microcommunication.yaml
```

### Service Fabric Mesh

```bash
az mesh deployment create --resource-group Demo --template-file env/servicefabric-mesh/servicefabric-mesh.json
```
