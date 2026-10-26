---
title: Tomcat
---

## Externi odkazy

[Tomcat Tutorial](http://www.coreservlets.com/Apache-Tomcat-Tutorial/)  
[Tomcat Manager](http://tomcat.apache.org/tomcat-4.1-doc/manager-howto.html)  
[http://tomcat.apache.org/](http://tomcat.apache.org/)  
[Apache http + Tomcat](http://www.root.cz/clanky/apache-20-amp-tomcat-41/)  

## Tomcat Manager

http://{host}:{port}/manager/{command}?{parameters}  
http://localhost:8080/manager/html ... pripojeni do managera  
http://localhost:8080/manager/status ... status pameti a prostredi  
http://localhost:8080/manager/list ... seznam a status aplikaci  
http://localhost:8080/manager/sessions?path=/aaa ... status sessions pro aplikaci aaa  
http://localhost:8080/manager/sessions?path=/aaa ... status sessions pro aplikaci aaa  

### Tomcat konfigurace

$tomcat/conf/server.xml ... porty, context root atd  
  &lt;host&gt;&lt;Context path="/aaa" docBase="aaa-1.0-SNAPSHOT"/&gt;&lt;/host&gt; ... jinaci kontext root pro aplikace aaa-1.0-SNAPSHOT  
$tomcat/conf/ENGINE/HOST/APLIKACE.xml (napr. $tomcat/conf/Catalina/localhost/example.xml)  
$tomcat/conf/
$tomcat/conf/tomcat-users.xml ... uzivatele, hesla a role
