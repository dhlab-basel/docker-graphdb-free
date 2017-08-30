FROM ubuntu:17.04

MAINTAINER Ivan Subotic "ivan.subotic@unibas.ch"

# Silence debconf messages
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get -qq update && apt-get -y install \
  byobu curl git htop man vim wget unzip \
  openjdk-8-jdk && \
  rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"

# Install GraphDB-Free
RUN curl -sS -o /tmp/graphdb.zip -L http://go.pardot.com/e/45622/7a-graphdb-free-8-2-0-dist-zip/4rzsm6/1106070369 && \
    unzip /tmp/graphdb.zip -d /opt && \
    ln -s /opt/graphdb-free-8.2.0 /opt/graphdb && \
    rm /tmp/graphdb.zip

EXPOSE 8080
CMD ["/opt/graphdb/bin/graphdb"]