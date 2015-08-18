# Dockerized AEM 6.0 author image

FROM aem-base:latest

ENV CQ_RUNMODE author
ENV CQ_PORT 4502
ENV PUBLISH_HOST publish

RUN echo sling.run.modes=${CQ_RUNMODE} >> crx-quickstart/conf/sling.properties && \
    crx-quickstart/bin/start && \
    until $(curl -u admin:admin --output /dev/null --silent --head --fail http://localhost:$CQ_PORT); do printf '.'; sleep 5; done && \
    curl http://localhost:4502/etc/replication/agents.author/publish/jcr:content -F transportUri=http://${PUBLISH_HOST}:4503/bin/receive?sling:authRequestLogin=1 -uadmin:admin && \
    crx-quickstart/bin/stop

EXPOSE $CQ_PORT

CMD java -XX:MaxPermSize=256M -Xmx1024m -jar $AEM_QUICKSTART_FILE -p $CQ_PORT -r $CQ_RUNMODE
