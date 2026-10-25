# WebSphere Application Server

### Externi odkazy

[WAS - System requirements](http://www-01.ibm.com/support/docview.wss?uid=swg27006921)  
[Dokumenty k WAS](ftp://ftp.software.ibm.com/software/webserver/appserv/library/)  
[http://download.boulder.ibm.com/ibmdl/pub/software/websphere/wasce/updates/](http://download.boulder.ibm.com/ibmdl/pub/software/websphere/wasce/updates/) ... update k WASCE  
[Trial verze WebSphere Application Server](http://www.ibm.com/developerworks/downloads/ws/was/?S_TACT=105AGX28&S_CMP=TRIALS)  
[Mnoho dokumentace k WAS](ftp://ftp.software.ibm.com/software/webserver/appserv/library/)  
[IBM Support Assistant](http://www-01.ibm.com/support/docview.wss?uid=swg24020502) for WebSphere Application Server  
AST ([L](http://www-01.ibm.com/support/docview.wss?uid=swg24014242),[W](http://www-01.ibm.com/support/docview.wss?uid=swg24014241)) - Application Server Toolkit ([L](ftp://public.dhe.ibm.com/software/websphere/appserv/support/tools/AST/local/refreshpacks/ast61/rp611/esd.image.ast.linux.zip), [W](ftp://public.dhe.ibm.com/software/websphere/appserv/support/tools/AST/local/refreshpacks/ast61/rp611/esd.image.ast.win32.zip))  
[RAD](http://www.ibm.com/developerworks/downloads/r/rad/?S_TACT=105AGX23&S_CMP=DWNL) - IBM Rational Application Developer - Trial  
[WebSphere Application Server Version 6.1 Information Center](http://publib.boulder.ibm.com/infocenter/wasinfo/v6r1/index.jsp?topic=/com.ibm.websphere.nd.doc/info/welcome_nd.html)  
[Connection pooling](http://www-01.ibm.com/software/webservers/appserv/whitepapers/connection_pool.pdf)  
[Redbook - Production Topologies for WebSphere Process Server and WebSphere ESB V6](http://www.redbooks.ibm.com/redbooks/pdfs/sg247413.pdf)  
[IBM DevelopersWork](http://www.ibm.com/developerworks/views/websphere/libraryview.jsp) - Clanky k WebSphere  
[Global WebSphere Comunity](http://www.websphereusergroup.org/)  

### Interni odkazy

[WAS - troubleshooting](was-troubleshoot.html)

### Komponenty

WebSphere Stand alone - typ profilu, ktery hostuje aplikace a neni managovany jinym procesem  
Federated Application Server - (federovany node) typ profilu, ktery hostuje aplikace a je managovany jinym profilem (procesem) - Konfiguracni mnozina je cela (cell)  
Deployment Manager - (dmgr) typ profilu, ktery nehostuje aplikace ale managuje vsechny profily v cele  
Node Agent - nehostuje aplikace ale je prostrednik mezi dmgr a federovanymi nody  
Administrative Agent, Job manager, Secure proxy server  

### Instalace/odinstalace/aplikace oprav

Pro nalezeni WebSphere Aplikacniho Serveru (WAS) je uzitecne vyjmenovat obvykle cesty k WAS soucastem:

<dl>
PLUGIN=/usr/WebSphere/Plugin|/opt/WebSphere/VERZE/Plugin ... AIX|Linux WebSphere HTTP Plugin adresar
WAS=/usr/IBM/WebSphere/AppServer|/usr/Websphere|/opt/IBM/WebSphere/AppServer|C:\program Files\IBM\WebSphere\AppServer ... AIX|AIX|Linux|Win WebSphere AS adresar
PROFILY=/usr/Websphere/profiles|/opt/IBM/Websphere/profiles ... AIX|Linux WAS adresar s profilama
PROFIL=$PROFILY/PROFIL ... Adresar s profilem Aplikacniho Serveru WAS
UI=/opt/IBM/WebSphere/UpdateLinstaller ... Adresar s Update Installerem
WAS/wstemp ... docasna data administracni konzoly
</dl>

V pripade nainstalovanych balicku s WAS, lze hledat nasledujici:

<dl>
lslpp -l | grep WSBAA ... WebSphere Base - Aplikacni server
rpm -qa | grep WSIHS ... WebSphere IBM Http Server
lslpp -l | grep WSPAA ... WebSphere Plugin - Plugin WAS pro HTTP server
</dl>

##### Architektura

Deployment Manager - DMgr - Administracni centralni bod mnoha aplikacnich serveru v administracni skupine - Cell - soucast WAS ND edice (Network Deployment)  
Nodeagent - JVM ktere dela prostrednika mezi DMgr a jednotlivymi servery - spousti, zastavuje, prenasi konfiguraci (synchronizuje)  
Aplikacni servery - bud standalone - administruje se kazdy sam, nebo soucasti Celly - administrovane pomoci Dmgr  
[CIM](http://www.ibm.com/support/knowledgecenter/SSAW57_8.0.0/com.ibm.websphere.installation.nd.doc/info/ae/ae/tins_cim_overview.html) - Centram Installation Manager - centralni misto na instalace, updaty a uninstalace AS  
[Job Manager](https://www.ibm.com/support/knowledgecenter/SS7K4U_8.5.5/com.ibm.websphere.nd.doc/ae/cagt_jobmanager.html) - administracni misto na posilani administracnich ukolu pro AS registrovanych v administracnich agentech ([admin agent](https://www.ibm.com/support/knowledgecenter/SS7K4U_8.5.5/com.ibm.websphere.nd.doc/ae/cagt_adminagent.html)) nebo DMgr. Popis v Redbooku [Flexible Management](http://www.redbooks.ibm.com/redpapers/pdfs/redp4839.pdf)  

##### Instalace

$PATH_TO_INSTALL_MEDIUM/WAS/install ... Instalace pomoci grafickeho pruvodce  
$PATH_TO_INSTALL_MEDIUM/WAS/install -options [response.txt](response.txt) -silent ... ticha instalace bez grafiky  
~/waslogs/* ... logy z instalace - Je treba prepinac traceLevel=INFO pod UNIXem  
C:\Docoments and settings\Administrator\Local settings\Temp\niflogs ... logy z instalace pod Win  
$WAS/logs/install/log.txt ... log instalace  

##### Odinstalace

$WAS/_uninst/uninstall -silent ... odinstalace WASu  

##### Aplikace oprav, update

Spustit **IBM Update Installer** - pruvodce instalaci update-u pro WAS, IHS, ..:
$UI/update.sh ... spusti UpdateInstaller pruvodce  
$WAS/bin/versionInfo.sh ... Verze WASu  
$WAS/logs/update/$VERZE/updatelog.txt

### Webove sluzby

http://HOSTNAME:9060/admin ... Administracni konzola na Manazeru Distribuovanych serveru  
https://HOSTNAME:9043/admin ... Administracni konzola na Manazeru Distribuovanych serveru - SSL  
http://HOSTNAME:9060/ibm/console ... Administracni konzola na Standalone aplikacnim serveru  
http://localhost:9080/bpc ... Portal WPC - WebSphere Process Serveru  
http://localhost:9080/snoop ... test interniho HTTP transportu  
http://localhost:9080/WSamples  
http://localhost:9080/PlantsByWebSphere  
https://localhost:9443/snoop ... test SSL HTTPS transportu  

### WAS: Start/Stop/Status

$WAS/bin/* ... binarky z tohoto adresare spousti akce na vychozi (default) profil, pokud se nezada jinak. Stejne binarky jsou v $PROFIL/bin a ty se spousti na dany profil  
$PROFIL/bin/serverStatus -all ... Vypise status vsech serveru  
$PROFIL/firststeps/firststeps.sh ... prvni kroky po instalaci profilu v WAS - zakladni konfigurace profilu, start/stop  
$PROFIL/bin/startNode.sh NODE ... Spusti node NODE v distribuovanem systemu  
$PROFIL/bin/startServer.sh AppServerN ... Spusti aplikacni server AppServerN v profilu PROFIL  
$PROFIL/bin/startManager.sh ... spusti Deployment manager  
$PROFIL/bin/stopServer.sh ... zastaveni Aplikacniho serveru  
$PROFIL/bin/stopNode.sh NODE ... Spusti node NODE v distribuovanem systemu  
$PROFIL/bin/stopManager.sh ... spusti Deployment manager  
$IBMHTTP/bin/apachectl start ... start IBMhttp server po startu WAS  

### WAS: konfiguracni binarky

$WAS/bin/* ... binarky z tohoto adresare spousti akce na vychozi (default) profil, pokud se nezada jinak. Stejne binarky jsou v $PROFIL/bin a ty se spousti na dany profil  
$PROFIL/bin/ProfileCreatcd or/pctPLATFORM ... Profile Creation Wizard  
$PROFIL/firststeps/firststeps.sh ... Graficky nastroj - prvni kroky po instalaci profilu v WAS - zakladni konfigurace profilu, start/stop, ivt, pmt, stusteni prikladu a admin konzoly, odkaz na infocentrum  
$PROFIL/bin/migration.sh ... Migration Wizard  
$PROFIL/bin/ivt.sh ... Installation Verification Test  
$PROFIL/bin/ivt.sh server1 default -p 9081 -host myhost  
$PROFIL/bin/pmt.sh ... Profile Management Tool - graficky nastroj na vytvareni profilu  

$WAS/java/bin/java -cp ws_runtime.jar com.ibm.ws.security.util.PasswordEncoder secret ... zakoduje heslo ve verzi 6.1  
$WAS/java/bin/java -cp ws_runtime.jar com.ibm.ws.security.util.PasswordDecoder {xor}LDo8LTor ... rozkoduje heslo ve verzi 6.1  
$WAS/java/bin/java -cp securityimpl.jar:iwsorb.jar::ras.jar:wsexception.jar:bootstrap.jar:emf.jar:ffdc.jar com.ibm.ws.security.util.PasswordEncoder secret ... zakoduje heslo secret ve verzi 6  
$WAS/java/bin/java -cp securityimpl.jar:iwsorb.jar::ras.jar:wsexception.jar:bootstrap.jar:emf.jar:ffdc.jar com.ibm.ws.security.util.PasswordDecoder {xor}LDo8LTor ... rozkoduje heslo {xor}LDo8LTor ve verzi 6  
${WAS_HOME}/java/bin/java -Djava.ext.dirs=${WAS_HOME}/plugins:${WAS_HOME}/lib com.ibm.ws.security.util.PasswordDecoder {xor}JycnJycnJyc= ... dalsi moznost  
$WAS/java/bin/java -cp securityimpl.jar:iwsorb.jar com.ibm.ws.security.util.PasswordEncoder secret ... zakoduje heslo secret ve verzi 5  
$WAS/java/bin/java -cp securityimpl.jar:iwsorb.jar com.ibm.ws.security.util.PasswordDecoder {xor}LDo8LTor ... rozkoduje heslo {xor}LDo8LTor ve verzi 5  
$WAS/bin/PropFilePasswordEncoder $PROFIL/properties/soap.client.props com.ibm.SOAP.liginPassword ... zakoduje heslo v souboru s heslem pro wsadmin  
$PROFIL/bin/addNode.sh DMGRSERVER DMGRPORT ... federace nodu v profilu PROFIL k bunce (cell) spravovane DMGR DMGRSERVER s SOAP portem DMGRPORT  
$PROFIL/bin/removeNode.sh DMGRSERVER DMGRPORT ... odtrzeni nodu v profilu PROFIL od bunce (cell) spravovane DMGR  
$PROFIL/bin/renameNode.sh DMGRSERVER DMGRPORT NOVEJMENO ... Prejmenovani nodu v profilu PROFIL v bunce (cell) spravovane DMGR na NOVEJMENO  
$PROFIL/bin/syncNode.sh DMGRSERVER DMGRPORT ... Synchronizace nastaveni **STOPLEHO** nodu v profilu PROFIL v bunce (cell) spravovane DMGR podle konfigurace na DMGR
$PROFIL/bin/syncNode.sh DMGRSERVER DMGRPORT -stopservers -restart ... Automaticky stopne servery, zesynchronizuje a nastartuje servery  
$PROFIL/bin/backupConfig.sh ... zazalohovani profilu  
$PROFIL/bin/restoreConfig.sh ... obnoveni profilu ze zalohy  
$WAS/bin/manageprofiles.sh -help ... spravce profilu - vytvareni/mazani/vypis/informace. Stejne prepinace jako u wasporfile + neco navic  
$WAS/bin/manageprofiles.sh -setDefaultName PROFIL ... nastavi vychozi profil  
$WAS/bin/manageprofiles.sh -backupProfile PROFIL ... zazalohuje profil  
$WAS/bin/manageprofiles.sh -restoreProfile PROFIL ... obnovi profil ze zalohy  
$WAS/bin/manageprofiles.sh -create -profileName AP1 -serverName AS1 -cellName TestCell -nodeName TestNode1
$WAS/bin/ProfileManagement/pmt.sh ... Profile Management Tool - Pruvodce vytvarenim profilu  
$WAS/bin/wasprofile.sh ... spravce profilu v nizsich verzich nez 6.0. Nahrazen prikazem manageprofiles.sh  
$WAS/bin/wasprofile.sh -help ... napoveda  
$WAS/bin/wasprofile.sh -delete -help ... napoveda k mazani profilu  
$WAS/bin/wasprofile.sh -delete -profile PROFILE ... smaze profil  
$WAS/bin/wasprofile.sh -create -profileName PROFILE -profilePath PROFILEPATH -templatePath install_root/profileTemplates/default -nodeName NN -hostName HN -serverName SN ... Vytvoreni profilu  
$WAS/bin/wasprofile.sh -listProfiles ... seznam profilu  
$WAS/bin/wasprofile.sh -getName -profilePaht PP ... jmeno profilu podle cesty  
$WAS/bin/wasprofile.sh -getPath - profileName PROFILE ... cesta profilu podle jmena  
$WAS/bin/wasprofile.sh -validateRegistry ... Otestovani integrity registru profilu  
$WAS/bin/wasprofile.sh -validateAndUpdateRegistry ... Otestovani integrity registru profilu, smaze profily, ktere nelze najit  
wsadmin -c "$AdminApp install /home/myDir/myApps/App1.ear {-appname appl1}" ... pomoci [JACL](../jacl/) prikazu nainstaluje balicek s aplikaci  
wsadmin -lang jython -c "AdminApp.install('/home/myDir/myApps/App1.ear', '[-appname appl1]')" ... pomoci [jythonu](../jython/) nainstaluje balicek s aplikaci  
wsadmin -f skript.jacl ... spusti jacl script  
wsadmin -lang jython -f skript.py ... spusty Jython script  
wsadmin -f test1.jacl -profile setup.jacl -conntype SOAP -port mymachinesoapportnumber -host mymachine ... SOAP spojeni na server mymachine a spusti jack skript pod profilem nadefinovanem v setup.jacl  
wsadmin -conntype NONE -c "$AdminApp uninstall app" ... lokalni uninstall aplikace  
wsadmin -lang jython -conntype NONE -c "AdminApp.uninstall('app')" ... lokalni uninstall aplikace pomoci jythonu  
$WAS\bin\WASService.exe ... konfigurace WAS jako sluzby  
$WAS\bin\WASService.exe -add "Deployment Mgr -serverName dmgr -profilePath "C:\...\DmgrProfile1" -restart true ... Registrace sluzby  
$WAS\bin\WASService.exe -remove ... Registrace sluzby  
[ikeyman](ssl.html) ... prace s SSL klici  
[gsk7cmd](ssl.html) ... prace s SSL klici  

### Logy

$PROFIL/logs/dmgr/SystemOut.log ... Logy Deployment Manageru  
$PROFIL/logs/nodeagent/SystemOut.log ... Logy Node Agenta (start/stop nodu)  
$PROFIL/logs/nodeagent/stopServer.log ... Logy Node Agenta - Stop nodu  
$PROFIL/logs/nodeagent/startServer.log ... Logy Node Agenta - Start nodu  
$PROFIL/logs/APPSERVER/SystemOut.log ... Logy aplikacniho serveru APPSERVER  
$PROFIL/logs/APPSERVER/stopServer.log ... Logy aplikacniho serveru APPSERVER - Stop serveru  
$PROFIL/logs/APPSERVER/startServer.log ... Logy aplikacniho serveru APPSERVER - Start serveru  
install_root/logs/wasprofile/ ... logy prikazu wasprofile
$PROFIL/wstemp ... sessions jednotlivych uzivatelu pres webovou administracni konzolu  
$PROFIL/log/AboutThisProfile.txt ... Informace o vytvorenem profilu (porty atd)  
??/commandAssistanceJythonCommands_USER.log ... logy Admin konzole  

### Konfiguracni soubory

$PROFIL/config/cells/$CELL/nodes/$NODE/serverindex.xml ... porty  
$PROFIL/config/cells/$CELL/virtualhosts.xml ... porty  
$PROFIL/config/cells/$CELL/security.xml ... nastaveni bezpecnosti, napriklad secure pristup k admin konzole atd  
$PROFIL/config/cells/FRELIXPRDAS1CCellAPAC/fileRegistry.xml ... nastaveni uzivatelu  

### Sledovani/ladeni vykonu

PMI ( Performance Monitoring Infrastructure ) ... Monitoring and Tuning > Performance Monitoring Infrastructure (PMI)  

### Sluzby, poskytovatele sluzeb

##### JMS

SIB (Service Integration Bus) je "domena zprav" ve vychozim WebSphere AS. Na SIB se definuji jednotlivi clenove SIBu - jednotlive AS, ve kterych zpravidla byva vytvoren Messaging Engine.  
1. Application servers &gt; server_name &gt; SIB service &gt; SIB_name &gt; Configuration reload enabled ... povoleni aktivace nekterych zmen bez restartu SIBu (Aplikacnich serveru, ktere jsou cleny SIBu)  

##### JDBC

[Oracle 10 JDBC](http://www.oracle.com/technetwork/database/enterprise-edition/jdbc-10201-088211.html) ovladace  

##### Webovy server a webove sluzby

Vytvoreni Weboveho Serveru je potreba k umozneni **generovani konfiguracniho** souboru k [WebSphere Pluginu](plugin.html). U IHS serveru s povolenou administracni konzolou umoznuje
 Webovy server i **stop** a **start** weboveho serveru, **propagaci konfiguracniho souboru**, atd.

<tt>Servers &gt; Server Type &gt; Webserver &gt; New</tt>  

Virtualni skupiny slouzi k vytvoreni tzv. skupin, ktere patri do stejneho Virtualniho jmena "Virtual Name". Obvykle 1 http server, nebo obecne 1 server s IP adresou hostuje nekolik
 domen - virtualnich jmennych adres. Do virtualni skupiny pak prirazujeme jednotlive aplikace, ktere jsou pod jedno virtualniu jmennou adresou. V nastaveni virtualni skupiny je treba
 nastavit vsechny porty, na kterych http server bude poslouchat a ktere nesledne bude preposilat WebSphere Aplikacnimu Serveru

Environment &gt; Virtual hosts &gt; default_host &gt; Host Alliases &gt; *:80  

Aplikace, ktera bude k dispozici pres HTTP server se musi nastavit, aby byla HTTP serveru pristupna (skrz plugin). Neni-li asociovana k Webovemu serveru, HTTP server nepouziva pro URL
 plugin ale hleda stranku v adresari se statickymi strankami definovanem v HTTP serveru (napr. httpd.conf)

Applications &gt; WebSphere enterprise applications &gt; APLIKACE &gt; Manage Modules ... Oznacit webovy modul web.xml a oznacit aplikacni server i webovy server, pote dat aplikovat a restartovat
 aplikaci. Nasledovne se vygeneruje a propaguje konfiguracni soubor pluginu  

### Aplikace

Ziskani URL aplikace: HTTP konfiguracni soubor + Plugin + application.xml a web.xml meta deskriptor aplikace  
grep context-root $PROFIL/InstalledApps/*/*.ear/META-INF/application.xml ... application.xml deskriptor aplikace  
grep url-pattern $PROFIL/InstalledApps/*/*.ear/*.war/WEB-INF/web.xml ... web.xml deskriptor aplikace  

### wsadmin prostredi

wsadmin pouziva k administraci 5 zakladnich commandu: AdminControl, AdminConfig, AdminApp, AdminTask a Help  
$WAS/web/mbeanDocs/index.html ... Popisy vsech MBean typu  

### shell: uzitecne prikazy

ps -ef | grep -v grep | grep WebS | awk '{ print $(NF-2),$(NF-1),$(NF) }' | sort | uniq  
ps -ef | grep httpd | grep -v grep | awk '{ print $9,$10,$11,$12,$13,$14 }' | sort | uniq  
LANG=en_US
