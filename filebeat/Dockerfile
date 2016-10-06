FROM  java:8u102-jdk
MAINTAINER Pranav S Kurup

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y wget vim less ca-certificates sudo

ENV ONEWEB_HOME /opt/oneweb
RUN useradd -d ${ONEWEB_HOME} -m oneweb
RUN chsh -s /bin/bash oneweb
WORKDIR ${ONEWEB_HOME}

ENV FB_VERSION 4.5.0
ENV FB_PACKAGE_NAME filebeat-${FB_VERSION}-x86_64
ENV FB_PACKAGE_TYPE tar.gz
ENV FB_PACKAGE ${FB_PACKAGE_NAME}.${FB_PACKAGE_TYPE}
ENV FB_TMP ${ONEWEB_HOME}/${FB_PACKAGE_NAME}
ENV FB_HOME ${ONEWEB_HOME}/filebeat

RUN \
 wget https://download.elastic.co/beats/filebeat/${FB_PACKAGE} && \
 tar xvzf ${FB_PACKAGE} && \
 rm -f ${FB_PACKAGE}

RUN mv ${FB_TMP} ${FB_HOME}

COPY config ${FB_HOME}/config.d

RUN \
 chown -R oneweb:oneweb ${ONEWEB_HOME}


CMD ["/opt/oneweb/filebeat/filebeat", "-c", "/opt/oneweb/filebeat/config.d/filebeat.yml", "-v"]