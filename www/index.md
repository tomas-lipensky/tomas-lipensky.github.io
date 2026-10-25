# index

### Architektura

(Load Balancer + Proxy cache) --- (HTTP server) --- (Plugin) --- (Aplikacni server) --- (Aplikace na AS, jako treba WP, WSS, ...)

Aplikace zpravidla bezi bud v Web kontejneru (programove prostredi umoznujici aplikaci vystupovat na netu), EJB konterneru (programove prostredi umoznujici aplikacim komunikovat s firemnim
 softwarem  jako treba DB, ERP, oddelene od webu a obecnymi aplikacemi (aplikace zahrnujici v sobe ruzne programovaci kody, jako treba C/C++, ... WAS Network Deployment). Jednotlive aplikace
 mezi sebou nejcasteji komunikuji pomoci JMS zprav. K tomu slouzi JMS infrastruktura, zajistovana napriklad WAS SIB, MQ, WESB atd. Pro komunikaci mezi jednotlivymi programy lze pouzivat SSL
 sifrovani pomoci [SSL klicu](ssl.html).

### load balancery, proxy cache atd.

<dl>
IBM Edge Load Balancer ... Load balancer od IBM
Pyranha ... Load balancer od RedHat
Infinspas ... cachovani dat, soucast JBoss projektu
[memcached](http://memcached.org/) ... Distribuovany, vykonny, opensource program pro cachovani dat
</dl>

### HTTP servery

<dl>
[IHS](ihs.html) (IBM HTTP Server + [WAS plugin](plugin.html))
IIS ... Internet Information Services (apache od Microsoft)
[lets encrypt](https://letsencrypt.org) - Autorita vydavajici SSL/TSL klice zdarma
</dl>

### Aplikacni servery

<dl>
[JVM](../sw/java.html) obecne
[WAS (WebSphere Application Server)](was.html)
WAS ESB (WAS Enterprise Service Bus) ... WAS rozsireny o spravu Service Busu - messagingu
WASCE - WebSphere AS Community Edition + [update k wasce](http://download.boulder.ibm.com/ibmdl/pub/software/websphere/wasce/updates/) - WebSphere pro komunitu zalozeny na Apache Geronimo
[JBoss AS](jboss.html) - JBoss Application Server (RadHat) ... Aplikacni server od RedHatu. Soucas JBosse je Apache TomCat
[Oracle WebLogic Server](wlc.html), drive Bea WLC
Apache [Tomcat](tomcat.html) (Apache) - Webovy kontejner
Apache Geronimo - Aplikacni server od Apache, obsahuje Webovy kontejner Tomcat, nebo Jetty, ActiveMQ (JMS), OpenEJB (EJB), OpenJPA, ServiceMix (ESB), Axis (SOAP), Derby (DB), WADI (Clustering, Load Balancing) atd.
Apache TomEE - Jiny aplikacni server od Apache, obsahujici Tomcat (Web Kontejner), ActiveMQ (JMS), OpenEJB (EJB), OpenJPA, MyFaces (JSF), CXF (SOAP), Derby (DB) a OpenWebBeans
Internet Application Server (iAS), drive Oracle Application Server (OAS) a jeste drive Oracle Web Server (OWS)
</dl>

### Performance testing

[Load Impact](https://app.loadimpact.com/account/login)
[Load Impact agent](https://support.loadimpact.com/3.0/monitoring-agents/load-impacts-open-source-monitoring-agents/)  

### JMS (Java messaging service)

Aplikace zajistujici vymenu zprav ci souboru mezi aplikacemi jako sluzbu. Komplexni Aplikacni servery (WAS, ...) v sobe obsahuji JMS providery, ale specializovane aplikace mohou poskytnout lepsi vykon, konfiguravatelnost a management sluzeb zprav.

<dl>
[Websphere MQ](mq.html) = MQ Series (IBM), [MBroker](mqsi.html)
JBoss Messaging, HornetQ (RedHat)
Oracle AQ (Oracle)
Tibco Enterprise Message Service (Tibco)
Apache ActiveMQ ... implementace JMS
Apache ServiceMix ... ESB
Apache Camel ... ESB
WAS - SIB (Service Integration Bus) + enterprise balicek <!--a href="wesb.html"-->IBM WESB - WebSphere Enterprise Service Bus<!--/a-->
TalenD ESB ... OpenSource ESB
WebSphere ESB
</dl>

### Aplikace

Aplikace v aplikacnich serverech vetsinou byvaji balene v baliccich:
- WAR - balicek obsahujici webobou aplicaci - prezentacni vrstvu - zip archiv obsahujici metainformace definujici zakladni vlastnosti aplikace, Java knihovny - JAR, staticke stranky a jejich komponenty (css, obrazky, js, ...) a aktivni stranku (jsp, ...)
- EAR - Enterprise balicek - obsahuje balicek WAR a sadu komponent k entrerprise vrstve a metadate k ni
- JAR - balicek obsahujici javovske tridy - komponenta kazdeho WAS a EAR

### Aplikacni reseni postavene na Aplikacnich serverech

<dl>

<dt>Commerce - nastroje pro obchod:</dt>
IBM WSC (WebSphere Commerce) ... kompletni reseni pro e-commerce postavene na WebSphere AS, IBM Http Server a DB2
[FAS (Fredhopper Access Server)](fas.html)

<dt>Informacni portaly:</dt>
[IBM WP (WebSphere Portal)](wp.html)
JBoss EPP ... JBoss Enterprise Portal Platform, Soucasti JBoss Portal jako WebSphere Portal
GateIn Portal ... jako WebSphere Portal

<dt>Aplikace na rizeni procesu:</dt>
IBM WPS (WebSphere Process Server) ... WAS ESB Rozsireny o spravu procesu
[flownimd](http://www.softscout.com/software/Project-and-Business-Management/Flowcharting-and-Process-Modelling/FlowMind%28TM%29.html) ... Webovy a javovy integracni balik, ktey umoznuje graficke modelovani a definovani procesu

<dt>Aplikacni servery pro telekomunikace:</dt>
Mobicents (RedHat) ... Aplikacni server pro telekomunikace

<dt>Aplikace pro bankovnictvi:</dt>
[SAB](http://www.sab-tm.com/) ... kombinace Cobol aplikaci a aplikace pro aplikacni server integrujici web-based interface se cobol enginem

<dt>[Aplikace pro manipulaci dat - Business inteligence, warehousing, big data](../data/)</dt>

<dt>Aplikace na sledovani aplikacnich serveru:</dt>
[ITCAMDC](itcamdc.html) (IBM Tivoli  Composite Application Manager) ... Data Collector

</dl>

### Aplikacni komponenty, API:

Vetsina javovych aplikaci pouziva obecne komponenty, ktere uznadnuji jejich beh a vyvoj.

<dl>
Apache Jetspeed2 ... portal od Apache pod Apache licenci
Apache Axis2 ... Implementace SOAP od Apache pro poskytovani WebServices. Upoznuje pridat WebServices (komunikujici treba pres SOAP) Webovym Aplikacim, nebo provozovat samotne WebService aplikace
</dl>

### Testovani

<dl>
[JMeter](http://jmeter.apache.org/) ... Apache produkt k testovani vykonnosti Webu (http, https), SOAP, mailu atd
[Java HotSwap](http://code.google.com/p/hotswap/) ... Technologie na dynamicke nahravani javovskych trid bez restartu JVM
</dl>

### Vyvojove a integracni nastroje (IDE)

<dl>
Eclipse
Application Server Toolkit ... Rozsireni Eclipse
Rational Application Developer ... Prostredi rozsirujici Eclipse zahrnujici funkce Application Server Toolkit a dalsi
IBM WebSphere Integration Developer ... Nastroj rozsirujici Rational Application Developer o business procesy. Integrace s WebSphere ESB Server, WebSphere Express Server, WebSphere Process Server, WebSphere Server, Tomcat Server
JRebel ... plugin do IDE na online implementace javovskych trid do JVM (pomoci HotSwap)
</dl>

### Inspekce a kontrola sitoveho toku

[Sitovy tok](network_flow.html)  
telnet a specificky protokol viz [dev/http](../dev/http.html), smtp, ...  

### Vyvoj

<dl>
[http](../dev/http.html)
[html](../dev/html.html)
[css](../dev/css.html)
[javascript](../dev/javascript.html)
<!--dd>[php](../dev/php.html)</dd-->
[java](../dev/java.html)
[j2ee](j2ee.html) - Webove java aplikace
</dl>

### Prohlizece

Firefox  
[Mozilla wiki](https://developer.mozilla.org/en-US/docs/Mozilla/)  
[Vivaldi](https://vivaldi.com)  
Chrome  
curl ... CLI web klient  
wget ... CLI web klient
