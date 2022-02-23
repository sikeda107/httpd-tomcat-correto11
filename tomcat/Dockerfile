FROM tomcat:9-jdk11-corretto

RUN yum update -y \
&& yum install -y less curl

COPY server.xml /usr/local/tomcat/conf/server.xml

RUN cd /usr/local/tomcat/webapps/ \ 
&& curl -LO https://tomcat.apache.org/tomcat-9.0-doc/appdev/sample/sample.war

EXPOSE 8009