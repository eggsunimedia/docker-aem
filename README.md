# Docker environment for AEM

## Required Applications
- [Docker](https://docs.docker.com/) or [Boot2Docker](https://github.com/boot2docker/boot2docker)
- [Docker Compose](https://docs.docker.com/compose/)

## Build Prerequisites
The following files are required, but they're not part of this repository. Add them manually before you're able to build the Docker images.
- AEM/aem-quickstart-6.0.jar
- AEM/license.properties
- Dispatcher/dispatcher-apache2.4-4.1.8.so

## Build AEM Images
Execute within the _AEM_ folder:
```
echo "Build AEM base image"
docker build --rm --force-rm -t aem-base -f Dockerfile-AEM-base ./
echo "Build AEM author image"
docker build --rm --force-rm -t aem-author -f Dockerfile-AEM-author ./
echo "Build AEM author image"
docker build --rm --force-rm -t aem-publish -f Dockerfile-AEM-publish ./
```

Execute within the _Dispatcher_ folder:
```
docker build --rm --force-rm -t apache-dispatcher -f Dockerfile ./
```

## Start environment
Execute within the project root folder
```
docker-compose up
```

## Access AEM Environment
When you want to access you environment on Windows or MAC, you have to resolve the IP of your Boot2Docker VM first:
```boot2docker ip```

Through this IP you can access the AEM author and publish as well as the Apache dispatcher through the known standard ports.
