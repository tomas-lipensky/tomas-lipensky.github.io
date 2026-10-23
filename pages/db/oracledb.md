SQL prikazy pro Oracle jsou na strance [Oracle SQL](oraclesql).

### Externi odkazy

[Uvod](http://www.abclinuxu.cz/clanky/navody/oracle-1-uvod-distribuce-oraclexe) na abc linuxu  
[Rychlejsi aplikace](http://www.dbsvet.cz/view.php?cisloclanku=2008112101) na db svete  
[Oracle Database Performance Tuning Guide](http://download.oracle.com/docs/cd/B19306_01/server.102/b14211/toc.htm)  

[Oracle Database Backup and Recovery Basics](http://download.oracle.com/docs/cd/B19306_01/backup.102/b14192.pdf)  
[Oracle Database Backup and Recovery Advanced User's Guide](http://download.oracle.com/docs/cd/B19306_01/backup.102/b14191/toc.htm)  
[SQL*Plus User's Guide and Reference](http://download.oracle.com/docs/cd/B10500_01/server.920/a90842/toc.htm)  
[Oracle Database Security Guide](http://download.oracle.com/docs/cd/B19306_01/network.102/b14266.pdf)  
[Oracle Database Concepts](http://download.oracle.com/docs/cd/B19306_01/server.102/b14220.pdf)  
[Oracle Database Performance Tuning Guide](http://download.oracle.com/docs/cd/B19306_01/server.102/b14211/toc.htm)  
[Oracle 2 Day DBA](http://www.stanford.edu/dept/itss/docs/oracle/10g/server.101/b10742.pdf)  
[Oracle Database Utilities](http://www.stanford.edu/dept/itss/docs/oracle/10g/server.101/b10825.pdf)  
[Oracle Real Application Clusters Installation and Configuration](http://download.oracle.com/docs/html/B10766_08/toc.htm)  

[Oracle Database Upgrade Guide](http://www.oracle.com/pls/db102/homepage)  
[Oracle Database Globalization Support Guide](http://download.oracle.com/docs/cd/B19306_01/server.102/b14225/toc.htm)  
[Pekny strucny navod na Oracle vcetne RMANu](http://www.cuddletech.com/articles/oracle/node1.html)  
[Obrazek](http://a5.sphotos.ak.fbcdn.net/hphotos-ak-snc3/11039_104638359549190_100000090807855_123129_1238581_n.jpg) - jak hezke mohou byt sql dotazy  

### Oracle soucasti a ovladani Oracle

Oracle Enterprise Manager - webova aplikace na management Oracle databazi v prostredi

#### I/SQL*Lnstalace

rpm -i oracle-xe-10.2.0.1-1.0.i386.rpm  
service oracle-xe configure  
touch /home/oracle/.profile  
chown oracle:oracle /home/oracle/.profile  
echo PATH=$PATH:/usr/lib/oracle/xe/app/oracle/product/10.2.0/server/bin >> /home/oracle/.profile ... prida binarky do cesty  
echo export ORACLE_HOME=/usr/lib/oracle/xe/app/oracle/product/10.2.0/server >> /home/oracle/.profile  
echo export ORACLE_SID=XE >> /home/oracle/.profile ... sdeli Oracle, se kterou databazi budu pracovat  
alias sqlplus="[rlwrap](http://freshmeat.net/projects/rlwrap/) sqlplus ... historie prikazu v sqlplus  

su - oracle  
sqlplus / AS SYSDBA  
nebo [http://127.0.0.1:8080/apex](http://127.0.0.1:8080/apex)  
opatch lsinventory ... vypise vsechny nainstalovane soucasti  
[opatch apply](https://taliphakanozturken.wordpress.com/tag/opatch-lsinventory/) ... aplikace pathcu  

### Stop/start/status

Start:  
su - oracle  
. oraenv  
sqlplus / as sysdba; startup;  .... (nebo startup nomount) (spusti se mimo jine smon)  
sqlplus / as sysdba; tartup pfile=/opt/oracle/product/11.2.0/dbhome_BI/dbs/initorcl.ora ... spusti se Ora s jinym specifikacnim souborem  
lsnrctl start ... start listeneru  
lsnrctl status LISTENER_ABC ... stav listeneru (portu  

Status:  
ps -ef | grep smon  
ps -ef | grep tns ... zda jede listener  
lsnrctl status  
tnsping orcl ... ping na instanci orcl  

Stop:  
sqlplus / as sysdba; shutown immediate;  
lsnrctl stop ... stop listeneru  

### Konfigurace

cat /etc/oratab ... SIDy, cesty atd.  
env | grep ORA ... ukaze informace z promennych s jakou instanci pracuji>br>
$ORACLE_HOME/dbs/spfileorcl.ora ... defaultnni specifikacni soubor pro instanci  
sqlplus / as sysdba; create spfile from pfile; ... vytvori se defaultni specificky soubor z aktualniho  
$ORACLE_HOME/network/admin/listener.ora<BR>
$ORACLE_HOME/network/admin/tnsnames.ora  

#### Nastroje

Database Configuration Assistant - DBCA - soucasti OUI, nebo pristupny pomoci GUI  
Oracle Universal Installer - OUI  
Oracle Application Express ... posloucha defaultne na http portu 8080  

AWR - Automatic Workload REpository ... monitoruje vykon a hlasi udalosti  
SQL*plus ... dotazovy interfejs SQL  
iSQL*plus ... Webova verze SQL*plus ... dotazoveho interfejsu. Spouzti se na adrese http://localhost:5560/isqlplus  
[YaSQL](http://sourceforge.net/projects/yasql/) ... Yet Another SQL*Plus - SQLPlus s historii a ovladanim vystupu pri dlouhych vypisech  
netvgr ... Oracle Net Manager - konfigurace Oracle, jak Oracle Enterprise Manager  
DMBS_SERVER_ALERT ... PL/SQL balicek pro spravu alertu systemovych udalosti  
DBMS_SESSIO, SBMD_MONITOR ... kontrolovani SQL tracovani  

#### Systemove procesy

[https://docs.oracle.com/cloud/latest/db112/CNCPT/process.htm#CNCPT9840](https://docs.oracle.com/cloud/latest/db112/CNCPT/process.htm#CNCPT9840)  

ps -ef | grep smon ... ([System MONitor](http://www.orafaq.com/wiki/SMON)) - proces na pozadi - se spousti pro kazdou instanci. Parametr - bezici instance. SMON provadi Recovery, cleaning and stara se o extendy  
ora_mman_INSTANCE ... ([Memory MANager](http://www.orafaq.com/wiki/MMAN)) - proces instance na pozadi, ktery se stara o zmeny velikosti SGA pameti  
ora_dbw?_INSTANCE ... ([DataBase Writer](http://www.orafaq.com/wiki/DBWR)) - proces instance na pozadi, ktery zapisuje z SGA pameti do DB souboru  
ora_pmon_INSTANCE ... ([Process MONitor](http://www.orafaq.com/wiki/PMON)) - proces instance na pozadi, ktery se stara o procesy  

ora_arc?_INSTANCE ... (ARChiver) - proces instance na pozadi, ktery kopiruje logy z REDO do ARCHIVE  
ora_lgwr_INSTANCE ... ([LoG WRiter](http://www.orafaq.com/wiki/LGWR)) - proces instance na pozadi, ktery zapisuje logy do Redologu  
ora_reco_INSTANCE ... ([Recovery ORAcle Process](http://www.orafaq.com/wiki/RECO)) - proces instance na pozadi, ktery resi konfliktni dotazy  
ora_mmnl_INSTANCE ... ([MMoN Lite](http://www.orafaq.com/wiki/MMNL)) - proces instance na pozadi, ktery pomaha MMON procesu zapisovat ASH Buffer do AWE tabulek  
ora_ckpt_INSTANCE ... ([Oracle Checkpoint Process](http://www.orafaq.com/wiki/CKPT)) - proces instance na pozadi, ktery dava casove snamky do vsech tadafiles a kontrolnich souboru  

SELECT SID,SERIAL#,STATUS,PROCESS,PROGRAM FROM V$SESSION; ... seznam procesu, PID a SID  
SELECT SID,SERIAL#,STATUS FROM V$SESSION WHERE USERNAME='JWARD'; ... ukaze vsechny procesy uzivatele JWARD;
SELECT * from V$PROCESS; ... seznam systemovych procesu  
SELECT * from V$SESS_IO; ... seznam I/O statistik jednotlivych procesu  
select * from V$SESSION_LONGOPS; ... seznam parametru procesu, jez jedou dele jak 6 sekund  
SELECT * from V$SESSION_WAIT; ... seznam prostredku, ci udalosti, na ktere cekaji aktivni sessions  
SELECT * from V$SYSSTAT; ... statistika systemovych udalosti  
SELECT * from V$RESOURCE_LIMIT ... seznam omezeni zdroju  
alter system kill session '21,5' ... zabije uzivetalsy proces 'SID,SERIAL#' = '21,5';  
Listener ... http://localhost:1520/mydb  

lsnrctl start/stop/status ... Listener  
tnsping localhost ... test listeneru  
isqlplusctl start/stop/status ... iSQL*plus  
database listener ... posloucha defaultne na portu 1521  
dbconsole ... Oracle Manager Console na adrese http://localhost:5500/em  
$ORACLE_HOME/bin/emctl start dbconsole  
$ORACLE_HOME/bin/emctl stop dbconsole  
$ORACLE_HOME/bin/emctl status dbconsole  

#### konfiruracni soubory Oracle

$ORACLE_HOME/network/admin/listener.ora ... konfigurace listeneru  
$ORACLE_HOME/network/admin/tsnames.ora ... konfigurace klientu pro listener  
/etc/oratab (/var/opt/oracle/oratadb) ... konfigurace instanci, obsahuje ORACLE_HOME a ORACLE_SID  
[init.ora](http://www.adp-gmbh.ch/ora/misc/init_params.html) ... inicializacni parametry  
$ORA_TZFILE=$ORACLE_HOME/oracore/zoneinfo/timezone.dat ... soubor s definicema zon. Vetsi soubor je timezlgr.dat, Pouziti ma vliv na vykon Oracle  
$ORACLE_HOME/network/admin/listener.ora ... soubor s nastavenim listeneru  

SELECT * FROM PRODUCT_COMPONENT_VERSION; ... ukaze verze vsech komponent  
SELECT * FROM V$VERSION ... Ukaze verze Oracle  

#### soubory/adresare

#### logy a alerty

SELECT
[udump](http://www.orafaq.com/wiki/UDUMP) ... user dump - trace soubory a logy k uzivatelskym jobum - chyby  
bdump ... background dump - trace soubory a logy k jobum na pozadi - chyby  

cdump ... core dump - trace soubory a logy k zakladnim jobum - chyby  
select * from V$LOGFILE; ... ukaze aktivni LOG soubory  
select METRICS_NAME,WARNING_VALUE,CRITICAL_VALUE from DBA_THRESHOLDS; ... Alerty, treba na threshold mista v tablespaces  
select OBJECT_NAME,MESSAGE_TYPE,METRIC_VALUE,CREATION_TIME from DBA_ALERT_HISTORY; ... historie alertu  
select * from V$ALERT_TYPES; ... typy alertu  
desc DBA_OUTSTANDING_ALERTS; ... dalsi tabulka s alerty  
desc V$METRICNAME; ... jmena metrik
desc V$METRIC; Metriky  
desc V$METRIC_HISTORY;  
BACKGROUND_DUMP_DEST ... nastaveni dumpu pro bdump  

USER_DUMP_DEST ... nastaveni udump  
MAX_DUMP_FILE_SIZE ... nastaveni max. velikosti pro dump  
SQL_TRACE = TRUE ... inicialsizacni parametr pro tracovani dumpu  
ALTR SESSION SET SQL_TRACE TRUE; ... zmeneni tracovani za behu  
trcsess ... program Oracle (spousti se z shellu) na cteni trejsu dumpu  

#### SQL Plus - pristup do Oracle

sqlplus username/password AS SYSDBA ... spusti sqlplus a pripoji se pod uzivatelem username jako uzivatel SYSDBA  

sqlplus / AS SYSOPER ... spusti sqlplus a pripoji se pod aktualnim uzivatelem jako uzivatel SYSOPER  
sqlplus /NOLOG ... spusti SQLPlus a nepripojuje se do instance  
desc V$SESSION ... ukaze popisy promennych tabulky (nahledu)  
[column](http://download.oracle.com/docs/cd/B19306_01/server.102/b14357/ch12013.htm) name format a10 ... format promenne NAME pri vypisu bude 10 znaku  
column id format 9; ... nastavi format sloupce id na cislo  

#### Pripojeni k databazi

CONNECT user/passwd ... pripojeni uzivatele user s heslem password  

CONNECT oracle/oracle AS SYSDBA ... pripoji uzivatele oracle s pravy uzivatele SYS (administrator)  
CONNECT oracle/oracle AS SYSOPER ... pripoji uzivatele oracle s pravy na prece s tabulkama  
CONNECT / ... pripoji se pod aktualnim systemovym uzivatelem  
CONNECT /@net_service ... pripoji  se na vzdalenou databazi net_service  
/D

#### Instance - proces Oracle, ktery se muze pripoji k nejake databazi a pracuje nad ni

STARTUP ... startovani instance, hleda SPFILE v  $ORACLE_HOME/dbs  
STARTUP PFILE= /mydb/pfile.ora ... spusti instanci s inicializacnimi parametry z /mydb/pfile.ora  
STARTUP NOMOUNT ... nastartuje instanci, nenamountuje databaze  

STARTUP MOUNT ... nastartuje instanci, namountuje databazi, ale neotevre  
STARTUP RESTRICT ... nastartuje instanci, mountuje a otevre databazi, ale omezi pripojovani jen na uzivatele s "RESTRICTED SESSION"  
STARTUP FORCE ... nejdriv provede SHUTDOWN ABORT, pote nastartuje instanci  
STARTUP OPEN RECOVVERY ... otevre instanci a zahaji recovery  
ALTER DATABASE MOUNT ... namountuje nenamountovanou databazi  
ALTER DATABASE OPEN ... otevre namountovanou databazi  
ALTER DATABASE OPEN READ ONLY ... otevre namountovanou databazi jen pro cteni  
ALTER DATABASE CLOSE ... zavre namountovanou databazi  
ALTER SYSTEM DISABLE RESTRICTED SESSION; ... vypne omezene pripojovani  

ALTER SYSTEM ENABLE RESTRICTED SESSION; ... zapne omezene pripojovani  
SHUTDOWN = SHUTDOWN NORMAL ... stopovani instance, pocka, az ulohy skonci  
SHUTDOWN IMMEDIATE ... stopovani instance  
STHUDOWN TRANSACTIONAL  
SHUTDOWN ABORT  
select host_name,instance_name from v$instance; ... ukaze bezici instance  
ALTER SESSION DISABLE PARALLEL DML; ... zakaze paralelni vykonavani SQL prikazu INSERT, UPDATE, DELETE  
ALTER SESSION ENABLE PARALLEL DDL; ... povoli paralelni vykonavani SQL prikazu CREATE, ALTER  
ALTER SESSION ENABLE FORCE PARALLEL QUERY PARALLEL 5; ... prikaze paralelni vykonavani SQL prikazu QUERY se stupne paralelismu 5  

#### Pamet SGA (System Global Area)

ALTER SYSTEM SGA_MAX_SIZE ... meneni max. velikosti SGA pameti  
SELECT SUM(value) FROM V$SGA; ... celkova velikost jednotlivych slozek SGA pameti  
SELECT * FROM V$SGA; ... vypis jednotlivych slozek pameti  
SELECT * FROM V$SGAINFO; ... podrobnejsi vypis jednotlivych slozek pameti  
SELECT * FROM V$SGASTAT; ... dlouhe statistiky o pameti SGA  
SELECT * FROM V$SGA_DYNAMIC_COMPONENTS; ... Ukaze informace o jednotlivych slozkach dynamickych SGA komponentach  
SELECT * FROM V$SGA_DYNAMIC_FREE_MEMORY; ... aktualni mnoztsvi volne pameti, ktera je k dispozici k dynamickym operacim  

SELECT * FROM V$SGA_RESIZE_OPS; ... ukaze poslednich 400 dynamickych zmen pameti  
SELECT * FROM V$SGA_CURRENT_RESIZE_OPS; ... ukaze probihajici dynamicke zmeny pameti  

#### Spousteni SQL, PL/SQL skriptu a shell prikazu

[[[http://download-west.oracle.com/docs/cd/B12037_01/appdev.101/b10807/toc.htm]([[http///download-west.oracle.com/docs/cd/B12037_01/appdev.101/b10807/toc.htm)

@/u01/oracle/rdbms/admin/catalog.sql ... pusti davku SQL prikazu  
!ls ... spusti prikaz ls z shellu  

#### Sluzby

Interni sluzby: SYS$BACKGROUND, SYS$USERS  
DBA_SERVICES  
SELECT * FROM ALL_SERVICES; ... ALL_SERVICES = V$SERVICES  
V$ACTIVE_SERVICES  
V$SERVICE_STATS  
V$SERVICE_EVENTS  
V$SERVICE_WAIT_CLASSES  
V$SERV_MOD_ACT_STATS  
V$SERVICE_METRICS  

V$SERVICE_METRICS_HISTORY  

V$SESSION  
V$ACTIVE_SESSION_HISTORY  
DBA_RSRC_GROUP_MAPPINGS  
DBA_SCHEDULLER_JOB_CLASSES  
DBA_TRESHOLDS  
SELECT * FORM [DBA_SERVICES,ALL_SERVICES=V$SERVICES,V$ACTIVE_SERVICES,V$SERVICE_STATS,V$SERVICE_EVENTS,V$SERVICE_WAIT_CLEASSES,V$SERV_MOD_ACT_STATS,V$SERVICE_METRICS,V$SERVICE_METRIC_HISTORY,V$SESSION,V$ACTIVE_SESSION_HISTORY,DBA_RSRC_GROUP_MAPPINGS,DBA_CHEDULER_JOB_CLASSES,DBA_THRESHOLDS] ... vypisy sluzeb  

### DATABAZE

#### Databaze

Mozno pouzit DCA - Database Configuration Assistant  
ALTER DATABASE DEFAULT TEMPORARY TABLESPACE tempts2 ... vytvori ci zmeni docasnou tablespace na tempts2. Tato ts musi byt jiz vytoverna  
ALTER DATABASE SET DEFAULT BIGFILE TABLESPACE ... Dynamicky zmeni velikost TS na BIGFILE  
ALTER SYSTEM GLOBAL_NAME ... zmeneni jmena a domeny databaze. Musi se pak vypnout DB, predelat kontrolni soubor a znovu spostit  
Vytvori Databazi vcetne Control File:\\

```
CREATE DATABASE mydb
  USER SYS IDENTIFIED by heslo1
  USER SYSTEM IDENTIFIED BY heslo2
  LOGFILE GROUP 1 ('/mydb/redo01.log') SIZE 100M,
    GROUP 2 ('/mydb/redo02.log') SIZE 100M,
    GROUP 3 ('/mydb/redo03.log') SIZE 100M
    MAXLOGFILES 5
    MAXLOGMEMGERS 5
    MAXLOGHISTORY 1
    MAXDATAFILES 100
    MAXINSTANCES 1
    CHARACTER SER US7ASCII
    NATIONAL CHARACTER SET AL16UTF16
    DATAFILE '/mydb/system01.dbf' SIZE 325M REUSE
    ENTENT MANAGEMENT LOCAL
    SYSAUX DATAFILE '/mydb/sysaux01.dbf'
    DEFAULT TABLESPACE tbs_1
    DEFAULT TEMPORARY TABLESPACE temts1
      TEMPFILE '/mydb/temp01.dbf'
      SIZE 20M REUSE
    UNDO TABLESPACE undotbs
      DATAFILE '/mydb/undotbs01.dbf'
      SIZE 20M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED;
```


##### Jednodussi vytvoreni DB

CREATE DATABASE mydb2; ... Vytvori databazi mydb2, s TS: SYSTEM, SYSAUX v DB_CREATE_FILE_DEST a REDO + Control files tolikrat, kolik je definovano DB_CREATE_ONLINE_DEST_n v tet olokaci. Vse velikost 100MB. Pokud je UNDO_MANAGEMENT povolen, vytvori se i UNDO TS o velikosti 10MB.  
DROP DATABASE; ... smazani databaze vcetne datafile, redologs souboru, control files a souboru s inicializacnimi parametry  
SELECT PROPERTY_VALUE FROM DATABASE_PROPERTIES WHERE PROPERTY_NAME = 'DEFAULT_TBS_TYPE';
SELECT NAME,DBID,OPEN_MODE,LOG_MODE FROM V$DATABASE; ... seznam databazi  
SELECT * from V$DATABSE; ... zakladni parametry k databazim  
SELECT * FROM GLOBAL_NAME ... ukaze jmeno databaze  
select NAME from V$DATAFILE; ... seznam datovych souboru  

##### Parametry pro CREATE DATABASE

RESETLOGS ... Oracle vytvori sam soubory pro REDO  
NORESETLOGS ... REDO soubory se musi specifikovat pri vytvareni DB pomoci klicoveho slova LOGFILE  

Vytvoreni kontrolniho souboru (napriklad pri poskozeni. Vytvori se kontrolni soubor uvedeni v PF dane databaze):\\

```
CREATE CONTROLFILE
SET DATABASE prod
LOGFILE GROUP 1 ('/ora/redo1-1.dbf', /ora/redo1-2.dbf),
GROUP 2 ('/ora/redo2-1.dbf', /ora/redo2-2.dbf)
RESETLOGS
DATAFILE '/ora/system.dbf' SIZE 3M, '/ora/users.dbf' SIZE 5M
MAXLOGFILES 50
MAXLOGMEMBERS 3
MAXLOGHISTORY 4000
MAXDAAFILES 200
MAXINSTANCES 6
ARCHIVELOG;
```

ALTER DATABASE BACKUP CONTROLFILE to '/ora/control.bkp'; ... vytvori zaloho kontrolniho souboru  
ALTER DATABASE BACKUP CONTROLFILE to TRACE; ... vytvori sekvenci SQL prikazu, ktera dokaze vytvorit soucasny kontrolni soubor  
alter dadatabase datafile '/oracle/FIN02/system/system02.dbf' resize 1000M; ... zmeni velikost datoveho souboru  
SELECT * FROM V$CONTROLFILE; ... seznam kontrolnich souboru\\  
select VALUE from V$PARAMETER where name = 'control_files'; ... ukaze nazev kontrolniho souboru pro Databazi  

#### SPF - Server Parameter File, PF a IPF - Initialisation PF

Binarni soubor s inicializacnimi parametry pro instanci, ktery se spusti automaticky pro STARTUP a nachazi se na strane serveru. Pokud neexistuje, musi se pri startu instance uvest nazev textoveho spuboru PFILE (parametr file), ktery muze byt na strane klienta, ne serveru. Pokud neni v defaultnim umisteni, musi se definovat SPFILE pred spustenim instance.  
CREATE SPFILE='/oracle/dbs/spfilemydb.ora' FROM PFILE='[/oracle/admin/initmydb/scripts/init.ora](init.ora.html)'; SHUTDOWN; EXIT ... Vytvori SPF, pri pristim startu se pouzije DPF  
CREATE SPFILE FROM PFILE=/oracle/admin/initmydb/scripts/init.ora; SHUTDOWN; EXIT ... vytvori standartni SPFILE (spfile$ORACLE_SID.ora)  
CREATE PFILE='/tmp/pfile.ora' FROM SPFILE; ... vyexporuje aktivni SPF do textoveho PFILE  
ALTER SESSION ... meni parametry pri aktualni session (napriklad DB_CREATE_*)  
ALTER SYSTEM ... meni parametry  
ALTER SYSTEM SCOPE=SPFILE ... zmeni parametry v SPFILE  
ALTER SYSTEM SET JOB_QUEUE_PROCESSES=50 COMMENT='temporary change 13/12/2010' SCOPE=MEMORY ... zmeni max. pocet frontovych procesu, SCOPE muze byt MEMORY,SPFILE,BOTH a nastavuje, kde se provede zmena  

ALTER SYSTEM SET LOG_ARCHIVE_DEST_4='LOCATION=/u02/oracle/rbdb1/'MANDATORY,'REOPEN=2' SCOPE=SPFILE ... specifikuje, kam se bude ukladat archiv logu c. 4  
%%ALTER SYSTEM SET LOG_ARCHIVE_DEST_$=''%% ... smazani parametru  
ALTER SYSTEM SET DB_BLOCK_CHECKSUM TRUE; ... dybamicky prepne prepinac  
SHOW PARAMETERS ... ukaze aktualni parametry  
SELECT * FROM V$PARAMETER ... ukaze aktualni parametry  
SELECT * FROM V$PARAMETER2 ... ukaze aktualni parametry, parametry v radcich  
SHOW PARAMETERS SPFILE; ... ukaze lokaci SPF, ktery se uziva  
SELECT * FROM V$SPPARAMETER; ... ukaze parametry SPF, ktery se uziva  

#### Parametry pro inicializacni soubory - PF (Parameter File)

SGA_MAX_SIZE ... maximalni velikost SGA pameti  
PROCESSES = 60 ... maximalni pocet soucasne spustenych procesu Oracle k instanci v OS  
UNDO_MANAGEMENT AUTO ... nastaveni undo politiky. Volby AUTO, nebo MANUAL  
COMPATIBLE = 9.2.0.2 ... nastaveni compatability souboru a zapnuti/vypnuti novych vlastnosti  
LICENCE_MAX_USERS = 200 ... nastaveni max. poctu uzivatelu  
LICENCE_MAX_SESSIONS = 1000 ... V Oracle mensi nez 10, omezeni poctu spojeni  
DB_CREATE_FILE_DEST ... Oracle bude sam managovat data soubory  
DB_ONLINE_LOG_DEST_3 ... Oracle bude sam managovat 3 redo logy?  

DB_FILES 100 ... Pocet souboru jez se alokuje v SGA pro datove soubory  
DB_CHECK_SUM TRUE ... Automaticky testuje Checksum datafiles. Pomalejsi, ale odhali chyby  
DB_RECOVERY_FILE_DEST_SIZE ... Velikost mista, jez muze Oracle vyuzit na Flash recovery area  
DB_CREATE_FILE_DEST='/a1'; ... Vychozi adresar, kam Oracle pri operaci CREATE bude vytvaret datove soubory a docasne soubory, pokud neni zadana cesta/soubor. Pokud neni definovano DB_CREATE_ONLINE_LOG_DEST_n, pak i pro REDO logy a kontrolni soubory.  
DB_CREATE_ONLINE_LOG_DEST_n = '/a2'; ... Vychozi adresar, kam se ukladaji REDO logy a kontrolni soubory (control files) pri operaci CREATE, pokud neni zadan adresar/soubor. n muze byt 1-5  
DB_RECOVERY_FILE_DEST = '/a3' ... Adresar, kam bude Oracle defaultne ukladat RMAN zalohy, flashback logy, a archivy se nezada adresar/jmeno souboru. Pokud neni nadefinovano DB_CREATE_ONLINE_LOG_DEST_N, pak take REDO logy a ovladaci soubory (control files)  
DB_RECOVERY_FILE_DEST ... Oblast (adresar), kde bude Oracle pouzivat, vytvaret a managovat soubory k zaloham a obdove (REDO TS, ...) - Flash recovery area. Musi byt nejdrive nadefinovana velikost  
LOG_ARCHIVE_DEST_n ... Oblast pro ARCHIVy, nesmi myt nastaveno zaroven DB_RECOVERY_FILE_DEST, nebo LOR_ARCHIVE_DEST_n musi byt rovno 'LOCATION=USE_DB_RECOVERY_FILE_DEST'  
LOG_ARCHIVE_DUPLEX_SET ... Oblast pro mirrorovane ARCHIVy, nesmi myt nastaveno zaroven DB_RECOVERY_FILE_DEST  

ARCHIVE_DEST_n  
DISPATCHERS="(ADDRESS=(PROTOCOL=TCP)(HOST=144.25.16.201)(PORT=5000))(DISPATCHERS=2)" ... Konfigurace 2 dispeceru, kteri poslouchaji TCP na addr. 144.25.16.201 na portu 5000  
UNDO_TABLESPACE=undotbs_01 ... Undo tabulkovy prostor - pokud neexistuje, UNDO_MANAGEMENT se nespusti. Dynamicky paramert, pouziva se, kdyz je vice undo TS  
UNDO_RETENTION=1800 ... Minimalni cas, po ktery se ukladaji data do undo tabulkoveho prostoru pri vykonavani prikazu, 900 vychozi hodnota. Dynamicky parametr  

#### Parametry DB

USER SYS IDENTIFIED be heslo1 ... zabezpeceni uzivatele heslem heslo1  
DATAFILE ... Definovani parametru, ci datafile pro SYSTEM TS, pokud neni uvedeno, Oracle vytvori a managuje soubor + TS sam  
EXTEND MANAGEMENT LOCAL ... lokalne manazovany teblespace SYSTEM, kdyz neni EXTENS MANAGEMENT LOCAL pri vytvareni DB, Oracle vytvori defaultne "slovnikove-managovany" SYSTEM tablespace. Pokud se zada, nejde konvertovat zpet na dictionary-managed tablespace  

LOGFILE ... Definovani parametru, ci datafile pro REDO TS, pokud neni uvedeno, Oracle vytvori a managuje 2 REDO TS a soubory sam  
(SMALLFILE|BIGFILE) DEFAULT TEMPORARY TABLESPACE ... Defaultni tablespace pro docasne operace. Neni-li zadano, uzivatele, kteri nemaji specifikovano jinak, pouzivaji SYSTEM tablespace - nedoporucije se. Pokud se pouzije Local Management, DEFAULT TEMPORARY TS se musi nadefinovat. Pokud Localy managed, pak default ts busi byt taky lokalne manazovana. Pokud se nezada TEMPFILE, system vytvori soubor sam.  
(SMALLFILE|BIGFILE) UNDO TABLESPACE ... Definovani parametru, ci datafile pro undo tablespace (undo management). Nezada-li se pri vytvareni DB pod jmenem SYS_UNDOTBS a ne ni-li specifikovan DATAFILE, system vytvori soubor sam. Neni li UNDO definovana, zaznamenavaji se akce do SYSTEM TS  
SYSAUX TABLESPACE ... Definovani parametru, ci datafile pro  SYSAUX tablespace. Neni-li definovana pri vytvareni DB, Oracle vytvori TS a soubor automaicky sam  
DEFAULT TABLESPACE ... Defaultni tablespace pro nesystemove uzivatele, kteri nemaji specificky nastavene tablespace. Pokud se nenastavi, pouzivati tablespace SYSTEM - nedoporucuje se  
CONTROL_FILES ... Definovanikontrolnich souboru pro databazi. Neni-li specifikovano, oracle  vytvori sam  
SET DEFAULT BIGFILE DATABASE ... Nastavi velikost TS na big - kazdy soubor muze mit az 4G bloku, oproti 4M pri small  
SET TIME_ZONE ... nastavi casovou zonu. Pokud se nenastavi, pouzije se defaultni. Casova zona jde zmenit ALTER SESSION. Definice zon jsou v soubory $ORA_TZFILE  
  SELECT * FROM V$TIMEZONE_NAMES ... seznam casovych zon  

NOLOGGING ... donuti databazi nelogovat nejake cinnosti do REDO  
(NO) FORCE LOGGING ...
NOARCHIVELOG ... nepouziva se archiv  
MAXLOGFILES 5 ... Maximalni pocet redologu  
MAXLOGMEMBERS 5 ... Maximalni pocet clenu v REDO LOG skupine  
MAXLOGHISTORY 1 ...  
MAXDATAFILES 100 ... maximalni pocet datovych souboru  
MAXINSTANCES 1 ... maximalni pocet instanci, ktere se daji spoustit nad databazi  
DB_BLOCK_SIZE 4096 ... velikost bloku 4096b pro SYSTEM TS. Pouziva se i jako vychozi nastaveni pro ostatni TS  
READ_ONLY_OPEN_DELAYED=TRUE ... pri otevirani databaze necte read only datove soubory, jen kdyz jsou potreba  

/

#### Tablespace - Tabulkove prostory

[http://aov.webzdarma.cz/oracle/tablespaces.html](http://aov.webzdarma.cz/oracle/tablespaces.html)  

Tabulky maji ulozene data v tabulkovych prostorech (Tablespace - TS - TBS) v datovych segmentech. Datovy segment je mnozina extentu (rozsahu), ktere mohou byt v roznych datovych souborech na ruznych mistech. Datovy extent je souvisly usek datovych bloku.
Pokud se pri tvoreni TS nezada jmeno souboru vcetne cesty, Oracle vytvori sam datovy soubor v adresari definovanem v jedne z promennych DB_CREATE_FILE_DEST, DB_CREATE_ONLINE_LOG_DEST_n, DB_RECOVERY_FILE_DEST. Soubory jsou pak ukladany napriklad do DB_CREATE_FILE_DEST/DB_UNIQUE_NAME/datafile/o1_mf_tbs1_1ixd90q.dbf.

alter system set DB_CREATE_FILE_DEST='/a1'; ... Vychozi adresar, kam Oracle pri operaci CREATE bude vytvaret datove soubory a docasne soubory, pokud neni zadana cesta/soubor. Pokud neni definovano DB_CREATE_ONLINE_LOG_DEST_n, pak i pro REDO logy a kontrolni soubory.  
alter system set DB_CREATE_ONLINE_LOG_DEST_n = '/a2'; ... Vychozi adresar, kam se ukladaji REDO logy a kontrolni soubory (control files) pri operaci CREATE, pokud neni zadan adresar/soubor. n muze byt 1-5  
alter system set DB_RECOVERY_FILE_DEST = '/a3'; ... Adresar, kam bude Oracle defaultne ukladat RMAN zalohy, flashback logy, a archivy se nezada adresar/jmeno souboru. Pokud neni nadefinovano DB_CREATE_ONLINE_LOG_DEST_N, pak take REDO logy a ovladaci soubory (control files)  
alter session set DB_RECOVERY_FILE_DEST = '/a3'; ... Dalsi moznost zmeny parametru  
CREATE TABLESPACE users; ... Vytvori tabulkovy prostor 'users'. Datovy soubor bude vytvoren automaticky  
create tablespace users SIZE 25M REUSE AUTOEXTEND on NEXT 1280K MAXSIZE UNLIMITED; ... vytvori tabuklovy prostor o velikosti 20 MB, ktery se v pripade potreby rozsiri vzdy o 128 KB. Maximalni velikost neni stanovena  

create tablespace tblspc DATAFILE '/oradata/tblspc.dbf'; ... Vytvori se tabulkovy prostor a vytvori se pro nej datovy soubor, jezs nesmi exisatovat  
create tablespace tblspc datafile '/oradata/tblspc.dbf' REUSE; ... Vytvori tabulkovy prostor a pouzije zadany soubor, i kdyz uz existuje  
create tablespace tblspc size 500K EXTENT MANAGEMENT LOCAL AUTOALOCATE; ... vytvori lokalne spravovany tablespace, jez pri rozsireni bude automaticky urcena velikost "extentu". Pouziva se, kdyz je v tablespace mnoho objektu ruznych velikost - VYCHOZI nastaveni, kdyz neni uveden MANAGEMENT tablespace, nebo kdyz neni nastavena metoda AUTO, ci manual. Lokalne spravovane extenty maji data o extentech ulozeny v bitmape primo v tablespace.  
create tablespace tblspc size 50M EXTENT MANAGEMENT LOCAL UNIFORM SIZE 128K; ... vytvori lokalne spravovan tabulkovy prostor, jez pri rozsireni bude rozsirena extenty o fixni velikosti 128kB  
create tablespace tblspc SEGMENT SPACE MANAGEMENT MANUAL; ... Vytvori takbulkovy prostor, kde se volne misto v segmentech spravuje manualne. VYCHOZI nastaveni, vyzaduje nastaveni parametru PCTUSED, FREELISTS a FREELIST GROUPS pro schema objektu  
create tablespace tblspc SEGMENT SPACE MANAGEMENT AUTO; ... Vytvori takbulkovy prostor, kde se volne misto v segmentech spravuje automaticky. Nevyzaduje nastavovani dalsich parametru  
create tablespace tblspc TABLESPACE GROUP tblgroup1; ... vytvori tabulkovy prostor a prida jej do skupiny tabulkovych prostoru tblgroup1  
create tablespace tblspc DB_BLOCK_SIZE 8K; ... vytvori tabulkovy prostor a nastavi velikost Bloku jinaci, nez vychozi  
create tablespace tblspc LOGGING ... Vytvori tabulkovy prostor a zapne logovani do REDO Logu (vychozi hodnota, neni-li uvedeno vubec)  

create tablespace tblspc FORCE LOGGING ... Vytvori tablespace a vynuti logovani vsech operaci. Hodi s v pripade STANDBY databazi  
create tablespace tblspc NOLOGGING ... Vytvori tabulkovy prostor a zakaze logovani do REDO Logu  
create tablespace dctspc size 50M EXTENT MANAGEMENT DICTIONARY DEFAULT STORAGE (INITIAL 50K NEXT 50K MINEXTENTS 2 MAXEXTENTS 50 PCTINCREASE 0); ... Vytvori tablespace se slovnikove spravovanymi extenty. DEFAULT STORAGE je nastaveni segmentu, initial je velikost prvniho extentu, NEXT je velikost dalsiho extentu, MINEXTENTS je min. pocet extentu, MAXEXTENTS je max. p. extentu, PCTINCREASE ke procentualni narust velikosti kazdeho dalsiho extentu  
create BIGFILE tablespace bigspc; ... Vytvori tabulkovy prostor s jednim souborem typu BIG, ktery muze dosahovat obrovskych velkosti (desitky TB). Je typu automaticky EXTEND MANAGEMENT LOCAL a SEGMENT SPACE MANAGEMENT AUTO a nemuze byt jinak  
CREATE TEMPORARY TABLESPACE tmpspc; .. vyvori (dalsi) docasny tablespace, ktery slouzi pro uchovani docasnych dat napriklad pri SORT funkci. data zanikaji s session.  
create bigfile temporary tablespcave bigtmpspc; ... vytvori docasny tabulkovy prostor s parametrem BIGFILE  
create temporary tablespace tmpspct TEMPFILE '/u2/data/tmpspc.dbf' REUSE; ...Vytvori tablespace pro docasna data, specifikuje se datovy soubor. Soubor se prepise, kdyz existuje.  
create temporary tablespace tmpspct SIZE 20M EXTENT MANAGEMENT LOCAL UNIFORM SIZE 16MB; ... vytvori se docasny tabulkovy prostor o danych parametrech (autoallocate nemuze byt pouzito u temptablespce)  
create temporary tablespace tmpspc TABLESPACE GROUP tmpgroup1; ... vytvori docasny tabulkovy prostor a zaroven ji prirazi do tablespace skupiny  

ALTER TABLESPACE tblspc ADD DATAFILE '/u2/data/tblspc2.dbf' SIZE 100M; ... Zmeni tabulkovy prostor tblspc tak, ze prida datovy soubor o velikosti 100MB  
alter tablespace tblspc TEMPORARY; ... zmeni tabulkovy prostor na docasny tabulkovy prostor  
alter tablespace tblspc TABLESPACE GROUP tblgroup1; ... prida tabulkovy prostor do skupiny tabulkovych prostoru  
%%alter tablespace tblspc TABLESPACE GROUP ''%%; ... odebere tabulkovy prostor ze skupiny tabulkovych prostoru  
alter tablespace tblspc RENAME TO users; ... prejmenuje tabulkovy prostor (COMPACTIBLE parametr musi byt &gt;= 10  
alter tablespace tblspc RENAME DATAFILE '/u1/1.dbf' '/u1/2.dbf' TO '/u2/1.dbf' '/u2/2.dbf'; ... prejmenuje Datove soubory v definicich, po te, co jsou fyzicky prejmenovane<. Musi byt v OFFLINE  
alter tablespace users OFFLINE NORMAL; ... prepne tabulkovy prostor do offline.  
alter tablespace users OFFLINE TEMPORARY; ... prepne tabulkovy prostor do offline. Jsou-li nektere soubory offline kvuli chybe zapisu, musi se pak udelat recovery pred online  

alter tablespace users OFFLINE IMMEDIATE; ... prepne tabulkovy prostor do offline, nezapise checkpointy a musi se udelat recovery pred online.  
alter tablespace users ONLINE; ... prepne tabulkovy prostor do online.  
alter tablespace tblspc READ ONLY; ... prepne tabulkovy prostor pouze do cteciho modu (zakaze zapis) (COMPACTIBLE musi byt vetsi nebo rovno 8.10)  
alter tablespace tblspc READ ONLY; ... prepne tabulkovy prostor pouze do modu cteni i zapis  
alter tablespace bigspc RESIZE 80G; ... zmeni velikost datoveho souboru u velikeho tabulkoveho prostoru na 80 GB  
alter tablespace bigspc AUTOEXTEND ON NEXT 10GB; ... zapne automaticke zvetsovani o 10 GB  
alter tablespace bigspc AUTOEXTEND ON NEXT 10GB MAXSIZE 100GB; ... zapne automaticke zvetsovani o 10 GB, max. velikost 100GB  
alter tablespace dctspc DEFAULT STORAGE (NEXT 100K); ... zmeni parametr NEXT u slovnikove manazovanych extentu  
alter tablespace dctspc COALESCE; ... Provede slouceni sousedicich volnych extentu  

alter tablespace tmpspc ADD TEMPFILE '/oradata/tmpfile2.dbf' SIZE 18M; ... Prida do docasneho tabulkoveho prostoru tmpspc dalsi datovy soubor o velikosti 18MB  
ALTER DATABASE TEMPFILE '/oradata/tmpfile2.dbf' OFFLINE; ... docasne vypne pouzivani datoveho souboru  
alter database tempfile '/oradata/tmpfile2.dbf' ONLINE; ... opet zapne pouzivani datoveho souboru  
alter database tempfile '/oradata/tmpspc.dbf' RESIZE 18M; ... zmeni velikost datoveho souboru  
alter datavase tempfile '/oradata/tmpfile2.dbf'  DROP INCLUDING DATAFLES; ... vylouci datasoubor z pouzivani a navic jej smaze z disku  
alter database XE DEFAULT TEMPORARY TABLESPACE tmpgroup1; ... nastavi vychozi docasny prostor GRUPU tmpgroups1  
alter database DATAFILE '/u2/data/tblspc2.dbf' AUTOEXTEND OFF; ... vypne automaticke zvetsovani  
alter database DATAFILE '/u2/data/tblspc2.dbf' RESIZE 100M; ... Manualne zmeni velkost datoveho souboru  
alter database DATAFILE '/u2/data/tblspc2.dbf' OFFLINE FOR DROP; ... Zmeni datovy soubor do OFFLINE i kdyz nejde dopsat logy. Datafile nepujde dato do online, da se jen smazat  

alter database RENAME DATAFILE '/u1/1.dbf' '/u1/2.dbf' TO '/u2/1.dbf' '/u2/2.dbf'; ... prejmenuje Datove soubory v definicich, po te, co jsou fyzicky prejmenovane<. Musi byt v OFFLINE  
DROP TABLESPACE users; ... zrusi prazdny tabulkovy prostor  
drop tablespace users INCLUDING CONTENTS; ... zrusi tabulkovy prostor i kdyz neni prazdny  
drop tablespace users INCLUDING CONTENTS AND DATAFILES; ... zrusi tabulkovy prostor i kdyz neni prazdny a smaze i daove soubory  
SELECT * FROM V$TABLESPACE; ... ukaze vsechny tablespace  
select PROPERTY_NAME,PROPERTY_VALUE FROM DATABASE_PROPERTIES where PROPERTY_NAME="DEFAULT_%_TABLESPACE"; vypise  docasne TS  
select * from DBA_TABLESPACES; ... informace o databazovych tabulkovych prostorech, velikosti, statusu a pod.  
select * from USER_TABLESPACES; ... informace o uzivatelskych tabulkovych prostorech, velikosti, statusu a pod.  

select * from DBA_TABLESPACE_GROUPS; ... Seznam skupin tabulkovych prostoru  
select * from DBA_SEGMENTS; ... Seznam vsech segmenu DB Tabulkovych prostoru  
select * from USER_SEGMENTS; ... Seznam vsech segmenu uzivatelskych tabulkovych prostoru  
select * from DBA_EXTENTS; ... Seznam vsech extentu DB Tabulkovych prostoru  
select * from USER_EXTENTS; ... Seznam vsech extentu uzivatelskych tabulkovych prostoru  
select TABLESPACE_NAME "TABLESPACE",FILE_ID,COUNT(*) "PIECES",MAX(blocks) "MAXIMUM",SUM(blocks) "TOTAL" from DBA_FREE_SPACE group by TABLESPACE_NAME, FILE_ID; ... Seznam vsech volnych mist DB tabulkovych prostoru a statistiky  
select * from USER_FREE_SPACE; ... Seznam vsech volnych mist uzivatelskych tabulkovych prostoru  
select NAME from V$DATAFILE; ... Seznam jednotlivych datovych souboru tabulkovych prostoru  
select NAME from V$TEMPFILE; ... Seznam jednotlivych datovych souboru docasnych tabulkovych prostoru  

select * from DBA_DATA_FILES; ... Seznam jednotlivych tabulkovych prostoru, datovych souboru a jejich parametry  
select * from DBA_TEMP_FILES; ... Seznam jednotlivych docasnych tabulkovych prostoru, datovych souboru a jejich parametry  
select USERNAME,ACCOUNT_STATUS,DEFAULT_TABLESPACE from DBA_USERS; ... Ukaze, ktery uzivatel standartne zapisuje do jakeho tabulkoveho prostoru  
select * from DBA_TS_QUOTAS; ... Ukaze kvoty na tabulkove prostory  
select BLOCK_ID, BYTES, BLOCKS from DBA_FREE_SPACE where TABLESPACE='dctscp' order by BLOCK_ID; ... vypise seznam volnych extentu ve slovnikove manazovanem tablespace  
select * from DBA_FREE_SPACE_COALESCED ... vypis parametru pro slucovani sousednich volnych extentu  
select * from V$SYSAUX_OCUPANTS; ... ukaze, jake tabulky obsahuje SYSAUX  
select * from V$TRANSPORTABLE_PLATFORM; ... seznam formatu pro exportovani tabulkovych prosoru  
EXECUTE DMBS_SPACE_ADMIN.SEGMENT_VERIFY('SYSTEM'); ... Soucast baliku DBMS_SPACE_ADMIN  - otestuje vsechny segmenty  

EXECUTE DMBS_SPACE_ADMIN.TSEGMENT_CORRUPT('SYSTEM'); ... Soucast baliku DBMS_SPACE_ADMIN  - oznaci spatne segmenty  
EXECUTE DMBS_SPACE_ADMIN.SEGMENT_DROP_CORRUPT('SYSTEM'); ... Soucast baliku DBMS_SPACE_ADMIN - smaze oznacene segmenty jako corrupt  
EXECUTE DMBS_SPACE_ADMIN.TABLESPACE_REBUILD_QUOTAS('SYSTEM'); ... Soucast baliku DBMS_SPACE_ADMIN - znovu rebuilduje kvoty  
EXECUTE DMBS_SPACE_ADMIN.TABLESPACE_MIGRATE_FROM_LOCAL('SYSTEM'); ... Soucast baliku DBMS_SPACE_ADMIN - prevod z localy managed tablespace  
EXECUTE DMBS_SPACE_ADMIN.TABLESPACE_MIGRATE_TO_LOCAL('SYSTEM'); ... Soucast baliku DBMS_SPACE_ADMIN - prevod na localy managed tablespace  
EXECUTE DBMS_TTS.TRANSPORT_SET_CHECK('tblspc1','tblspc2', TRUE); ... otestuje, zda tabulkove prostory neovsahuji odkazy na data v jinych tabulkovych prostorech a zda mohou byt transportovany. Vystup jde do TRANSPORT_SET_VIOLATIONS  

#### [REDO Log](http://www.adp-gmbh.ch/ora/concepts/online_redo_logs.html)

Parametry databaze (v PF): NOARCHIVELOG, ARCHIVELOG  

ALTER SYSTEM SET ACHIVE_LAG_TARGET=1800; ... zmeni cas, po kterem se rotuji REDO logy  
alter database archivelog; ... povoli logivani (musi byt vypnuta databaze  
ALTER DATABASE ADD LOGFILE ('/ora/1.rdo', '/ora/2.rdo') SIZE 500K; ... prida do databaze 2 REDO logy  
ALETR DATABASE ADD LOGFILE GROUP 10 ('/ora/g10l1.rdo', '/ora/g10l2.rdo') SIZE 500K; ... prida grupu REDO logu do databaze  
ALTER DATABASE ADD LOGFILE MEMBER '/ora/G10l3.rbo' to GROUP 10; ... prida dalsi datafile do REDO grupy 10  
ALTER DATABASE ADD LOGFILE MEMBER '/ora/G10l3.rbo' to ('/ora/g10l1.rdo', '/ora/g10l2.rdo') ... jiny zpusob pridani data souboru do skupuny REDO logu  
ALTER DATABASE RENAME FILE '/ora/G10l3.rbo' TO '/ora2/g10l3.rbo'; ... prejmenuje REDO log (musi byt prejmenovany soubor na systemu a zavrena databaze)  
ALTER DATABASE DROP LOGFILE GROUP 3; ... smaze REDO skupinu 3  
ALTER DATABSE DROP LOGFILE MEMBER '/ora2/g10l3.log'; ... smaze clena REDO skupiny  

ALTER DATABASE CLEAR LOGFILE gROUP 3; ... vycisti / promaze logy ve skupine 3  
ALTER DATABASE CLEAR LOGFILE UNARCHIVED GROUP 3; ... vycisti / promaze logy ve skupine 3, ktera nebyla archivovana  
ALTER DATABASE CLEAR LOGFILE UNRECOVERABLE DATAFOILE '/ora/a.rdo'; ... vymaze redo v offline databazi, kdyz ji chci dat do online a RDO log je poskozeny  
alter database OPEN RESETLOG; ... vytvori se dalsi REDO logy v DB_CREAE_ONLINE_DEST_n  
ALTER SYSTEM DB_BLOCK_CHECKSUM DISABLE; ... vypne kontrolu bloku v REDO logach  
ALTER SYSTEM SWITCH LOGFILE; ... prinuti zmenit pouzivani redologu na dalsi soubor  
select member from v$logfile; ... ukaze ve kterem souboru je redolog tablespace  
select status from v$log; ... ukaze status REDOLogu  
select * from V$LOG_HISTORY; ... vypis historie zmen v redo logach  

#### Archiv Redologu

select log_mode from v$database; ... Stav archivu  
show parameter log_archive_start; ... ukaze, zda se archiv startuje pri startu instance  
alter database archivelog; ... pri neotevrene databazi zapne archivovani REDO logu  
alter database archivelog manual; ... zapne manualni archivovani REDO logu  
ALTER SYSTEM ARCHIVE LOG ALL; ... zaarchivuje aktualni REDO logy  
ALTER SYSTEM SET LOG_ARCHIVE_MAX_PROCESSES=3; ... Zmeni maximalni pocer ARC procesu  
ALTER SYSTEM SET LOG_ARCHIVE_DEST_4='LOCATION=/u02/oracle/rbdb1/' ... specifikuje lokaci archivu c 4  

ALTER SYSTEM SET LOG_ARCHIVE_DEST_4='LOCATION=/u02/oracle/rbdb1/'MANDATORY ... specifikuje lokaci archivu c 4 a nastavi, ze zapis do nej je povinny  
ALTER SYSTEM SET LOG_ARCHIVE_DEST_5='SERVICE - standby1'; ... specifikuje, ze archiv 5 bude zalohovat na "standby1" z tnsnames.ora  
ALTER SYSTEM LOG_ARCHIVE_FORMAT=arch_%t_%s_%r.dbf; ... specifikuje format jmena souboru archivu  
alter system archive log_start; ... automaticky start archivu, nebo to stejne lze nastavit v init.ora  
alter system LOG_ARCHIVE_DEST = '/arch1'; ... zapne jen jeden/2 archivy, nastavi jejich lokaci  
alter system LOG_ARCHIVE_DUPLEX_DEST = '/arch2'; ... prida k 1 archivu druhy, zalozni  
alter system LOG_ARCHIVE_MIN_SUCCEED_DEST=3; ... nastavi, ze se musi povest zapis minimalne do 3 destinaci archivu  
alter system set LOG_ARCHIVE_TRACE=12; ... nastavi uroven logovani udalosti pri archivaci  
archive log list; ... ukaze stav archivu a zda je archivace zapnuta  

recover database until cancel; ... Obnova z archivu?  
select DEST_ID,DEST_NAME,STATUS,BINDING from V$ARCHIVE_DEST; ... Vypise seznam a stav vsech Archivu  
select RECID,STAMP,NAME,DEST_ID from V$ARCHIVED_LOG; ... ukaze lokace archivu  
select * from V$ARCHIVE_PROCESSES; ... prehled archivacnich procesu  
select * from SYS.V$LOG; ... seznam REDOLOGu, kde je vicet, co je potreba zaarchivovat  
select * from V$BACKUP_REDOLOG; ... informace o zalohach v archivech  

#### Undo log

Undo tabulkovy prostor slouzi na ukladani undo logu. Uchovavaji se tam informace, ktere se meni v datovych souborech pri vykonavani operaci s daty  

ALTER SYSTEM SET UNDO_RETENTION=2400; ... zmeni UNDO_RETENTION - min. cas po ktery se uchovavaji data pri zmenach zpusobenych operacemi s daty  
ALTER SYSTEM SET UNDO_TABLESPACE=undotbs2; ... zmeni tabulkovy prostor pro UNDO logy  
%%ALTER SYSTEM SET UNDO_TABLESPACE=''%%; ... Vypne soucasny tabulkovy prostor z uzivani  
ALTER TABLESPACE undotbs2 RETENTION NOGUARANTEE; ... Zmeni garantovani zpetnych logu na vypnuto  
CREATE UNDO TABLESPACE undotbs2 RETENTION GUARANTEE; vytvori Undo TS undotbs2, ktery garantuje undo proceduru pro datove operace. Pokud opearce nemuze jiz zapisovat do undo, tak se stornuje  
SELECT TUNED_UNDORETENTION FROM V$UNDOSTAT; ... ukaze hodnotu UNDO_RETENTION  
SELECT RETENTION FROM DBA_TABLESPACES; ... Ukaze u undo tabulek hodnotu, zda je nastaveno GUARANTEE, NONGUARANTEE nebo NOT APPLY  
select * V$UNDOSTAT; ... Obsahuje informace pro monitorovani a ladeni Undo prostoru  
select * V$ROLLSTAT; ... Pro automaticky Undo management, informace o chovani undo segmentu v undo TS  

select * V$TRANSACTION; ... Informace i Undo segmentech  
select * DBA_UNDO_EXTENTS; ... Ukaze status a velikost vsech extentu Undo TS  
select * WRH$_UNDOSTAT; ... Ukaze statisticky snapshot V$UNDOSTATu  
select * WRH$_ROLLSTAT; ... Ukaze statisticky snapshot V$UNDOSTATu  
select TO_CHAR(BEGIN_TIME 'MM/DD/YYYY HH24:MI:SS') BEGIN_TIME, TO_CHAR(END_TIME 'MM/DD/YYYY HH24:MI:SS') END_TIME, UNDOTSN, UNDOBLKS, TXNCOUNT, MAXCONCURENCY as 'MAXCON" FROM v$UNDOSTAT WHERE rownum <= 144; ... ukaze statistiky uzivani unda  
UNDO_POOL ... kvoty pro UNDO prostor pro jednotlive uzivatele  

==odhad velikosti Undo TS==

```
DECLARE
  tid NUMBER;
  tname VARCHAR2(30);
  oid NUMBER;
  BEGIN
  DBMS_ADVISOR.CREATE_TASK('Undo Advisor', tid, tname, 'Undo Advisor Task');
  DBMS_ADVISOR.CREATE_OBJECT(tname, 'UNDO_TBS', null, null, null, 'null', oid);
  DBMS_ADVISOR.SET_TASK_PARAMETER(tname, 'TARGET_OBJECTS', oid);
  DBMS_ADVISOR.SET_TASK_PARAMETER(tname, 'START_SNAPSHOT', 1);
  DBMS_ADVISOR.SET_TASK_PARAMETER(tname, 'END_SNAPSHOT', 2);
  DBMS_ADVISOR.execute_task(tname);
  end;
```


Vystup lze videt v DBA_ADVISOR_*, nebo v Automatic Database Diagnostic Monitor v Enterprise Manager\\. Velikost UndoTS se doporucuje: UndoSpace_bloky = Undo_retention * Undo_blocks_per_second + overhead.

##### Balicek Flashback

DBMS_FLASHBACK ... balicek na vraceni zmen pri omylem spustenych prikazech ci pri vyvoji  
FLASHBACK TABLE ... umozni uzivatelum obnovit tabulku do predchoziho casoveho bodu  

==Prechod na automaticky undo management==

```
DECLARE
  utbsiz_in_MB NUMBER;
BEGIN
  utbsiz_in_BM ;= DBMS_UNDO_ADV.RBU_MIGRATION;
end;
```


### Objekty v databazich

<a name="uzivatele|]]
#### Uzivatele

Zakladni uzivatele: SYS (pwd: CHANGE_ON_INSTALL), SYSTEM (pwd: MANAGER)

alter user user quota unlimited on users;  
ALTER USER "BENR" IDENTIFIED BY "passwd"; ... zmeni heslo uzivatele BENR  
CREATE USER obchod IDENTIFIED BY heslo; ... vytvori uzivatele obchod s heslem heslo  
create user ibm02wrd profile default identified by passwd default tablespace users temporary tablespace temp account unlock;  
SELECT * FORM V$PWFILE_USERS ... ukaze, kteri uzivatele maji SYSDBA a SYSOPER prava v souboru s hesly  
GRANT SYSDBA to user; ... prida prava SYSDBA uzivateli user  
GRANT connect, resource TO obchod; ... Prida prava na pripojeni a praci s tabulkoy pro uzivatele obchod  
REVOKE CONNECT FROM user; ... odebere prava CONNECT uzivateli user  
orapwd file=hesla.pwd password=HESLO entries=30 ... Vytvori soubor s hesly hesla.pwd na 30 zaznamu. heslo pro usivatele SYS je HESLO (nastavuje se jeste parametr REMOTE_LOGIN_PASSWORDFILE v init.ora)  
init.ora : REMOTE_LOGIN_PASSWORDFILE ... nastaveni souboru s hesly  

select USERNAME,ACCOUNT_STATUS from dba_users where USERNAME like 'rman%'; ... vylistuje uzivetere RMAN* a jejich status  
select * from all_users; ... vypis vsech nuzivatelu  
select * from DBA_ROLES; ... vylistuje seznam roli  
select * from DBA_ROLE_PRIVS; ... vylistuje seznam opravneni  

#### Tabulky - Table

SELECT table_name FROM user_tables; ... seznam tabulek  
CREATE TABLE test (name VARCHAR(20)); ... vytvori tabulku test s jednim sloupcem  
create table sales (invoice_no NUMBER, s_y INT NOT NULL, s_m INT NOT NULL, s_d INT NOT NULL) PARTITION BY RANGE (Ss_y, _m, s_d) (partition jan04 values less than (2004, 2, 1), partition feb04 values less than (2004, 3, 1)); ... vytvori tabulku, ktera je spojenim vice tabulek. Pouziva se napriklad ve skladisti (warehouse) dat  
ALTER TABLE sales ADD PARTITION mar04 VALUES LESS THAN (2004,4,1); ... prida dalsi cast tabulky do skladiste dat  

alter table sales EXCHANGE PARTITION mar04 WITH TABLE sales_march_2004 INCLUDING INDEXES; ... prepise data z tabulky sales_marc_2004 do tabulku mar02  
alter table MOVE PARTITION jan04; ... zrusi cast tabulky jan04  
CREATE INDEX salex_index ON salex(invoice_no) LOCAL; vytvori index pro tabulku sales  

#### Nahledy - View

CREATE VIEW cz_firmy AS SELECT id, zakaznik FROM firmy WHERE zemeid='CZ'; ... vytvori nahled cz_firmy z tabuly firmy, vybere jen nektere radky a sloupce  
SELECT * FROM cz_firmy; ... Oracle toto prelozi jako: SELECT * FROM (select id, zakaznik from firmy WHERE zemeid='CZ')  

#### Oracle procesy

ALTER SYSTEM SHARED_SERVERS = 3 ... nastavi minimalni pocet sdilenych procesu na 2  
ALTER SYSTEM MAX_SHARED_SERVERS = 100 ... nastavi maximalni pocet sdilenych procesu na 100, mel by byt mensi nez inicializacni parametr PROCESSES  
ALTER SYSTEM SET SHARED_SERVER_SESSIONS ... Celkovy soucet sessions, ktere mohou jet soucasne. Omezene inicializacnim parametrem SESSIONS  
ALTER SYSTEM SET DISPATCHERS = '(PROT=tcp)(DISP=2), '(PROT=tcps)(DISP=2)' ... Nastaveni/zmena poctu dispatcheru  
ALTER SYSTEM SET DISPATCHERS = '(INDEX=0)(DISP=3), '(INDEX=1)(DISP=1)' ... Nastaveni/zmena poctu dispatcheru  
ALTER SYSTEM SET MAX_DISPATCHERS ... Max pocet dispatcheru. Do verze vcetne 10 se nepouziva  
ALTER SYSTEM SET CIRCUITS ... Celkovy pocet virtualnich okruhu v pameti ???  
SELECT * FROM V$DISPATCHER;  
SELECT * FROM V$DISPATCHER_CONFIG;  

SELECT * FROM V$DISPATCHER_QUEUE;  
SELECT * FROM V$QUEUE;  
SELECT * FROM V$SHARED_SERVER;  
SELECT * FROM V$CIRCUIT;  
SELECT * FROM V$SHARED_SERVER_MONITOR;  
SELECT * FROM V$SGA;  
SELECT * FROM V$SGASTAT;  
SELECT * FROM V$SHARED_POOL_RESERVED;  

#### Oracle zamky / locks

select * from V$LOCKS; ... seznam zamknutych zamku  
select * from DBA_BLOCKERS; ... seznam procesu, ktere blokuji objekty, na ktere ostatni procesy cekaji  
select * from DBA_WAITERS; ... seznam procesu, ktere cekaji na zamknute objekty  
select * from DBA_DDL_LOCKS; ... seznam DDL zamku  
select * from DBA_LOCKS; ... seznam zamku  
select * from DBA_LOCK_INTERNAL;  
select * from V$LOCKED_OBJECT; ... seznam zamknutych objektu  

<a name="zalohovani|]]
### Zalohovani a obnova databazi

#### Spusteni RMAN - Recovery MANager

echo $ORACLE_SID ... kontrola, zda je nastaven SID instance  
[rman](http://ss64.com/ora/rman.html) ... nastartuje RMAN, nepripoji se do zadne zatabaze  
rman @/dir/prikazy.txt  ... spusti RMAN a vykona prikazy v souboru prikazy.txt  
rman TARGET SYS/pwd@target_str ... Spusti RMAN a pripoji se do databaze  

rman TARGET SYS/pwd@target_str LOG $ORACLE_HOME/dbs/log/my_log.log APPEND ... Spusti RMANm pripoji se do DB a exportuje logy do souboru  
rman TARGET SYS/pwd@target_str CATALOG cat_usr/pwd@cat_str ... Spusti RMAN, pripoji se do DB a obnovi katalog\\

```
cat backup_full.rman
run {
   allocate channel d1 type disk;
   backup full database format '/export/rman/rman_%n_%T_%s_%p.bus';
}
rman nocatalog target / cmdfile='backup_full.rman' log='/export/rman/rman.log' ... spusti RMAN davkovy soubor\\
```


#### Ovladani RMAN

RMAN> @/my_dir/my_command_file.txt ... spusti prikazy ze souboru  
RMAN> backup database; ... nejjednoduzsi zazalohovani databaze  
RMAN> list backup; ... bylistovani backupu  

RMAN> list backup smmary; ... statistiky backupu  
RMAN> restore datafile '/oradata/system.dbf'; ... obnoveni ze zalohy  
RMAN> recover datafile '/oradata/system.dbf'; ... obnoveni ze zalohy  
RMAN> startup force nomount; ... nastartuje instanci, ale nemountuje databazi  
RMAN> CONVERT TABLESPACE tblspe1,tblspc2 TO PLATFORM 'Microsoft Windows NT' FORMAT '/temp/%U'; ... zkonvertuje tabulkovy prostor do formatu Windows NT  
RMAN> CONVERT DATADILE '/oradata/d1.dbf', '/oradata/d2.dbf' TO PLATFORM="Solaris(tm) OE (32-bit)" FROM PLATFORM="HP TRu64 UNIX" DBFILE_NAME_CONVERT "/oradata/", "/oradatasun" PARALLELISM=5; ... konvertuje datove souboru  

<a name="dump|]]
#### DUMP

EXPORT:\\

```
# mkdir /export/oracle_exports
# chown oracle:dba /export/oracle_exports
create or replace directory exportdir as '/export/oracle_exports';
grant read, write on directory exportdir to system;
$ expdp system/passwd FULL=y DUMPFILE=exportdir:Oracle-Oct11-fullexp.dmp LOGFILE=exportdir:Oracle-Oct11-fullexp.log
```

$ EXPDP system/passwd DUMPFILE=expdat.dmp DIRECTORY=dpump_dir TRANSPORT_TABLESPACES = tblspc1,tblspc2 ... exportuje data pro prenos tabulkovych prostoru mezi databazemi. Exp.dump je potrebny i spolu s datovymi soubory pro import do jine DB. Tabulkove prostory musi byt v read only modu, kdyz se dela dump.  
IMPORT:\\

```
startup
create or replace directory dump_dir as '/u01/app/oracle/DUMPS';
$ impdp system/passwd FULL=y DIRECTORY=dump_dir DUMPFILE=Oracle-Oct11-fullexp.dmp LOGFILE=Oracle-Oct11-import.log
```

$IMPDP system/passwd DUMPFILE=expdat.dmp DIRECTORY=dpump_dir TRANSPORT_DATAFILES=/oradata/d1.dbf,/oradata/d1.dbf REMAP_SCHEMA=(orgiser1:newuser1) REMAP_SCHEMA=(orgiser2:newuser2) ... naimportuje prenesene tabulkove prostory  

#### Kopirovani souboru pomoci Oracle DBMS_FILE_TRANSFER

CREATE DIRECTORY SOURCE_DIR AS '/usr/adim/source'; ... nastaveni promenne pro zdroj  
CREATE DIRECTORY DEST_DIR AS '/usr/adim/destination'; ... nastaveni promenne pro cil  

GRANT EXECUTE ON DBMS_FILE_TRANSFER TO strmadmin; ... nastaveni prava transferu pro uzivatele strmadmin  
GRANT READ ON DIRECTORY source_dir TO strmadmin; ... nastaveni prava cteni pro uzivatele strmadmin  
GRANT WRITE ON DIRECTORY dest_dir TO strmadmin; ... nastaveni prava zapisu pro uzivatele strmadmin  
CONNECT strmadmin/strmadminpwd; ... Pripojeni pod uzivatelem  
BEGIN BBMS_FILE_TRANSFER.COPY_FILE(source_directory_object => "SOURCE_DIR', source_filename => 'db1.dbf', destination_directory_object => "DEST_DIR', destination_filename => 'db1_copy.dbf'); END; ... Kopirovani souboru  
BEGIN BBMS_FILE_TRANSFER.COPY_FILE@DB(source_directory_object => "SOURCE_DIR', source_filename => 'db1.dbf', destination_directory_object => "DEST_DIR', destination_filename => 'db1_copy.dbf'); END; ... Kopirovani souboru na vzdalenych DB  
DBMS_FILE_TRANSFER.PUT_FILE@DB1 ... prenos na jiny server  
DBMS_FILE_TRANSFER.GET_FILE@DB1 ... prenos z jineho serveru  

<a name="sqlloader|]]
#### SQL*Loader - Import dat ze souboru

SQL*Loader nacita data ze souboru do Oracle tabulek. Je to velice rychlaa cesta, jak nacist data do tabulek.

```
create table sys_log_tbl (timestamp date, hostname varchar2(12), message varchar2(1024) );
$ cat syslog.ctl 
-- SQL*Loader Control File for Syslog
-- Oct  5 11:28:33 vixen su: [ID 810491 auth.crit]....
-- Oct  5 11:29:06 vixen last message repeated 4 times
-- 1-----  -0----| |--0| |--------------->
-- 1----------->15 17-21 23--->1024
LOAD DATA
INFILE 'messages.0'
APPEND
INTO TABLE sys_log_tbl
(timestamp      POSITION(01:15) DATE "Mon DD HH24:MI:SS",
 hostname       POSITION(17:21) CHAR,
 message        POSITION(23:1024) CHAR
)
$ sqlldr USERID=ben/passwd CONTROL=syslog.ctl LOG=syslog.log 
```
