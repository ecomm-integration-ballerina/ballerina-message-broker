# Base image
FROM openjdk:8-jre-alpine
MAINTAINER WSO2 Docker Maintainers "dev@wso2.org"

# User details
ARG USER=ballerina
ARG USER_GROUP=ballerina
ARG USER_HOME=/home/${USER}

# Resource directory
ARG FILES=./files

# Broker details
ARG BROKER_NAME=message-broker
ARG BROKER_VERSION=0.970.5
ARG BROKER_DISTRIBUTION=${BROKER_NAME}-${BROKER_VERSION}
ARG BROKER_HOME=${USER_HOME}/${BROKER_DISTRIBUTION}

# Add a user group and a user
RUN addgroup -S ${USER_GROUP} && adduser -S -G ${USER_GROUP} ${USER}

# Copy message broker distribution to user's home directory
COPY --chown=ballerina:ballerina ${FILES}/${BROKER_DISTRIBUTION} ${BROKER_HOME}

# set the user and work directory
USER ${USER}
WORKDIR ${USER_HOME}

# Set environment variable
ENV BROKER_HOME ${BROKER_HOME}

# Expose broker ports
EXPOSE 5672 8672 9000

# Execute broker startup script
CMD ["sh", "-c", "${BROKER_HOME}/bin/broker"]
