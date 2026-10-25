# Watson Explorer

Puvodne Data Explorer od [Vivisimo](http://en.wikipedia.org/wiki/Vivisimo), pozdeji Vivisimo prevzala IBM a prejmenovala na IBM Infosphere Data Explorer, nyni IBM Watson Explorer. Data Explorer umi prochazet informacni zdroje, at jiz uvnitr
podniku ci na internetu ci u obchodnich partneru, indexovat a kolektovat informace a nabizet jejich souhrn a vyhledavani. Komponenty WEX jsou [Zookeeper](https://zookeeper.apache.org/) (centralni spravce konfiguraci a synchronizaci sluzeb, podporujici clustery) a [Velocity](http://velocity.apache.org/engine/1.7/overview.html) (template engine - MVC pristup) od Apache.

### Interni odkazy

### Externi odkazy

[Pekny popis WEX na DW](https://www.ibm.com/developerworks/community/blogs/IMRedbooks/entry/a_quick_view_of_ibm_infosphere_data_explore?lang=en)  
[Knowledge Center](http://www.ibm.com/support/knowledgecenter/en/SS8NLW_11.0.0/watsonexplorer_11.0.0.html)  

### Procesy, adresare, konfiguracni soubory

org.apache.zookeeper.server.quorum.QuorumPeerMain ... [Zookeeper](https://zookeeper.apache.org/)  
/opt/IBM/IDE/AppBuilder/wlp/bin/tools/ws-server.jar AppBuilder ... AppBuilder  
org.eclipse.help.base.infocenterApplication ... InfoCenter  
/opt/IBM/IDE/ResultsModule/wlp/lib/ws-launch.jar ResultsModule ... results module  
/opt/ibm/IDE/Engine/bin/indexer-service  
/opt/ibm/IDE/Engine/bin/collection-service  
/opt/ibm/IDE/Engine//bin/collection-service-dispatch  
/opt/ibm/IDE/Engine/bin/query-service  
/opt/ibm/IDE/Engine/webserver/httpd ... Apache Http Server  

### Start/stop/status/info

<b>Start</b>  
nohup /opt/ibm/IDE/InfoCenter/IC_start.sh &amp; ... spusti Data Explorer InfoCenter  
/opt/IBM/IDE/Engine/bin/velocity-startup --yes --start-query-service ... spusti Data Explorer Engine vcentne WebServeru  
nohup /opt/IBM/IDE/ResultsModule/wlp/bin/server start ResultsModule & ... spusti Data Explorer Results Module  
/opt/IBM/IDE/ZooKeeper/zookeeper/bin/zkServer.sh start ... nastartuje ZooKeeper  
nohup /opt/IBM/IDE/AppBuilder/wlp/bin/server start AppBuilder & ... nastartuje AppBuilder  
<b>Stop</b>  
/opt/IBM/IDE/Engine/bin/velocity-shutdown --yes ... zastavi Data Explorer Engine vcetne Web Serveru  
/opt/IBM/IDE/ResultsModule/wlp/bin/server stop ResultsModule ... zastavi Data Explorer Results Module  
/opt/IBM/IDE/AppBuilder/wlp/bin/server stop AppBuilder ... zastavi AppBuilder  
/opt/IBM/IDE/ZooKeeper/zookeeper/bin/zkServer.sh stop ... zastavi ZooKeepra  
/opt/ibm/IDE/InfoCenter/IC_end.sh ... zastavi Data Explorer InfoCenter  
/mnt/DataExplorer/IDE/Engine/bin/velocity-webserver stop ... stop jen Web Serveru  

<b>Status</b>  
/mnt/DataExplorer/IDE/Engine/bin/velocity-webserver info ... status Web Serveru  
velocity-cmd ping ... zkusi ping Explorera  
Engine/bin/velocity-status ... Status Data Explorera, vypis procesu  

### Sluzby

http://localhost:9080/vivisimo/cgi-bin/admin  
http://localhost:9081/ResultsModule  
http://localhost:9082/AppBuilder
