# Docker environment for AEM

## Build AEM Images
```
echo "Build AEM base image"
docker build --rm --force-rm -t aem-base -f Dockerfile-AEM-base ./
echo "Build AEM author image"
docker build --rm --force-rm -t aem-author -f Dockerfile-AEM-author ./
echo "Build AEM author image"
docker build --rm --force-rm -t aem-publish -f Dockerfile-AEM-publish ./
```
