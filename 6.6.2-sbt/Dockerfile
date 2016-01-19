FROM centos:7

MAINTAINER Ivan Subotic "ivan.subotic@unibas.ch"

# IMPORT the Centos-7 GPG key to prevent warnings
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7

# Add bintray repository where the SBT binaries are published
RUN curl -sS https://bintray.com/sbt/rpm/rpm | tee /etc/yum.repos.d/bintray-sbt-rpm.repo

# Base Install + JDK + SBT
RUN yum -y update && \
    yum -y install java-1.8.0-openjdk && \
    yum -y install java-1.8.0-openjdk-devel && \
    yum -y install sbt && \
    yum -y install unzip && \
    yum -y update bash && \
    rm -rf /var/cache/yum/* && \
    yum clean all
    
# Run SBT once so that all libraries are downloaded
RUN sbt exit

# Install GraphDB-Free
RUN curl -sS -o /tmp/graphdb.zip -L http://info.ontotext.com/e/45622/7a-graphdb-free-6-6-2-dist-zip/2q3hp8/748768455 && \
    unzip /tmp/graphdb.zip -d /opt && \
    ln -s /opt/graphdb-free-6.6.2 /opt/graphdb && \
    rm /tmp/graphdb.zip

ADD run.sh /run.sh
RUN chmod +x /*.sh

EXPOSE 8080
CMD ["/run.sh"]