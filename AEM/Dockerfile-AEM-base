# Dockerized AEM 6.0 base image

FROM ubuntu:14.04

ENV AEM_VERSION 6.0
ENV AEM_QUICKSTART_FILE aem-quickstart-6.0.jar
ENV AEM_USER aem
ENV AEM_WORKING_DIR /opt/aem
ENV DEBIAN_FRONTEND noninteractive
ENV JAVA_VERSION 7
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle

# Install updates and Java 7
RUN apt-get update && \
    apt-get install -y curl unzip software-properties-common && \
    add-apt-repository ppa:webupd8team/java && \
    apt-get update && \
    apt-get -y upgrade && \
    echo oracle-java${JAVA_VERSION}-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    apt-get -y install oracle-java7-installer && \
    apt-get clean && \
    apt-get purge && \
    update-alternatives --display java

# Cleanup installation
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/oracle-jdk7-installer

# Add quick-start file and license properties
ADD ./$AEM_QUICKSTART_FILE $AEM_WORKING_DIR/$AEM_QUICKSTART_FILE
ADD ./license.properties $AEM_WORKING_DIR/license.properties

# Create user and unpack AEM quick-start
RUN groupadd -r $AEM_USER && useradd -r -g $AEM_USER $AEM_USER -d $AEM_WORKING_DIR && \
    java -jar $AEM_WORKING_DIR/$AEM_QUICKSTART_FILE -unpack && \
    chown -R $AEM_USER:$AEM_USER $AEM_WORKING_DIR

USER $AEM_USER

WORKDIR $AEM_WORKING_DIR
