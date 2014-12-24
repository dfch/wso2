# Dockerfile to build WSO2 Message Broker
#
# Copyright 2014 Ronald Rink, d-fens GmbH
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Build the container
#       cd <path to Dockerfile>
#       sudo docker build -t wso2mb-2.2.0 .
#
# Run a container using the built image
#       sudo docker run -d -i -p 9443:9443 -t --name mb wso2mb-2.2.0
#
# Login to the running container
#       sudo docker attach mb
#
# Exit from a attached container
#       ^p^q (Ctrl+p and Ctrl+q)
#


# Use CentOS base image
FROM centos

# Maintainer
MAINTAINER Ronald Rink <ronald.rink@d-fens.net>

# Update system
RUN yum update -y
RUN yum install -y wget
RUN yum install -y unzip
RUN yum install -y tar

## Download and install Oracle JAVA JRE 1.7
RUN cd /opt && wget -q --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/7/jre-7-linux-x64.tar.gz
RUN cd /opt && tar -zxvf /opt/jre-7-linux-x64.tar.gz
RUN rm /opt/jre-7-linux-x64.tar.gz
RUN ln -s /opt/jre1.7.0 /opt/java
ENV JAVA_HOME /opt/java
ENV PATH ${PATH}:${JAVA_HOME}/bin

# Install WSO2 MB 2.2.0 (manually download it in advance and place it into a 'src' subdirectory below the 'Dockerfile')
COPY src/wso2mb-2.2.0.zip /opt/src/wso2mb-2.2.0.zip
RUN unzip -q /opt/src/wso2mb-2.2.0.zip -d /opt
RUN rm /opt/src/wso2mb-2.2.0.zip

# Set environment variables
# HOME is already set correctly in centos image
# ENV HOME /root

# Management Ports
EXPOSE 9443
#EXPOSE 9763
# AMQP
EXPOSE 5672
EXPOSE 8672
# JMX
#EXPOSE 11111

WORKDIR /root

CMD /opt/wso2mb-2.2.0/bin/wso2server.sh