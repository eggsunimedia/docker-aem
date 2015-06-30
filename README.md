# Docker environment for AEM

## Prerequisites
The following files are required, but they're not part of this repository. Add them manually before you're able to build the Docker images.
- AEM/aem-quickstart-6.0.jar
- AEM/dispatcher-apache2.4-4.1.8.so
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
