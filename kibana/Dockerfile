FROM  java:8u102-jdk
MAINTAINER Pranav S Kurup

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y wget vim less ca-certificates sudo

ENV ONEWEB_HOME /opt/oneweb
RUN useradd -d ${ONEWEB_HOME} -m oneweb
RUN chsh -s /bin/bash oneweb
WORKDIR ${ONEWEB_HOME}

ENV KB_VERSION 4.5.0
ENV KB_PACKAGE_NAME kibana-${KB_VERSION}-linux-x64
ENV KB_PACKAGE_TYPE tar.gz
ENV KB_PACKAGE ${KB_PACKAGE_NAME}.${KB_PACKAGE_TYPE}
ENV KB_TMP ${ONEWEB_HOME}/${KB_PACKAGE_NAME}
ENV KB_HOME ${ONEWEB_HOME}/kibana

RUN \
 wget https://download.elastic.co/kibana/kibana/${KB_PACKAGE} && \
 tar xvzf ${KB_PACKAGE} && \
 rm -f ${KB_PACKAGE}

RUN mv ${KB_TMP} ${KB_HOME}

COPY config ${KB_HOME}/config

RUN \
 chown -R oneweb:oneweb ${ONEWEB_HOME}

RUN ${KB_HOME}/bin/kibana plugin --install elastic/sense


EXPOSE 5601

CMD ["/opt/oneweb/kibana/bin/kibana"]