# index

## Architektura

(Load Balancer + Proxy cache) --- (HTTP server) --- (Plugin) --- (aplikační server) --- (aplikace na AS, například WP, WSS, ...)

Aplikace zpravidla běží buď ve webovém kontejneru (programové prostředí umožňující aplikaci vystupovat na internetu), nebo v EJB kontejneru (programové prostředí umožňující aplikacím komunikovat s firemním softwarem, jako je DB nebo ERP, odděleně od webu a obecných aplikací, tedy aplikací zahrnujících různé programovací kódy, například C/C++; WAS Network Deployment). Jednotlivé aplikace mezi sebou nejčastěji komunikují pomocí zpráv JMS. K tomu slouží infrastruktura JMS zajišťovaná například pomocí WAS SIB, MQ nebo WESB. Pro komunikaci mezi jednotlivými programy lze použít šifrování SSL pomocí [klíčů SSL](ssl.html).

## Load balancery, proxy cache a další

IBM Edge Load Balancer ... Load balancer od IBM  
Piranha ... Load balancer od Red Hatu  
Infinispan ... cachování dat, součást projektu JBoss  
[memcached](http://memcached.org/) ... distribuovaný, výkonný open source program pro cachování dat

## HTTP servery

[IHS](ihs.html) (IBM HTTP Server + [zásuvný modul WAS](plugin.html))  
IIS ... Internet Information Services (Apache od Microsoftu)  
[Let's Encrypt](https://letsencrypt.org) - autorita vydávající certifikáty SSL/TLS zdarma

## Aplikační servery

[JVM](../sw/java.html) obecně  
[WAS (WebSphere Application Server)](was.html)  
WAS ESB (WAS Enterprise Service Bus) ... WAS rozšířený o správu Service Bus a messagingu  
WASCE - WebSphere AS Community Edition + [aktualizace WASCE](http://download.boulder.ibm.com/ibmdl/pub/software/websphere/wasce/updates/) - WebSphere pro komunitu založený na Apache Geronimo  
[JBoss AS](jboss.html) - JBoss Application Server (Red Hat) ... aplikační server od Red Hatu. Součástí JBossu je Apache Tomcat  
[Oracle WebLogic Server](wlc.html), dříve BEA WLC  
Apache [Tomcat](tomcat.html) (Apache) - webový kontejner  
Apache Geronimo - aplikační server od Apache, který obsahuje webový kontejner Tomcat nebo Jetty, ActiveMQ (JMS), OpenEJB (EJB), OpenJPA, ServiceMix (ESB), Axis (SOAP), Derby (DB) a WADI (clustering, load balancing)  
Apache TomEE - jiný aplikační server od Apache obsahující Tomcat (webový kontejner), ActiveMQ (JMS), OpenEJB (EJB), OpenJPA, MyFaces (JSF), CXF (SOAP), Derby (DB) a OpenWebBeans  
Internet Application Server (iAS), dříve Oracle Application Server (OAS) a ještě dříve Oracle Web Server (OWS)

## Performance testing

[Load Impact](https://app.loadimpact.com/account/login)
[Load Impact agent](https://support.loadimpact.com/3.0/monitoring-agents/load-impacts-open-source-monitoring-agents/)  

## JMS (Java Messaging Service)

Aplikace zajišťující výměnu zpráv či souborů mezi aplikacemi jako službu. Komplexní aplikační servery (WAS, ...) v sobě obsahují poskytovatele JMS, ale specializované aplikace mohou poskytnout lepší výkon, konfigurovatelnost a správu služeb zpráv.

[WebSphere MQ](mq.html) = MQ Series (IBM), [MBroker](mqsi.html)  
JBoss Messaging, HornetQ (Red Hat)  
Oracle AQ (Oracle)
Tibco Enterprise Message Service (Tibco)
Apache ActiveMQ ... implementace JMS
Apache ServiceMix ... ESB
Apache Camel ... ESB
WAS - SIB (Service Integration Bus) + enterprise balíček IBM WESB - WebSphere Enterprise Service Bus  
TalenD ESB ... open source ESB
WebSphere ESB

## Aplikace

Aplikace v aplikačních serverech bývají většinou zabalené v balíčcích:

- WAR - balíček obsahující webovou aplikaci a prezentační vrstvu; zip archiv obsahující metainformace definující základní vlastnosti aplikace, knihovny Java (JAR), statické stránky a jejich komponenty (CSS, obrázky, JS, ...) a aktivní stránku (JSP, ...)
- EAR - Enterprise balíček - obsahuje balíček WAR a sadu komponent pro enterprise vrstvu a metadata k nim
- JAR - balíček obsahující javovské třídy - komponenta každého WAS a EAR

## Aplikační řešení postavená na aplikačních serverech

### Commerce - nástroje pro obchod

IBM WSC (WebSphere Commerce) ... kompletni reseni pro e-commerce postavene na WebSphere AS, IBM Http Server a DB2
[FAS (Fredhopper Access Server)](fas.html)

### Informační portály

[IBM WP (WebSphere Portal)](wp.html)
JBoss EPP ... JBoss Enterprise Portal Platform, součást JBoss Portal jako WebSphere Portal  
GateIn Portal ... jako WebSphere Portal

### Aplikace na řízení procesů

IBM WPS (WebSphere Process Server) ... WAS ESB rozšířený o správu procesů  
[FlowMind](http://www.softscout.com/software/Project-and-Business-Management/Flowcharting-and-Process-Modelling/FlowMind%28TM%29.html) ... webový a javovský integrační balík, který umožňuje grafické modelování a definování procesů

### Aplikační servery pro telekomunikace

Mobicents (Red Hat) ... aplikační server pro telekomunikace

### Aplikace pro bankovnictví

[SAB](http://www.sab-tm.com/) ... kombinace aplikací COBOL a aplikace pro aplikační server integrující webové rozhraní s COBOL enginem

### Aplikace na sledování aplikačních serverů

[ITCAMDC](itcamdc.html) (IBM Tivoli  Composite Application Manager) ... Data Collector

## Aplikační komponenty a API

Většina javovských aplikací používá obecné komponenty, které usnadňují jejich běh a vývoj.

Apache Jetspeed2 ... portal od Apache pod Apache licenci
Apache Axis2 ... implementace SOAP od Apache pro poskytování webových služeb. Umožňuje přidat webové služby (komunikující například přes SOAP) webovým aplikacím nebo provozovat samostatné webové služby

## Testování

[JMeter](http://jmeter.apache.org/) ... produkt Apache pro testování výkonu webu (HTTP, HTTPS), SOAP, e-mailu atd.  
[Java HotSwap](http://code.google.com/p/hotswap/) ... technologie pro dynamické nahrávání javovských tříd bez restartu JVM

## Vývojové a integrační nástroje (IDE)

Eclipse
Application Server Toolkit ... rozšíření Eclipse  
Rational Application Developer ... prostředí rozšiřující Eclipse, které zahrnuje funkce Application Server Toolkit a další  
IBM WebSphere Integration Developer ... nástroj rozšiřující Rational Application Developer o business procesy. Integrace s WebSphere ESB Server, WebSphere Express Server, WebSphere Process Server, WebSphere Server a Tomcat Server  
JRebel ... plugin do IDE pro online implementaci javovských tříd do JVM pomocí HotSwap

## Inspekce a kontrola síťového toku

[Síťový tok](network_flow.html)  
telnet a specificky protokol viz [dev/http](../dev/http.html), smtp, ...  

## Vývoj

[http](../dev/http.html)
[html](../dev/html.html)
[css](../dev/css.html)
[javascript](../dev/javascript.html)
[php](../dev/php.html)
[java](../dev/java.html)
[j2ee](j2ee.html) - webové aplikace v Javě


## Generátory statických stránek

[Jekyll](jekyll)

## Prohlížeče

Firefox  
[Mozilla wiki](https://developer.mozilla.org/en-US/docs/Mozilla/)  
[Vivaldi](https://vivaldi.com)  
Chrome  
curl ... webový klient CLI  
wget ... webový klient CLI
