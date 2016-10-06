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
ENV ES_PLUGIN_DIR ${ES_HOME}/plugin
ENV ES_WRK_DIR ${ES_HOME}/work

RUN \
 wget https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/${ES_VERSION}/${ES_PACKAGE} && \
 tar xvzf ${ES_PACKAGE} && \
 rm -f ${ES_PACKAGE}

RUN mv ${ES_TMP} ${ES_HOME}

COPY config ${ES_HOME}/config

RUN \
 chown -R oneweb:oneweb /opt/oneweb/

#  Set environment variables defaults
ENV ES_HEAP_SIZE 256m
ENV CLUSTER_NAME elasticsearch-oneweb
ENV NODE_MASTER true
ENV NODE_DATA true
ENV HTTP_ENABLE true
ENV NETWORK_HOST _site_
ENV HTTP_CORS_ENABLE true
ENV HTTP_CORS_ALLOW_ORIGIN *
ENV NUMBER_OF_MASTERS 1
ENV NUMBER_OF_SHARDS 1
ENV NUMBER_OF_REPLICAS 0

# Export HTTP & Transport
EXPOSE 9200 9300

CMD ["${ES_HOME}/bin/elasticsearch"]
