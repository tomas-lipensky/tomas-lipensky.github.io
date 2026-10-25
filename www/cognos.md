# Cognos BI

### Interni odkazy

<dl>
<dt>[Externi odkazy](#odkazy)</dt>
</dl>

### Externi odkazy

[Cognos BI training](www.ibm.com/cognos/training)  
[IBM Support page](https://www-947.ibm.com/support/entry/myportal/support)  
[Fixlist for Cognos BI 10.2](http://www-01.ibm.com/support/docview.wss?uid=swg27027081)

### Cognos portfolio

Cognos BI je zakladni produkt, jsou k dispozici dalsi placene nadstavby - FPM (financial performacne mangement) a nastroj pro KPI  

### Procesy, adresare, konfiguracni soubory

cgsServer ... External Report Server  
BmtMDProviderMain ... Metadata Service - The metadata service handles metadata requests including lineage, queryMetadata, updateMetadata, and testDataSourceConnection.  
BIBusTKServerMain ... report server process  
CAM_LPSvr ... is related to the cognos authentication with LDAP, one process for each authentication provider  
java com.cognos.xqe.cubingservices.DQServer ...  
java com.ibm.cgsBus.CGSServer ...  
java org.apache.catalina.startup.Bootstrap ...  

### Start/stop/status/info

cogconfig.sh -stop ... stop Cognosu  
cogconfig.sh -s ... start Cognosu  
cogconfig.sh -s -nolockcheck -notest  
cogbootstrapservice -stop -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -start -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -restart -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -isrunning -install_root=/usr/ibm/cognos/c10_64 -stdoutLog=INFO ... status Cognosu  
cogbootstrapservice -isrunning -install_root=/usr/ibm/cognos/c10_64 -stdoutLog=DEBUG ... status Cognosu - podrobny vypis testovanych sluzeb  
[Verze Cognosu](http://www-01.ibm.com/support/docview.wss?uid=swg21338694)  

### konfigurace cognosu

configuration/cogstartup.xml ... konfigurace Cognosu
