---
title: MDM CS - Colaborative Server (PIM, CE)
---

## Externi odkazy

[Product information](http://www-01.ibm.com/software/data/master-data-management/) - on IBM sites  
[MDM Developers](https://www.ibm.com/developerworks/community/blogs/64033fdd-4a35-4733-852f-a39abcdf4fb3/?lang=en) - on IBM DevelopersWorks  
[MDM training](http://www-304.ibm.com/services/learning/ites.wss/us/en?pageType=page&c=a0000038)  
[MDM 10.1 documentation](http://pic.dhe.ibm.com/infocenter/mdm/v10r1/index.jsp) on IBM InfoCenter  
konkurence - [Informatica MDM](http://www.informatica.com/us/products/master-data-management/mdm/)  

## Interni odkazy

[WAS](was.html)  
[Python](../dev/pzthon.html)  
[JACL](jacl.html)  

## MDM portfolio

## URL aplikace

http://IP:7507/ ... MDM aplikace  
https://IP:9043/ibm/console/ ... WAS Administracni konzole  

## Procesy, adresare, konfiguracni soubory

## Start/stop

**Kompletni stop MDM**
su - -c "/opt/IBM/HTTPServer/bin/apachectl -k stop" ... stop IHS  
$TOP/go/stop_local.sh ... stop MDM  
/opt/IBM/WebSphere/profiles/Dmgr01/bin/stopManager.sh ... stop WAS DMGR  
/opt/IBM/WebSphere/profiles/AppSrv01/bin/stopNode.sh ... stop WAS NODEAGENT  
su - db2inst1 -c "db2stop" ... stop databaze  

**Kompletni start MDM**
db2start ... start DB2  
/opt/IBM/WebSphere/profiles/Dmgr01/bin/startManager.sh ... start WAS DMGR  
/opt/IBM/WebSphere/profiles/AppSrv01/bin/startNode.sh ... Start WAS NODEAGENT  
$TOP/bin/go/start_local.sh ... start MDM  
su - -c "/opt/IBM/HTTPServer/bin/apachectl -k start" ... start IHS  

**Ovladani jednotlivych komponent**
$TOP/bin/go/svc_control.sh --action=start  --svc_name=scheduler_WPCVM ... nastartuje pouze scheduler  

**Status**
$TOP/bin/test_db.sh ... test pripojeni do DB  
$TOP/bin/go/rmi_status.sh ... seznam vseh sluzeb a jejich status  
$TOP/bin/go/get_service_status.sh --svc_name scheduler_LINUX01 ... status komponenty (sluzby)  
$TOP/bin/get_ccd_version.sh ... zobrazi verzi MDM CS  

## Konfigurace

$TOP/bin/conf/env_settings_ini ... zakladni soubor konfigurace  
$TOP/setup.sh ... prvni konfigurace prostredi (cesty ke konfiguraci env_settings and $TOP) + test prostredi (php knihovny, syntaxe envv_settings_ini)  
$TOP/bin/configureEnv.sh ... generovani konfiguracnich souboru (xml, atd.). Prepise vsechny konf. soubory krome common.properties  
$TOP/etc/default/common.properties ... hlanvni nastaveni MDM. Neni prepsano configureEnv.sh, jen updatovano. Neni realtime, je treba restartovat sluzbu  
$TOP/etc/default/log.xml ... konfigurace logu MDM - zmena je realtime, netreba restartovat JVM  
$TOP/etc/default/data_entry_properties ... konfigurace IHM (WAS aplikace), memeni polozek portalu - pridavani novych menu a JARek. Neni online, potreba restart WAS  
$TOP/etc/default/db.xml ... obsahuje data na pripojeni DB  
$TOP/etc/default/mdm_cache.properties ... cache parametry pro objekty  

## Logy

Pokud neni urceno jinak, tak jsou logy v $TOP/log, v adresarich ${komponenta}_${instance} a v User_Logs.

default.log ... udalosti komponenta  
db.log ... pomale requesty (20 minut), ne pro jednotlive BD query  
svc.pid ... pid procesu  
svc.out ... informace ze startu sluzby (classpath, jake sluzby komponenty jsou spusteny atd)  
svc.err, exception.log ... chyby  

## Procesy - komponenty

rmi_LINUX01 ... RMI Registry - ELF process - ktery dela directory services pro MDM CS  
admin_LINUX01 ... java com.ibm.ccd.admin.common.Admin  
eventprocessor_LINUX01 ... java com.ibm.ccd.common.event.EventProcessor  
workflowengine_LINUX01 ... java com.ibm.ccd.workflow.common.WorkflowEngine  
queuemanager_LINUX01 ... java com.ibm.ccd.connectivity.common.QueueService  
appsvr_LINUX01 ... WAS  
scheduler_LINUX01 ... java com.ibm.ccd.scheduler.common.Scheduler  

## monitoring

bin/go/rmi_status.sh (perl /elixas/IBM/MDMPIM/bin/perllib/rmiStatus.pl) ktery spusti java tridu com.ibm.ccd.admin.common.RootAdmin na URL trigo_url=http://FRELIXPRDAS1A.loreal.wans:7514) neni
vhodny na monitoring - kdyz nejede MDM, dlouhy timeout, kdyz jede ukaze vsechny procesy, neupozorni, kdyz nejake procesy chybi. Lze zkombinovat s jinym skriptem ktery obhospodari jine podminky (existence RMI portu, timeout, pocet procesu).
Stejne to nepokryje vetsinu pripadu, kdy pocess existuje, ale neni funkcni.

Efektivni je monitorovat existenci procesu WAS, httpd, rmiregistry, admin eventprocessor  workflowengine scheduler queuemanager

log monitor SystemOutLog na vsechny exception.log a SystemOut.log

URL monitorin

## Best practice

- Nesestavovat Master Data z casto menicich se polocek - cena atd.

## Struktura DB

Vsechna data se importuji fo tabulky ITA, ulozene sloupce ID (id polozky) a BLOB - serializovana data (specialni format obsahujici vsechny mozne atributy) ktere nejsou citelna z DB, ale pomoci API (napr. trida getItemId(attr1="red"). Pomale na operace, optimalizovane na extenzivni atributy a misto v DB. Tabulky ITM jsou interni idexace produktu podle atributu, interni indexace definovana jen v MDM.
Od MDM9 nelze hledat nezindexovana data. Zavadi se ttabulka s XML. Pro kazdy pridany produkt se data updatuji v ITA, pokud se parametry indexuji, tak se updatuje ITM (idnex) a navic se produkt v XLM forme prida do XLM tabulky, kde probiha hledani v pripade nezindexovanych atributu.
Hledani podle atributu probiha tak, ze se nejdriv vyraz provede na zindexovanych sloupcich - predfiltrovana data, a zbytek se hleda v XML tabulce.
Kazda zmena parametru je verzovana. Zmena se prida jako dalsi polozka do ITA, updatuje se verze starte polozky a prida se do indexu nova verze. Cisteni lze delat jen smazanim starych verzi.

## DocStore

Uloziste dokumentu, nachazi se jak v DB tak i na disku $TOP/public_html/suppliers. Pokud je soubor na disku, musi byt vytovrena reference v DB. Starcim a se o to "sluzba" docstore_mount (docstore_mount.xml je konfigurace). "Colaboration Manager - Document store"

## Repports

Jedna se o joby. Joby jsou but "import", "export", nebo "report". Reporty jsou joby ktere jsou bud napsany MDM skriptovacim jazyku (forma vbs), pripona .script, nebo skripty napsane v shelu nebo perlu na disku. "Product Manager - Repports"

## Zaloha

binarni - adresare s instalaci (MDM, WAS) - pred kazdym updatem, deployem. DB - svechny data v MDM, vcetne DocStore. Je monzo delat studeny i teply backup. Je potreba i zalohovat exporty/importy z/do SAP a byt optrny s restorem aby se neztratily data z importu/exportu

## Scheduler

Je proces, ktery cte v DB co ma delat. Admin proces zapise do DB udelej report1 s parametry1 a scheduler cte kazdych x min/sek tabulku a najde report1 parametry1 co ma vykonat a vykona to.

## Monitoring

uziti tablespaces, disku na DB, disku, procesu, URL, kontrola zprocesovani importu/exportu

## Udrzba

Mazani logu, DocStore, $TOP/src/db/schema/util/oracle/purge_profiles.sh - trace pri profilovani (debugu), $TOP/src/db/schema/util/drop_temp_agg_tables.pl, $TOP/src/db/schema/util/drop_log_tables_seq.pl, $TOP/src/db/schema/util/oracle/delete_versions_before_date.pl, $TOP/bin/db/analyze_schema.sh

## Ovladani pomoci JAVA_RT

. $TOP/bin/compat.sh ... nacte promenne, mimo jine JAVA_RT  
$JAVA_RT com.ibm.ccd.common.wpcsupport.util.SupportUtil --cmd=getRunTimeCacheDetails ... ukaze vyuziti cache  
$JAVA_RT com.ibm.ccd.common.wpcsupport.util.SupportUtil --cmd=getRunTimeMemDetails ... ukaze vyuziti pameti  
$JAVA_RT com.ibm.ccd.common.wpcsupport.util.SupportUtil --cmd=filterLogFiles  --fromtime="${_CCD_FROMTIME}"  --totime="${_CCD_TOTIME}" --srcDir="${WORKDIR}
/pimLogs"  
$JAVA_RT com.ibm.ccd.common.wpcsupport.util.SupportUtil --cmd=getTimeStamp  
$JAVA_RT com.ibm.ccd.common.wpcsupport.util.SupportUtil --cmd=validateAdmin  
$JAVA_RT com.ibm.ccd.common.wpcsupport.util.SupportUtil --cmd=validateServc --svclist=all  

## MDM Skripty

### Export lookup table

```
var envObjList = new EnvObjectList();
envObjList.addAllObjectsToExport("LOOKUP_TABLE_CONTENT");
var result = exportEnv(envObjList, "LOOKUP_CONTENT_export_20140918_153200.zip");
out.println("result: " + result);
```

### Export current “JOB_LOOKUP_EXPORT_” 
Tables content

```
var envObjList = new EnvObjectList();

envObjList.setTypeToExport("LOOKUP_TABLE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_BPG", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_ELIXCORE", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_ELIXPUBLISH", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_ELIXSPEC", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_OGCOM", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_OGDIM", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_SAPTR", null, "CREATE_OR_UPDATE");

envObjList.setTypeToExport("LOOKUP_TABLE_CONTENT");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_BPG", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_ELIXCORE", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_ELIXPUBLISH", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_ELIXSPEC", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_OGCOM", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_OGDIM", null, "CREATE_OR_UPDATE");
envObjList.addObjectByNameToExport("JOB_LOOKUP_EXPORT_SAPTR", null, "CREATE_OR_UPDATE");

var result = exportEnv(envObjList, "JOB_LOOKUP_CONTENT_export.zip");
out.println("result: " + result);
```

### Vymazani BUSINESS RULES

```
var ctgName = "BUSINESS_RULES";

var time1 = today().getTime();

var i = 0;
var item;
forEachCtgItem(ctgName, item) {
	out.writeln("Delete item " + item.getCtgItemPrimaryKey());
	deleteCtgItem(item);
	i++;
}
out.writeln("Deleted items : " + i);

var time2 = today().getTime();
var delay = time2 - time1;
out.writeln("Time : " + delay + " seconds");
```
