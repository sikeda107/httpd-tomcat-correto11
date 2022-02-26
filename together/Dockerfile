FROM tomcat:9-jdk11-corretto

RUN yum update -y \
    && yum install -y curl less vim tree procps\
    httpd
RUN rm -rf /var/cache/yum/* \
    && yum clean all

# Httpd
COPY httpd.conf /etc/httpd/conf/httpd.conf
COPY httpd-proxy.conf /etc/httpd/conf/extra/httpd-proxy.conf

# Tomcat
WORKDIR /usr/local/tomcat/webapps/
RUN curl -LO https://tomcat.apache.org/tomcat-9.0-doc/appdev/sample/sample.war
COPY server.xml /usr/local/tomcat/conf/server.xml

COPY --chown=root:root entrypoint.sh /app/entrypoint.sh
RUN chmod 755 /app/entrypoint.sh
EXPOSE 80 8009 8000
ENTRYPOINT ["sh","-c","/app/entrypoint.sh"]