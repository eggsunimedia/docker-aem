# Dockerized AEM 6.0 author image

FROM aem-base:latest

ENV CQ_RUNMODE publish
ENV CQ_PORT 4503

RUN echo sling.run.modes=${CQ_RUNMODE} >> crx-quickstart/conf/sling.properties && \
    crx-quickstart/bin/start && \
    until $(curl -u admin:admin --output /dev/null --silent --head --fail http://localhost:$CQ_PORT); do printf '.'; sleep 5; done && \
    crx-quickstart/bin/stop

EXPOSE $CQ_PORT

CMD java -XX:MaxPermSize=256M -Xmx1024m -jar $AEM_QUICKSTART_FILE -p $CQ_PORT -r $CQ_RUNMODE -verbose -nofork
