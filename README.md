# Docker environment for AEM

## Abstract
In normal project work everybody will have heard the sentence: „On my local machine it worked“! The circumstances which lead to this statement are that there are usually minor inconsistencies within the setup of the different environments. Different operating systems, Java versions or installed hot fixes influent the behavior of the developed application and cause issues. This is where Docker comes in place. Docker automates the deployment of applications and isolates them inside software containers, by providing an additional layer of abstraction and automation but with out the overhead caused by a virtual machine. Ones set up, it limits the installation process to 5 minutes independent which environment. Furthermore, the same application can be reused to run on local machines, data centers or in the cloud. We will show you how we incorporated Docker in our continuous deployment process and how we facilitate it for our development and deployment chain.

Presentation: http://eggs.de/connect2015

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

## Known Issues
- The default replication agent isn't configured correctly. The hostname _localhost_ has to be replaced by _publish_.

## Access AEM Environment
When you want to access you environment on Windows or MAC, you have to resolve the IP of your Boot2Docker VM first:
```boot2docker ip```

Through this IP you can access the AEM author and publish as well as the Apache dispatcher through the known standard ports.
