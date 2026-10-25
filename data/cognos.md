# Cognos BI

### Interni odkazy

### Externi odkazy

[Cognos BI training](www.ibm.com/cognos/training)  
[IBM Support page](https://www-947.ibm.com/support/entry/myportal/support)  
[Fixlist for Cognos BI 10.2](http://www-01.ibm.com/support/docview.wss?uid=swg27027081)
[DW - IBM Cognos Proven Practices: Securing the IBM Cognos 10 BI Environment](http://www.ibm.com/developerworks/data/library/cognos/security/cognos_bi_platform/page602.html)  
[DW - IBM Business Analytics Proven Practices: IBM Cognos BI Dispatcher Routing Explained](http://www.ibm.com/developerworks/data/library/cognos/infrastructure/cognos_specific/page510.html)  
[IBM Cognos Planning and BI Backup and Recovery Guide (Updated)](http://www.ibm.com/developerworks/data/library/cognos/page324.html)  
[IBM Cognos Proven Practices: IBM Cognos 10 Dynamic Query Analyzer User Guide](http://www.ibm.com/developerworks/data/library/cognos/infrastructure/cognos_specific/page578.html)  
[Logging Console and Monitoring](http://www.ibm.com/developerworks/data/library/cognos/page80.html)  

### Cognos portfolio

Cognos BI je zakladni produkt, jsou k dispozici dalsi placene nadstavby - FPM (financial performacne mangement) a nastroj pro KPI  

### Procesy, adresare, konfiguracni soubory

cgsServer ... External Report Server  
BmtMDProviderMain ... Metadata Service - The metadata service handles metadata requests including lineage, queryMetadata, updateMetadata, and testDataSourceConnection.  
BIBusTKServerMain ... Business Intelligence BUS, proces ktery provadi DB dotazy ke generovani reportu  
CAM_LPSvr ... is related to the cognos authentication with LDAP, one process for each authentication provider  
java com.cognos.xqe.cubingservices.DQServer ...  
java com.ibm.cgsBus.CGSServer ...  
java org.apache.catalina.startup.Bootstrap ... Apache Tomcat - webovy kontejner, ktery poskytuje webovy portal s reportama  

### Start/stop/status/info

[cogconfig.sh](http://www-01.ibm.com/support/knowledgecenter/SSEP7J_10.2.0/com.ibm.swg.ba.cognos.c8pp_inst.10.2.0.doc/c_zig_commandlineoptions.html) -stop ... stop Cognosu  
cogconfig.sh -s ... start Cognosu  
cogconfig.sh -s -nolockcheck -notest  
cogbootstrapservice -stop -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -start -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -restart -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -isrunning -install_root=/usr/ibm/cognos/c10_64 -stdoutLog=INFO ... status Cognosu  
cogbootstrapservice -isrunning -install_root=/usr/ibm/cognos/c10_64 -stdoutLog=DEBUG ... status Cognosu - podrobny vypis testovanych sluzeb  
[Verze Cognosu](http://www-01.ibm.com/support/docview.wss?uid=swg21338694)  

### Prikazy

[dcadmin](http://www-01.ibm.com/support/docview.wss?uid=swg27040451) ... ovladani sluzby Dynamic Cubes  

### URL

IP:80/ibmcognos ... IBM Cognos portal na Webovem serveru  
IP:9300/ ... Websphere Liberty vychozi stranka  
IP:9300/p2pd/servlet ... IBM Cognos Content Manager  
localhost:9300/p2pd/servlet/dispatch/ext ... IBM Cognos Connection bez grafiky  
localhost:9300/p2pd/servlet/dispatch ... IBM Cognos Connection s grafikou  
localhost:9300/p2pd/cm_tester.htm ... Content manager tester  
/p2pd/servlet/gc ... info o verzi a stavu dispatchera  
/p2pd/servlet/ping ... test dispatchera. HTTP kod 200 - dispatcher je pripraven  

### konfigurace cognosu

configuration/cogstartup.xml ... konfigurace Cognosu  
$COGHOME/bin/[ij.sh](http://www.ibm.com/support/knowledgecenter/SSWGNW_8.0.0/com.ibm.swg.im.cognos.inst_cr_winux.8.4.1.doc/inst_cr_winux_id7206derby_create_content_store.html%23derby_create_content_store) ... nastroj na managovani a vytvareni Cognos Content databaze  

### Logy

$COGDIR/cogserver.log ... sloupce: HostID;PID;Time;TZ;SessionID;RequestID;SubrequestID;StepID;Thread;Component;BuildNb;Level;Logger;Operation;Object;Status;Message;LogData  
egrep "[A-Z]+-[A-Z]+-[0-9]+" cogserver.log* | sed -e 's/.*[^A-Z]\([A-Z]*-[A-Z]*-[0-9][0-9]*\).*/\1/' ... ukaze chybove kody  

### Nastroje

$COGHOME/bin/runlvV2.sh ... prohlizec logu  
I.C.E.T.E.A ... analyza logu, analyza Cognos prostredi
