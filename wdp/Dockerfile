#FROM rhel7:7.3-45
FROM centos:latest
#MAINTAINER Westpac Digital Platform
#
#If there's no artifactory connection then uncomment the following lines to replace the commands below.
#
#ADD artifactory.repo /etc/yum.repos.d/rhel-server.repo
ENV JAVA_HOME /usr/lib/jvm/jre
ENV PATH /usr/local/tomcat/bin:$PATH
RUN yum install curl tar openssl alternatives java-1.8.0-openjdk java-1.8.0-openjdk-headless -y \
#    && yum clean all --disablerepo="*" --enablerepo="rhel-server-rpms" \
    && mkdir -p /usr/local/tomcat \
#   && curl -Ss https://artifactory.srv.westpac.com.au/artifactory/Westpac-Digital-Platform/com/misc/bins/com/apache/tomcat/8.5.8/apache-tomcat-8.5.8.tar.gz \
    && curl -Ss http://www.apache.org/dist/tomcat/tomcat-8/v8.5.8/bin/apache-tomcat-8.5.8.tar.gz \
    | tar xzC /usr/local/tomcat --strip-components=1 --exclude=webapps/\* --exclude=conf/server.xml --exclude=bin/\*.bat --exclude=conf/web.xml \
    && mkdir -p /usr/local/tomcat/lib/org/apache/catalina/util \
    && rm -rf /var/log /var/cache /root/* /tmp/*
#ADD artifactory.repo /etc/yum.repos.d/rhel-server.repo
#ENV JAVA_HOME /usr/lib/jvm/jre
#ENV PATH /usr/local/tomcat/bin:$PATH
#RUN rm -f /etc/yum.repos.d/redhat.repo \
#    && yum install curl tar openssl alternatives java-1.8.0-openjdk java-1.8.0-openjdk-headless -y --disablerepo="*" --enablerepo="rhel-server-rpms" \
#    && yum clean all --disablerepo="*" --enablerepo="rhel-server-rpms" \
#    && curl -Ssk 'https://artifactory.srv.westpac.com.au/artifactory/Westpac-Digital-Platform/com/misc/sources/packer-sources/Westpac-Trust-Chain.tar.gz' \
#    | tar xzC /etc/pki/ca-trust/source/anchors \
#    && update-ca-trust enable \
#    && update-ca-trust \
#    && mkdir -p /usr/local/tomcat \
#    && curl -Ss https://artifactory.srv.westpac.com.au/artifactory/Westpac-Digital-Platform/com/misc/bins/com/apache/tomcat/8.5.8/apache-tomcat-8.5.8.tar.gz \
#    | tar xzC /usr/local/tomcat --strip-components=1 --exclude=webapps/\* --exclude=conf/server.xml --exclude=bin/\*.bat --exclude=conf/web.xml \
#    && mkdir -p /usr/local/tomcat/lib/org/apache/catalina/util \
#    && rm -rf /var/log /var/cache /root/* /tmp/*
WORKDIR /usr/local/tomcat
EXPOSE 8080
ADD ServerInfo.properties /usr/local/tomcat/lib/org/apache/catalina/util/ServerInfo.properties
ADD server.xml /usr/local/tomcat/conf/server.xml
ADD web.xml /usr/local/tomcat/conf/web.xml
RUN groupadd -g 900 tomcat \
    && useradd -d /usr/local/tomcat -u 900 -G tomcat -s /bin/sh -M -N tomcat \
    && chown -R tomcat:tomcat /usr/local/tomcat \
    && chmod 400 /usr/local/tomcat/conf/* \
    && chmod -R 300 /usr/local/tomcat/logs \
    && chmod -R 600 /usr/local/tomcat/temp \
    && rm -rf /var/log /var/cache
ENV "SERVICE_TAGS=rhel73-45,jre-180u111-2b15,tomcat-858"
