# FAS - Fredhopper Access Server

### Externi odkazy:

[FAS](http://www.cse.chalmers.se/research/hats/node/150) (Fredhopper Access Server)  
[Clanek a dokumnetace k FAS](http://www.itu.dk/courses/DSDS/F2010/notes/j_kohne_thesis.pdf)  
[Brief introduction to FAS](http://www.hats-project.eu/node/150)  
[Oficialni (placena) dokumentace](https://www.fredhopper.com/learningcenter/display/learningcenter)  
[ETL](http://en.wikipedia.org/wiki/Extract,_transform,_load)Extract Transform Load proces  
[SDL Fredhopper](http://retailingtoday.com/article/sdls-cloud-based-solution-optimizes-online-shopping-experience) - clanek  

### Fredhopper

Produkt Fredhopper - FAS je program, ktery umi naseptavat pri psani textu do vyhledavaciho policka, umi zobrazovat relevantni produkdy atd., umi strukturovat url tak,
aby vyhledavace umely prohledat web (SEO) a umi reportovat data z fredhopperu. Soucasti fradhoperu jsou:

<li>Program samotny - ktery obsahuje aplikacni server - jboss (ale umi jet i pod jinymi) a aplikaci samotnou</li>

<li>Instance - jednotlive "profily", instance mohou mit ruzne funkce a muze jet vice instanci na jednou pocitaci</li>
<li>Deployment agent - javovsky program na snadnou administraci fredhopperu a jeho instanci, transfer souboru, konfiguraci a instalaci</li>
<li>Data manager - Nastroj na ETL - import dat do FAS</li>
<li>Business manager - Web nastroj na business konfiguraci (business.xml, i18n - lokalizace, enrich.py, atd.)</li>
<li>kitchen ... customizovatelny nastroj na import dat z DB do XML a pote do Derby DB</li>
<li>qserver - spousteny $FAS/j2ee/jboss/bin/run.sh -c fas - engine ktery provadi vyhledavani polozek z DB a indexu na zaklade webovych pozadavku (obecne z aplikace - WCS, WAS atd)</li>
<li>treebuilder - spousteny $FAS//bin/treebuilder -u catalog01 -U 0 -I 1 ... Vytvari seznamy kategorii a prirazuje k nim polozky</li>
<li>searchindexer - spousteny $FAS/bin/searchindexer -I 1 ... Vytvari indexy z klicovych slov pouzivanych v qserveru na vyhledavani v datech z DB</li>
<li>xmlloader - spousteny $FAS/bin/xmlloader -I 1... Nastroj na transformaci dat z xml z kitchen a import do treebuilderu searchindexeru</li>
<li>syncclient - spousteny $FAS/bin/syncclient -I 1 -s SYNCSERVERNAME -P PORT ... nastroj na prijimani dat do LIVE qserveru obecne po indexaci</li>
<li>reporting ... (reporting.pentaho.com) nastroj na reportovani a statistiky vyhledavani</li>

Kazda instance obahuje vlastni procesy. Tyto procesu jsou: searchindexer, xmlloader, treebuilder, syncclient, syncserver, reporting, qserver.

##### Single Start/Stop

$FAS/bin/qserver ... start qserveru  
$FAS/bin/reporting ... start reportingu  
$FAS/bin/qserver stop ... stop  
$FAS/bin/reporting stop ... stop  

/home/fredhopper/instance01/FAS/j2ee/jboss/bin/run.sh -c fas  
/bin/sh bin/syncclient -I 1 -s BO1P01FRHS01 -P 8100  

/home/fredhopper/instance01/FAS/j2ee/jboss/bin/run.sh -c fas  
/home/fredhopper/instance01/FAS/bin/searchindexer -I 1  
/home/fredhopper/instance01/FAS/bin/treebuilder -u catalog01 -U 0 -I 1  
/home/fredhopper/instance01/FAS/bin/xmlloader -I 1  

##### info

ps -ef | grep java | awk -F"/" '{ a=1; for (i=1; i<=NF; i++) if [^1]

[^1]: $(i) ~ "PRO") || ($(i) ~ "WORK") || ($(i) ~ "LIVE" a=i; } ; { if (a != 1) print ($a) }' ... ukaze bezici instance  
ps -ef | grep java | sed 's/-classpath [^ ]**g' | sed 's/-X[^ ]**g' | sed 's/-D[^ ]**g' | sed 's/\s\+/ /g' | sed -e 's/\S* \S* \S* \S* \S* \S* \S* *' ... Ukaze java procesy bez  
$INSTANCE/bin/get-qserver-port ... port, na kterem bezi qserver  
$[^2]

[^2]:  $($FAS/bin/get-qserver-port) + 100  ... port, na kterem bezi reporting  

### Deployment Agent

##### Start/Stop/Status

Sluzba ktera umoznuje ovladat jednotlive instance a nabizi k tomu krome klienta (deployment-agent-client) i webove rozhrani (http://localhost:8177).

~/bin/fredhopper start/stop/status ... Start/stop/status Deployment agenta. Spusti: ~/bin/deployment-agent nebo ~/bin/deployment-agent-client stop-agent  
~/bin/deployment-agent start/stop ... Nastartuje/zastavi DA pomoci ~/deployment-agent/bin/deployment-agent  
~/deployment-agent/bin/deployment-agent ... Spusti java proces s com.fredhopper.deployment.agent.AgentBooter tridou  

##### Ovladani a konfigurace pomoci Deployment agenta

bin/deployment-agent-client ... vypise napovedu k prikazum  
bin/deployment-agent-client info ( http://localhost:8177 ) ... vypise informace o instancich, verzi DA atd.  
bin/deployment-agent-client environment ( http://localhost:8177/environment ) ... Seznam promennych prostredi  
bin/deployment-agent-client list-installations ( http://localhost:8177/installation ) ... Seznam instalaci komponent (FAS, DM)  
bin/deployment-agent-client describe-installation FAS ( http://localhost:8177/installation/FAS ) ... Ukaze, kde je komponenta nainstalovana  
bin/deployment-agent-client install ... nainstaluje komponentu ze zdrojoveho kodu  
bin/deployment-agent-client uninstall FAS ... odinstaluje komponentu FAS  
bin/deployment-agent-client list-instances ( http://localhost:8177/instance ) ... seznam instanci  
~/bin/deployment-agent-client list-processes INSTANCE ( http://localhost:8177/instance/INSTANCE/process/ ) ... seznam procesu dane instance  
bin/deployment-agent-client list-universes LIVE1 ... seznam promennych dane instance  
~/bin/deployment-agent-client list-verbs INSTANCE qserver ( http://localhost:8177/instance/INSTANCE/process/qserver ) ... seznam akci/statusu  
bin/deployment-agent-client describe-instance INSTANCE ( http://localhost:8177/instance/INSTANCE ) ... Vypise podrobne informace o instanci, portech atd., , pokud jede Deployment Agent  
bin/deployment-agent-client get-option LIVE1 qserver_memory ... Vypise prepinac qserver_memory z instance LIVE1  
bin/deployment-agent-client set-option LIVE1 qserver_memory=2000 ... nastavi prepinac  
bin/deployment-agent-client delete-option LIVE1 qserver_memory ... smaze prepinac  
bin/deployment-agent-client rename-instance LIVE1 LIVE2 ... prejmenuje instanci z LIVE1 na LIVE2  
bin/deployment-agent-client create -I 3 LIVE1 FAS ... vytvori instanci c. 3 (jedouci na portu 3*1000 + 7180 ) - LIVE1 v instalaci FAS  
bin/deployment-agent-client remove LIVE1 ... smaze instanci LIVE1  
bin/deployment-agent-client invoke LIVE1 qserver stop ( http://localhost:8177/instance/LIVE1/process/qserver/verb/stop ) ... provede akci (stop) na danem procesu (qserver) a instanci (LIVE1)  
bin/deployment-agent-client import-capture STAGING ... import zalohy konfigurace  
bin/deployment-agent-client export-capture STAGING ( http://localhost:8177/instance/STAGING/capture ) ... export nastaveni konfigurace instance STAGING  
bin/deployment-agent-client list-jmx LIVE2 qserver ( http://localhost:8177/instance/LIVE2/process/qserver/monitor ) ... Seznam JMX objektu procesu qserver instance LIVE2
bin/deployment-agent-client list-jmx LIVE2 qserver mbeans.fredhopper.com:type=QServer ( http://localhost:8177/instance/LIVE2/process/qserver/monitor/mbeans.fredhopper.com:type=QServer ) ... Vypis atributu JMX objektu  
bin/deployment-agent-client get-jmx LIVE2 qserver mbeans.fredhopper.com:type=QServer QServerState ( http://localhost:8177/instance/LIVE2/process/qserver/monitor/mbeans.fredhopper.com:type=QServer/QServerState ) ... Vypise hodnotu atributu JMX objektu  
bin/deployment-agent-client add-role STAGING FAS/staging.xml ... prida roli do instance LIVE2 z xml souboru  
bin/deployment-agent-client list-roles STAGING ( http://localhost:8177/instance/STAGING/role ) ... seznam roli instance STAGING  
bin/deployment-agent-client get-role STAGING staging ( http://localhost:8177/instance/STAGING/role/staging ) ... popis role staging na instanci STATING  
bin/deployment-agent-client remove-role LIVE2 qserver ... smaze roli qserver  
bin/deployment-agent-client invoke-command LIVE1 stop ( http://MA1FHORS01:8177/instance/LIVE1/role/qserver/stop ) ... Vyvola zastaveni role na instanci LIVE1  
curl http://localhost:8177/instance/INSTANCE/stop ... zastavi celou instanci  
http://localhost:8177/instance/NORTH_PRODREADY1/capture ... ulozi konfiguraci instance  
~/bin/deployment-agent-client list-roles WEST_PRODREADY2 ... seznam roli  
bin/deployment-agent-client --location <HOST> get --instance <INSTANCE> config/java.options.<PROCESS> > tmp/java.options.txt ... stahne soubor z jineho serveru na kterem bezi DA  
bin/deployment-agent-client --location FHORS01 put --instance LIVE1 config/java.options.qserver tmp/java.options.txt ... posle soubor na jiny server na kterem bezi DA  
bin/deployment-agent-client --location FHORS01 delete --instance LIVE1 config/aaa ... smaze soubor na jinem serveru na kterem bezi DA  

### Ostatni spustitelne soubory

bin/chk-up LIVE1 ... zkontroluje kazdych 20 sec. dostupnost qserveru, indexy a upozorni na (ne)dostupnost a pocet polozek  
bin/chk-publishing STAGING ... zkontroluje datum business.xml pro publikace (v data/business)  
bin/chk-valid-index LIVE1 ... zkontroluje indexy a podindexy instance LIVE1 oproti minimalimu cislu polozek MINITEMS nastavenych ve config/fasrc. RC=0, pokud je polozek vic.  
bin/ws-query localhost 12180 'fh_location=/companyitems/nl_NL/categories&lt;{manutan_3074457345616669470_8563771665917835204}' ... posle dotaz na qserver a vrati datum,cas,queryID,page_time,round_trip_time,query  
bin/ws-query localhost 12180 '//company/de_CH&amp;fh_secondid=7158312898563771665917839687' ... dalsi dotaz

```
~/bin/instance INSTANCE start/stop ... it will manually start/stop individual INSTANCE on the server. It runs ~/bin/run-job jobs/ACTION-instance-with-variable.kjb -Didentifier=INSTANCE. INSTANCE is from:
	ls ~/data/instances | grep _

~/bin reindex INSTANCE ... Index creation - it will process the reindexing. It starts ~bin/run-job jobs/reindex-all-instances.kjb -Didentifier=$INSTANCE, where INSTANCE is WORKSPACE1 or PRODREADY1 from
	ls ~/data/instances | grep _

~/bin/fresh-index-to-live AREA_PRODREADY1 preprod ... Deployment of the index to the Query server PRODREADY. I will lunch: ~/bin/run-job jobs/fresh-index-and-config-to-live.kjb -Didentifier=$INSTANCE -Dlive=$LIVE

~/bin/run-etl-job ... runs    ~/bin/data-manager-blocking-process etl kitchen $@
~/bin/run-job    ...  runs    ~/bin/data-manager-blocking-process deployment kitchen $@
~/bin/data-manager-blocking-process ... runs    ~/bin/deployment-agent-client invoke $1 $2 start -DfileName=$3 -DlogLevel=basic $4+ and then it chacks every 2 seconds the status until it is not STOPPED (~/bin/deployment-agent-client invoke $1 $2 status)
~/bin/deployment-agent-client ... runs ~/deployment-agent/bin/deployment-agent-client $@
~/deployment-agent/bin/deployment-agent-client ... runs java process with com.fredhopper.deployment.client.CLIMain class
```

##### Role:

Role je definice procesu, ktere se startuji, ci stopuji pri spusteni instance. Zda se, ze existuji pouze pri existency Deployment Agenta.  
lynx http://localhost:8177/instance/INSTANCE/role  
ls $INSTANCE_PATH/role ... seznam roli a jejich xml definice  

### URL qserveru

http://localhost:8180/fredhopper/query ... zobrazovani dotazu ve forme XML  
http://localhost:8180/preview/  ... zobrazovani dotazu ve forme html  
http://localhost:8180/status/ ... zobrazeni casu spusteni qserveru  
http://localhost:8180/fredhopper/up.txt ... zobrazeni  casu spusteni qserveru  
http://localhost:8180/fredhopper/xml/index.jsp?fh_log=0  
http://localhost:8180/fredhopper-ws/services/FASWebService?wsdl .. dotaz na qserver  
http://localhost:8180/fredhopper ... Fredhopper Business manager - urava konfigurace  
http://localhost:20180/fredhopper/sysadmin/ ... System admin - provadeni nekterych akci na qserveru  
wget -O - http://MA1FHORS01:8180/fredhopper/sysadmin/reload-config.jsp?select=business ... znavu nacte business.xml  

##### Konfiguracni soubory

topology.txt ... definice instanci pro vytvoreni instalace pomoci ?cluster-config?. Cislo instance urcuje porty isntance. napr. instance 1 -> 7180 + 1*1000, 10 -> 7180 + 10*1000.  
$FAS/conf/instance ... cislo instance  
$FAS/conf/instance.conf ... config portu a dalsich globalnich promennych JVM (memory,...) - To same pomoci DA: "deploymneet-agent-client describe-instance"  
$FAS/conf/java.options* ... JVM parametry procesu  
$FAS/conf/enrich.py ... config nastaveni ktere se budur respektovat behem ?indexace?  
$FAS/conf/business.xml ... business konfigurace pro qserver a indexaci  
$FAS/conf/repporting-instance.conf ... globalni nastaveni pro pentaho reporting (ports, memory, ...)  

##### LOG soubory

data/log/agent.log ... log deployment agenta  
data/instances/deployment/log/kitchen.log ... log deployment procesu (publikace konfigurace)  
data/instances/etl/log/kitchen.log ... log ETL procesu (indexace)  
data/instances/<INSTANCE>/log/qserver.log  ... log JBoss AS - pri spusteni qserveru  
data/instances/<INSTANCE>/log/fredhopper.log  ... Fredhopper udalosti v qserveru  
data/instances/<INSTANCE>/log/xmlloader.log  ... logy xml loaderu  
data/instances/<INSTANCE>/log/searchindexer.log ... logy searchindexeru  
data/instances/<INSTANCE>/log/treebuilder.<UNIVERSENAME>.log ... logy treebuilderu  
data/instances/<INSTANCE>/log/syncserver.log ... logy synchronizavniho serveru (na STAGING)  
data/instances/<INSTANCE>/log/syncclient.log ... logy synchronizavniho klienta (na LIVE)  
~/data/instances/etl/log/kitchen.log  
~/data/log/agent.log ... deployment agent log  
~/data/instances/etl/log/pan.log ... output of data manager transformation (ETL - extract, transform, load)  
~/data/instances/<INSTANCE>/log/*log ... FAS logs of an instance  

### Priklady JMX objektu

http://MA1FHORL01:8177/instance/LIVE1/process/searchindexer/monitor/mbeans.fredhopper.com:type=ItemStore/IndexingId  
/instance/<INSTANCE>/process/qserver/monitor/mbeans.fredhopper.com:type=ItemStore/ItemCount  
instance/<INSTANCE>/process/qserver/monitor/mbeans.fredhopper.com:type=QServer/DeploymentServerRole (bin/deployment-agent-client get-jmx SOUTH_LIVE1 qserver mbeans.fredhopper.com:type=QServer DeploymentServerRole) ... Vypise jakou roli jede qserver (staging/live)  
/instance/<INSTANCE>/process/qserver/monitor/mbeans.fredhopper.com:type=ItemStore/ItemCount ... Celkovy pocet nahranych indexu  
/instance/<INSTANCE>/process/qserver/monitor/mbeans.fredhopper.com:engine=<UNIVERSE>-<LOCALE>,server=Server,type=Search/Alive ... Vrati "true" pokud je vyhledavani nastavene a dostupne pro danou universe-locale kombinaci.  
/instance/<INSTANCE>/process/qserver/monitor/mbeans.fredhopper.com:type=Tree,universe=<UNIVERSE>/NavigationIndexSize ... Pocet polozek v navigation index pro specificky universe. Nejzajimavejsi k monitorovani je pocet polozek v produktovem rejstriky (universe).  
/instance/<INSTANCE>/process/qserver/monitor/mbeans.fredhopper.com:engine=<UNIVERSE>-<LOCALE>,indextype=<INDEX>,server=Server,type=Search/Size ... Vrati pocet polozek pro universe-locale-index typ kmbinace. Available index types are  : "Index for spell correction suggestions", "Index over specific attributes of items", "Index over text content of items"  
http://localhost:8177/instance/LIVE1/process/qserver/monitor/java.lang:name=ConcurrentMarkSweep,type=GarbageCollector/CollectionCount ... Ukaze pocet Full GC od startu procesu  

### REPORTING:

V FAS &lt; 7 je soucasti FAS reporting. Konkretne Pentaho reporting:

bin/install .. nainstaluje (preinstaluje) parametery. Smaze java nastaveni a znovu vytvori  
$FAS/reporting/db ... Vzor Derby DB  
$FAS/data/reporting/DB6 ... Derby DB - Pro vycisteni reportingu je treba smazat  
INFO: Inflating reporting/BACKUP.HISTORY  
INFO: Inflating reporting/service.properties  
INFO: Inflating reporting/log/log.ctrl  
INFO: Inflating reporting/log/logmirror.ctrl  
INFO: Inflating reporting/log/log180737.dat  
reporting/seg0/*  
Config: reporting-instance.conf: instanceX_reporting_qserver  (port napr. 8180) (server.xml)  
Config - reporting-instance.conf: instanceX_reporting_jbossport (port napr. 8280)  
(reporting-instance.conf - instance1_reporting_jbossport=8280 )  

URL:  
http://localhost:8280/pentaho ... login  
http://localhost:8280/status/ ... status reportu
