---
title: IBM Infosphere - Datastage
---

## Odkazy

[IIS - dokumentace](http://www-01.ibm.com/support/docview.wss?uid=swg27041358#qs)  
[IIS system requirements](http://www-01.ibm.com/support/docview.wss?uid=swg27036191)  
[Datastage training](www.ibm.com/datastage/training)  
[IBM Education manager - Monitoring memory consumption of datastage process](http://publib.boulder.ibm.com/infocenter/ieduasst/imv1r0/index.jsp?topic=/com.ibm.iea.infosphere_is/infosphere_is/8.5/ProbDeter/MemoryUsage/player.html)  
[IBM Education manager - Datastage](http://publib.boulder.ibm.com/infocenter/ieduasst/imv1r0/index.jsp?topic=/com.ibm.iea.datastage/plugin_coverpage.html)  
[InfoSphere DataStage](https://www-947.ibm.com/support/entry/myportal/product/information_management/infosphere_datastage?productContext=-2069227258) - stranka podpory  
[IBM InfoSphere Information Server, system requirements](http://www-01.ibm.com/support/docview.wss?uid=swg21315971)  
[Datastage tutorial](http://etl-tools.info/en/datastage/datastage_tutorial.htm)  

## Komponenty

Datastage (Infosphere Information Server) se sklada z nekolika komponent:

- Designer - windows program na vytvareni ETL jobu
- Director - windows program na spousteni a kontrolu jobu
- Administrator - windows program na administraci DS (projekty, uzivatele atd.
- Manager - windows program na prohlizeni a editaci DS repozitare (tabulek, jobu, transformaci, ..)

## Procesy, adresare, konfiguracni soubory

Pekny popis Datastage [procesu](https://dstagenotes.wordpress.com/tag/dsrpcd/)

*dsrpcd ... DSRPC Service - Datastage RPC (Remote Procedure Call) - soucast DS Engine - umoznuje DS klientum pripojit se k DS engine  
ps -ef | grep dscs ... pocet pripojenych klientu (proces adfdscs)  
ps -ef | grep dsapi_slave ... pocet klienty pristupujicich k repozitari (proces dsapi_slave)  
ps -ef | grep "JobMonApp" ... proces ktery zachytava vykonostni statistiky  
ps -ef | egrep -e "phantom|osh" ... zrovna jedouci ETL ulohy  
com.ibm.iis.common.wlm.service.server.ds.DSWLMServer ... IBM Information Server WorkLoad Management(WLM) Server  
com.ibm.datastage.runtime.odbqapp.server.ODBQueryAppSocketServer  
[com.ibm.datastage.runtime.engmonapp.EngMonApp](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.5.0/com.ibm.swg.im.iis.ds.monitor.doc/topics/intro.html)  
com.ascential.acs.logging.agent.LoggingAgentSocketImpl ... Logging agent - loguje udalosti do metadata repozitare  
com.ibm.datastage.runtime.resmonapp.ResMonApp  
ResourceTracker  
DSAppWatcherStart / DSAppWatcher.exe... App Watcher Service  
RunAgent / ASBAgent - (Unix/Win) predava pozadavky Sluzebni vrstvy (service layer) do InfoSphere Information serveru  
tl_dsservice ... DSTELNET windows sluzba umoznujici pripojeni telnetem  
dsservice.exe ... DataStage Engine Resource Service sluzba  

## Start/stop/status/info

DS=`cat /.dshome` ... instalacni cesta instance (popripade .dshome2)  
. $DS/dsenv ... inicializace prostredi  
$DS/bin/uv -admin -stop ... stop DS sluzeb (Engine) (DSEngine, uvrpc daemon, JobMonApp, resource_tracker)  
$DS/bin/uv -admin -start ... start DS sluzeb  
$DS/bin/uv -admin -info ... informace o instance (verze, lokace, status)  
$DS/../ASBNode/bin/NodeAgents.sh stop ... zastavi ASB agenty  
$DS/../ASBNode/bin/NodeAgents.sh start ... spusti ASB agenty  
cat $DS/.dsrel ... verze IIS Datastage  
$DS/Version.xml ... verze IIS Datastage
ipcs|grep adf ... sdilena pamet Datastage  
netstat -a|grep dsrpc ... sitovy tok datastage  
$DS/../DSODB/bin/DSAppWatcher.sh -status ... status sluzeb ktere sbiraji data (AppWatcher, EngMonApp, ODBQueryApp, ResMonApp)  
$DS/../DSODB/bin/DSAppWatcher.sh -start EngMonApp ... start EngMonApp  
$DS/Server/PXEngine/java/jobmoninit -stop ... zastavi JobMonApp resource_tracker  
$DS/Server/PXEngine/bin/shutdown_trackers [-local | -configFile $CONFIG_FILE] ... zastavi jen resource_tracker  

## URL

http://IP:port/ibm/iis/launchpad/ ... rozcestnik pro konzole  
http://IP:port/ibm/iis/console/ ... Web Administration console pro IIS  
http://IP:port/ibm/iis/dc/console/ ... Operations console pro IIS  
http://IP:port/ibm/imam/console/main/main.jsp ... Metadata Asset Manager  
http://IP:port/ibm/iis/qs/StandardizationRulesDesigner ... Standardization Rules Designer  
http://IP:port/ ... Web console pro Datastage verze 8 a niz  
http://IP:port/RegistrationServlet/registration ... Java naming space informace  

## Konfigurace

$DS/../../ASBNode/bin/DirectoryCommand.sh ... prace s adresarem uzivatelu a skupin - vyzaduje autentifikaci  
$DS/../../ASBNode/bin/DirectoryCommand.sh -usr isadmin -pwd isadmin -list USERS ... seznam uzivatelu  
$DS/../../ASBServer/bin/DirectoryAdmin.sh -user -userid dsadmin -password HESLOo01 ... prida noveho uzivatele  
$DS/../../ASBServer/bin/DirectoryAdmin.sh -user -s -idp \* -max_count 200 ... seznam uzivatelu  
$DS/../Configurations/  
$DS/../DSEngine/uvconfig ... obecne parametry DS  
$DS/../../Clients/istools/cli/[istool](http://www-01.ibm.com/support/knowledgecenter/SSZJPZ_11.3.0/com.ibm.swg.im.iis.iisinfsv.assetint.doc/topics/commandset.html) ODBAdmin countdb -domain server:port -server server -username dsadm -password dspwd -upto 15 -days -verbose  
$DS/../DSEngine/bin/uvregen ... vygeneruje binarni uvconfig  
$DS/../DSEngine/dsenv ... promenne prostredi  
$DS/uvodbc.config , $PROJECT/uvodbc.config ... konfigurace ODBC spojeni a driveru  
DataStageJobExecutor.properties ... pripojovaci parametry TWS plug-inu pro DS pro kontroly jobu  
/dspx_moteur_pr/IBM/InformationServer/Server/Configurations/default.apt ... konfigurace projektu  
Server/DSODB/DSODBConfig.cfg ... konfigurace pro kolektory dat (AppWatcher, EngMonApp, ODBQueryApp, ResMonApp)  
$DS/../PXEngine/etc/restrack_settings ... konfigurace logu resource trackeru  

## Logy

$DS/../DSWLM/logs/wlm.properties  
grep submitJob wlm.*.log ... vypise kdy se nastartoval jaky job
[Logging agent](http://www-01.ibm.com/support/docview.wss?uid=swg21439251)  

## prikazy

$DS/ASBNode/bin/SessionAdmin.sh -url https://server_hostname:server_port -user username -password plaintext_password -kill-user-sessions ... ukonci neadministratorske pripojeni  
$DS/ASBNode/bin/SessionAdmin -url https://server_hostname:server_port -user username -password plaintext_password -set-maint-mode ON ... zapne maintenance mode - zakaze pripojovat neadministratorskym uctum  
$DS/ASBNode/bin/SessionAdmin -url https://server_hostname:server_port -user username -password plaintext_password -set-maint-mode OFF ... vypne maintenance mode - zakaze pripojovat neadministratorskym uctum  
$DS/bin/dssh ... uvsh ... Universe Shell - Administrator Command Prompt - prikazovy interface, ktery umozni pristup k objektum - historie behu jobu, datasource, ..  
$DS/bin/dssh; LOGTO project_name; DS_CONNECT; DS_CONNECT dsn ... pripojeni do projektu, vylistovani datasourcu, pripojeni k datasourcu  
$DS/bin/dsadmin -listprojects ... seznam projektu  
$DS/bin/dsadmin -listenv PROJ1 ... seznam parametru projektu PROJ1 (APT_CONFIG_FILE je konfigurace a lokace adresare s projektem)  
$DS/bin/dsadmin -listproperties PROJ1 ... dalsi parametry projektu  
$DS/bin/dsjob -lprojects ... seznam projektu  
$DS/bin/dsjob -ljobs PROJEKT ... seznam jobu v projektu  
$DS/bin/dsjob -jobinfo PROJEKT JOB ... informace o jobu  
$DS/bin/dsjob -logsum PROJEKT JOB ... summary udalosti - ktery job kdy jak jel  
$DS/bin/dsjob -report PROJEKT JOB ... podrobny report  
$DS/bin/[dsjob -run](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_8.5.0/com.ibm.swg.im.iis.ds.cliapi.ref.doc/topics/r_dsvjbref_Starting_a_Job.html) PROJECT JOB ... spusti job  
Returncody jobu: 0 RUNNING,1 RUN OK, 2 RUN with WARNINGS, 3 RUN FAILED, 96 UNKNOWN,97 STOPPED, 98 NOT RUNNABLE  
export APT_CONFIG_FILE=/dspx_moteur_pr/IBM/InformationServer/Server/Configurations/default.apt ... potreba pro orchadmin  
$DS/../PXEngine/bin/orchadmin ... prace s Filesetama a datasetama  
$DS/../PXEngine/bin/orchadmin diskinfo -a .. ukaze info o discich  
$DS/../PXEngine/bin/orchadmin check  
DSXImportService -List –DSXFile c:\archives\oldproject.dsx ... vylistuje obsah DSX souboru  

## prikazy DS clienta

dscmdimport.exe /H=myfrvmmop1datap /U=domain\user /P=heslo /NUA projekt a.dsx /V ... prenos dsx souboru  
dscc /h server /u domena/uzivatel /p heslo PROJEKT /j JOB  
dssearch -domain DATASTAGEDES:9080 -user wasadmin -password wasadmin -server DATASTAGEDES -ljobs -matches Transformacion *  

## Databaze

- XMETA - x metadata DB - Datastage metadata
- DSODB - Operations database
- IADB - Information Analysis DB - Information Analzer modul - hleda sloupce ktere jsou vhodne na primarni klice a jin
- QSDB - Qualitystage DB - Qualitystage modul

## procesy

com.ibm.iis.common.wlm.service.server.ds.DSWLMServer  
com.ascential.acs.logging.agent.LoggingAgentSocketImpl  
com.ibm.datastage.runtime.resmonapp.ResMonApp ... Resource monitor - monitoruje systemove zdroje (CPU, pamet, ..) a zaznamenava je fo DSODB. ResMonApp pouziva ResTrackApp proces na jednotlivych nodech.  
JobMonApp ... job monitor - poskytuje informace o jobu pro Datastage Director  
com.ibm.datastage.runtime.engmonapp.EngMonApp ... engine monitor - DS Engine uklada udalosti do Events adresare. EngMonApp posila data od DSODB a maze soubory  
com.ibm.datastage.runtime.odbqapp.server.ODBQueryAppSocketServer ... Komunikuje s DSODB a predava data ASBAgentovi pro Operations Console a pro "istool ODBAdmin"  
dsrpcd ... Engine - rodicovsky proces jobu - spousti joby (transformace)  
ASBNode/bin/RunAgent ... Node agent - interface mezi WAS a metadata serverem  
Server/PXEngine/DSResourceTracker/bin/ResTrackApp ... Resource tracker - sledovac zdroju (CPU, pameti atd. pro lepsi spravu a pro Operations console) - je potreba pro ResMonApp, ktery posila data do DSODB  
GP1P02IDSP02Node02Cell GP1P02IDSP02Node02 server1  
com.ibm.iis.common.wlm.service.server.ds.DSWLMServer ... WorkLoad Manager Server - spousti v Enginu joby (transformace) na zaklade pravidel (max. pocet soubeznych procesu, priorit atd.)  
DSResourceTracker  
resource_tracker  
DSAppWatcherStart  
com.ascential.acs.logging.agent.LoggingAgentSocketImpl  

## Utility, nastroje

ISA - nastroj na ziskavani informanci o IIS, exporty se posilaji na software support - PMR  

### uvsh - dssh

LOGTO projekt; ... pripojeni k projektu  
SELECT * FROM DS_JOBS; ... seznam IDcek vsech jobu  
SELECT JOBNO FROM DS_JOBS WHERE NAME LIKE '%<JOB NAME>%'  ... zjisti JOBID  
SELECT CATEGORY FROM DS_JOBS WHERE NAME = '$job' ... cesta (adresar) k jobu  
SELECT TIMESTAMP FROM RT_LOG123; ... sezam casu vsech udalosti pro jobID 123  
SELECT TYPE,TIMESTAMP,FULL.TEXT FROM RT_LOGnnn  
SELECT @ID,TYPE,WAVE.NO,TIMESTAMP,MSG.ARGS,MSG.TEXT,FULL.TEXT,SEVERITY FROM RT_LOG974  
SELECT * FROM DS_AUDIT; ... Audit  
CLEAR.FILE RT_LOG$JOBNO; ... vycisti data o behu jobu - umi i "Clear" utilita v Directoru  
LIST DS_JOBS WITH JOBNO=14 ... ukaze co je za job JOBID 14 (data v $PROJECTDIR/RT_CONFIG$JOBID)  
SELECT PATH FROM UV_SCHEMA ... seznam cest k jednotlivym projektum  

## Datastage databaze

db2 connect to xmeta  
select * from [DSODB.JOBRUN](https://www.ibm.com/support/knowledgecenter/en/SSZJPZ_11.5.0/com.ibm.swg.im.iis.ds.monitor.ref.doc/topics/jobruntable.html) fetch first 10 rows ... seznam uloh z Workload managera z DSODB  
[SELECT H.HostName](https://www.ibm.com/support/knowledgecenter/SSZJPZ_11.5.0/com.ibm.swg.im.iis.ds.monitor.doc/topics/queryodb.html), J.ProjectName, J.JobName, R.InvocationId, S.MajorStatusName, R.RunStartTimeStamp  
FROM DSODB.JobExec AS J, DSODB.JobRun AS R, DSODB.Host AS H, DSODB.RunMajorStatusRef AS S  
WHERE  H.HOSTID = J.HOSTID AND  R.JOBID = J.JOBID AND  R.RunMajorStatus = S.MajorStatusCode  
AND  R.RunStartTimeStamp >= '2011-09-26' ORDER BY R.RunStartTimeStamp;
