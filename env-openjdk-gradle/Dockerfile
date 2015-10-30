# The image source
FROM ubuntu:trusty
# Tell everyone who is maintaining this tragedy
MAINTAINER Andy Chan <andy@channie.co.uk>
# Set some environment variables
ENV JAVA_VERSION 8
ENV GRADLE_VERSION 2.8
# Ubuntu trusty fix to install add-apt-repository
# Get and install some stuff
RUN apt-get -y install software-properties-common && \
    add-apt-repository -y ppa:openjdk-r/ppa && \
    apt-get update && \
    apt-get -y install \
      openjdk-${JAVA_VERSION}-jdk \
      unzip \
      wget && \
    wget https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip -oq gradle-${GRADLE_VERSION}-bin.zip -d /usr/lib/ && \
    rm gradle-${GRADLE_VERSION}-bin.zip && \
    ln -s "/usr/lib/gradle-${GRADLE_VERSION}/bin/gradle" /usr/bin/gradle && \
    rm -rf /var/lib/apt/lists/*
