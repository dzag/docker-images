FROM openjdk:11-jre-slim-buster

# Install GPG for package vefification
RUN apt-get update \
	&& apt-get -y install gnupg wget

# Add the liquibase user and step in the directory
RUN addgroup --gid 1001 liquibase
RUN adduser --disabled-password --uid 1001 --ingroup liquibase liquibase

# Make /liquibase directory and change owner to liquibase
RUN mkdir /liquibase && chown liquibase /liquibase
WORKDIR /liquibase

# Change to the liquibase user
USER liquibase

# Download, verify, extract
ARG LIQUIBASE_VERSION=4.1.1
ARG LB_SHA256=ef8e0b8f7f0cabc34a61b8a1e7f4feac46652b6f5e62b58a9f2d2cfc98f0033f
RUN set -x \
  && wget -O liquibase-${LIQUIBASE_VERSION}.tar.gz "https://github.com/liquibase/liquibase/releases/download/v${LIQUIBASE_VERSION}/liquibase-${LIQUIBASE_VERSION}.tar.gz" \
  && echo "$LB_SHA256  liquibase-${LIQUIBASE_VERSION}.tar.gz" | sha256sum -c - \
  && tar -xzf liquibase-${LIQUIBASE_VERSION}.tar.gz

# Setup GPG
RUN GNUPGHOME="$(mktemp -d)"

ARG MYSQL_CONNECTOR_VERSION=8.0.22
ARG MYSQL_SHA256=5019defbd12316295e97a6e88f2a9b07f118345a4e982710bba232e499b22f4f
RUN wget -O /liquibase/lib/mysql.jar "https://repo1.maven.org/maven2/mysql/mysql-connector-java/${MYSQL_CONNECTOR_VERSION}/mysql-connector-java-${MYSQL_CONNECTOR_VERSION}.jar" \
	&& echo "$MYSQL_SHA256  /liquibase/lib/mysql.jar" | sha256sum -c -

ENTRYPOINT ["/liquibase/liquibase"]
