# httpd-tomcat-correto11

# 参考

- [Dockerで別コンテナでApache+Tomcat連携する | 株式会社CONFRAGE ITソリューション事業部](https://confrage.jp/docker%E3%81%A7%E5%88%A5%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%A7apachetomcat%E9%80%A3%E6%90%BA%E3%81%99%E3%82%8B/)
- [DockerでApacheとTomcat環境構築。ついでにMaven&Java連携 - Qiita ](https://qiita.com/shintaro123/items/a8a3d222d3dd46aba876)
- [Apache HTTP ServerとApache Tomcatを連携させる - しがないPGの自衛記録](https://ashitaka.hateblo.jp/entry/2020/08/16/103012)

# 起動

```bash
# 起動確認
docker-compose up --build
open http://localhost/sample
```

# 解説

```bash:設定ファイル
# httpdの設定ファイルテンプレを出力
mkdir -p ~/httpd-tomcat-correto11/httpd; cd $_
docker run -it --rm httpd:2.4 cat /usr/local/apache2/conf/httpd.conf > httpd.conf
echo 'ProxyPass / ajp://tomcatcorreto11:8009/' > httpd-proxy.conf

# Tomcatの設定ファイルテンプレを出力
mkdir -p ~/httpd-tomcat-correto11/tomcat; cd $_
docker run -it --rm tomcat:9-jdk11-corretto cat /usr/local/tomcat/conf/server.xml > server.xml

```

```conf:httpd/httpd.conf
以下のコメントアウトを外す
#LoadModule proxy_module modules/mod_proxy.so
#LoadModule proxy_ajp_module modules/mod_proxy_ajp.so

以下を追記する
Include conf/extra/httpd-proxy.conf
```

```xml:tomcat/server.xml
以下を
<!-- Define an AJP 1.3 Connector on port 8009 -->
    <!--
    <Connector protocol="AJP/1.3"
               address="::1"
               port="8009"
               redirectPort="8443" />
    -->
    
↓に変更する
<Connector protocol="AJP/1.3"
           address="0.0.0.0"
           port="8009"
           redirectPort="8443"
           secretRequired="false" />
```

