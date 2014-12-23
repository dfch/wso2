# Dockerfile to build WSO2 Complex Event Processor
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
# 	cd <path to Dockerfile>
# 	sudo docker build -t wso2cep310 .
# 
# Run a container using the built image
# 	sudo docker run -d -i -p 9443:9443 -t --name cep wso2cep310
#
# Login to the running container
# 	sudo docker attach CEP
#
# Exit from a attached container
# 	^p^q (Ctrl+p and Ctrl+q)
#

	
# Use Ubuntu base image
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

# Download and install WSO2 CEP 3.1.0
# RUN cd /src && wget -q --no-cookies http://dl.sharedop.net.s3.amazonaws.com/shared/wso2/wso2cep-3.1.0.zip
RUN cd /opt && unzip -q /src/wso2cep-3.1.0.zip -d /opt

# Set environment variables
# HOME is already set correctly in centos image
# ENV HOME /root

WORKDIR /root

CMD /opt/wso2cep-3.1.0/bin/wso2server.sh
