FROM httpd:2.4

RUN apt update \ 
&& apt install curl

COPY httpd.conf /usr/local/apache2/conf/httpd.conf
COPY httpd-proxy.conf /usr/local/apache2/conf/extra/httpd-proxy.conf

EXPOSE 80