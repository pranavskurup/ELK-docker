FROM  java:8u102-jdk
MAINTAINER Pranav S Kurup

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y wget vim less ca-certificates sudo

ENV ONEWEB_HOME /opt/oneweb
RUN useradd -d ${ONEWEB_HOME} -m oneweb
RUN chsh -s /bin/bash oneweb
WORKDIR ${ONEWEB_HOME}

ENV LS_VERSION 2.4.0
ENV LS_PACKAGE_NAME logstash-${LS_VERSION}
ENV LS_PACKAGE_TYPE tar.gz
ENV LS_PACKAGE ${LS_PACKAGE_NAME}.${LS_PACKAGE_TYPE}
ENV LS_TMP ${ONEWEB_HOME}/${LS_PACKAGE_NAME}
ENV LS_HOME ${ONEWEB_HOME}/logstash

RUN \
 wget https://download.elasticsearch.org/logstash/logstash/${LS_PACKAGE} && \
 tar xvzf ${LS_PACKAGE} && \
 rm -f ${LS_PACKAGE}

RUN mv ${LS_TMP} ${LS_HOME}
COPY config ${LS_HOME}/config.d
# # add templates
# COPY ./templates/ ${LS_HOME}/templates/
RUN \
 chown -R oneweb:oneweb ${ONEWEB_HOME}

 CMD ["/opt/oneweb/logstash/bin/logstash", "-f", "/opt/oneweb/logstash/config.d/logstash.conf" , "-l" , "/opt/oneweb/logstash/logs/logstash.log"]