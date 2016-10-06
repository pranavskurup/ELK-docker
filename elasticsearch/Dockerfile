FROM  java:8u102-jdk
MAINTAINER Pranav S Kurup

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y wget vim less ca-certificates sudo

ENV ONEWEB_HOME /opt/oneweb
RUN useradd -d ${ONEWEB_HOME} -m oneweb
RUN chsh -s /bin/bash oneweb
WORKDIR ${ONEWEB_HOME}

ENV ES_VERSION 2.4.1
ENV ES_PACKAGE_NAME elasticsearch-${ES_VERSION}
ENV ES_PACKAGE_TYPE tar.gz
ENV ES_PACKAGE ${ES_PACKAGE_NAME}.${ES_PACKAGE_TYPE}
ENV ES_TMP ${ONEWEB_HOME}/${ES_PACKAGE_NAME}
ENV ES_HOME ${ONEWEB_HOME}/elasticsearch
ENV ES_LOG_DIR ${ES_HOME}/log
ENV ES_DATA_DIR ${ES_HOME}/data

RUN \
 wget https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/${ES_VERSION}/${ES_PACKAGE} && \
 tar xvzf ${ES_PACKAGE} && \
 rm -f ${ES_PACKAGE}

RUN mv ${ES_TMP} ${ES_HOME}

# Export HTTP & Transport
EXPOSE 9200 9300
