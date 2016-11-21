#FROM rhel7:7.3-45
#Replaced RHEL with latest centos & changed Maintainer name
FROM centos
MAINTAINER WDP Poc Team


#Making changes to the file from here. We don't and we won't have access to the artifactory repository
#ADD artifactory.repo /etc/yum.repos.d/rhel-server.repo

ENV JAVA_HOME /usr/lib/jvm/jre
ENV PATH /usr/local/tomcat/bin:$PATH


RUN yum install curl tar openssl alternatives java-1.8.0-openjdk java-1.8.0-openjdk-headless -y  \
    && yum clean all  \
    && update-ca-trust enable \
    && update-ca-trust \
    && mkdir -p /usr/local/tomcat \
    && curl -S http://apache.mirror.serversaustralia.com.au/tomcat/tomcat-8/v8.5.8/bin/apache-tomcat-8.5.8.tar.gz \
    | tar xzC /usr/local/tomcat --strip-components=1 --exclude=webapps/\* --exclude=conf/server.xml --exclude=bin/\*.bat --exclude=conf/web.xml \
    && mkdir -p /usr/local/tomcat/lib/org/apache/catalina/util \
    && rm -rf /var/log /var/cache /root/* /tmp/*



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

ENV "SERVICE_TAGS=centos,jre-180u111-2b15,tomcat-858"

CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
