FROM  java:8u102-jdk
MAINTAINER Pranav S Kurup

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y wget vim less ca-certificates sudo

ENV ONEWEB_HOME /opt/oneweb
RUN useradd -d ${ONEWEB_HOME} -m oneweb
RUN chsh -s /bin/bash oneweb
WORKDIR ${ONEWEB_HOME}


ENV OW_SDK_VERSION 8.0.37
ENV OW_SDK_MIN 8
ENV OW_SDK_PACKAGE_NAME apache-tomcat-${OW_SDK_VERSION}
ENV OW_SDK_PACKAGE_TYPE tar.gz
ENV OW_SDK_PACKAGE ${OW_SDK_PACKAGE_NAME}.${OW_SDK_PACKAGE_TYPE}
ENV OW_SDK_TMP ${ONEWEB_HOME}/${OW_SDK_PACKAGE_NAME}
ENV OW_SDK_HOME ${ONEWEB_HOME}/oneweb-sdk


RUN \
 wget http://apache.rediris.es/tomcat/tomcat-${OW_SDK_MIN}/v${TOMCAT_VERSION}/bin/${OW_SDK_PACKAGE} && \
 tar xvzf ${OW_SDK_PACKAGE} && \
 rm -f ${OW_SDK_PACKAGE}

RUN mv ${OW_SDK_TMP} ${OW_SDK_HOME}

EXPOSE 8080
EXPOSE 8009

CMD ["/opt/oneweb/oneweb-sdk/bin/catalina.sh", "run"]
