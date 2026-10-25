# IBM Infosphere - Datastage

### Odkazy

[Datastage training](www.ibm.com/datastage/training)  
[IBM Education manager - Monitoring memory consumption of datastage process](http://publib.boulder.ibm.com/infocenter/ieduasst/imv1r0/index.jsp?topic=/com.ibm.iea.infosphere_is/infosphere_is/8.5/ProbDeter/MemoryUsage/player.html)  
[IBM Education manager - Datastage](http://publib.boulder.ibm.com/infocenter/ieduasst/imv1r0/index.jsp?topic=/com.ibm.iea.datastage/plugin_coverpage.html)  
[InfoSphere DataStage](https://www-947.ibm.com/support/entry/myportal/product/information_management/infosphere_datastage?productContext=-2069227258) - stranka podpory  
[IBM InfoSphere Information Server, system requirements](http://www-01.ibm.com/support/docview.wss?uid=swg21315971)  
[Datastage tutorial](http://etl-tools.info/en/datastage/datastage_tutorial.htm)  

### Komponenty

Datastage (Infosphere Information Server) se sklada z nekolika komponent:

- Designer - windows program na vytvareni ETL jobu
- Director - windows program na spousteni a kontrolu jobu
- Administrator - windows program na administraci DS (projekty, uzivatele atd.
- Manager - windows program na prohlizeni a editaci DS repozitare (tabulek, jobu, transformaci, ..)

### Procesy, adresare, konfiguracni soubory

dsrpcd ... Datastage engine  
BmtMDProviderMain ... Metadata Service - The metadata service handles metadata requests including lineage, queryMetadata, updateMetadata, and testDataSourceConnection.  
BIBusTKServerMain ... report server process  
CAM_LPSvr ... is related to the cognos authentication with LDAP, one process for each authentication provider  
java com.cognos.xqe.cubingservices.DQServer ...  
java com.ibm.cgsBus.CGSServer ...  
java org.apache.catalina.startup.Bootstrap ...  

### Start/stop/status/info

. ./dsenv ... inicializace prostredi  
bi/uv -admin -stop ... stop DS  
bi/uv -admin -start ... start DS  
cogbootstrapservice -stop -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -start -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -restart -install_root=/usr/ibm/cognos/c10_64  
cogbootstrapservice -isrunning -install_root=/usr/ibm/cognos/c10_64 -stdoutLog=INFO ... status Cognosu  
cogbootstrapservice -isrunning -install_root=/usr/ibm/cognos/c10_64 -stdoutLog=DEBUG ... status Cognosu - podrobny vypis testovanych sluzeb  
[Verze Cognosu](http://www-01.ibm.com/support/docview.wss?uid=swg21338694)  
cat $DS/Server/DSEngine/.dsrel ... verze IIS Datastage  

### URL

http://IP:port/ibm/iis/console/ ... Web console pro IIS  
http://IP:port/ ... Web console pro Datastage verze 8 a niz  
http://IP:port/RegistrationServlet/registration ... Java naming space informace
