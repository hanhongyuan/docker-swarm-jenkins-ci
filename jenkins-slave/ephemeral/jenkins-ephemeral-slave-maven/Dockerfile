FROM jsdidierlaurent/jenkins-ephemeral-slave
LABEL maintainer "Jean-Sébastien Didierlaurent <js.didierlaurent@gmail.com>"

USER root
ARG MAVEN_VERSION=3.5.0
ARG SHA=beb91419245395bd69a4a6edad5ca3ec1a8b64e41457672dc687c173a495f034
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-$MAVEN_VERSION-bin.tar.gz \
  && echo "${SHA}  /tmp/apache-maven.tar.gz" | sha256sum -c - \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

RUN mkdir -p "$HOME/.m2" && \
  chown ${SLAVE_USERNAME} "$HOME/.m2"

USER ${SLAVE_USERNAME}
ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$HOME/.m2"

COPY settings-docker.xml /usr/share/maven/ref/

VOLUME "$HOME/.m2"