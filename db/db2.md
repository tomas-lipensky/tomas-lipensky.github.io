---
title: IBM DB2
---

## Odkazy

[Historie na linuxsoft](http://www.linuxsoft.cz/article.php?id_article=1684)  
[DB2 clanky](http://www.databasejournal.com/features/db2/) na databasejournal.com  
[IBM DB2 Express-C](http://www.db2teamblog.com/2010/11/rpm-and-deb-packages-for-db2-express-c.html)Volna verze DB2  
[Instalace DB2 klienta](http://newpush.com/installing-the-db2-95-client-on-aix-61/)  
[DW - Nativni DB2 enkrypce](https://www.ibm.com/developerworks/community/groups/service/html/communityview?communityUuid=fc834388-7630-4b28-9abd-2f6e702b7df7#fullpageWidgetId=Wde943098055e_4dce_8377_a82fbb3a7d55&file=a39bb3eb-5ea5-4c43-a0da-48e3eef294ed)  
[DW - DB2 security - 4: Authorities and priviledges](http://www.ibm.com/developerworks/data/library/techarticle/dm-0601wasserman/index.html)  
[DW - DB2 security - 8: Best practice](http://www.ibm.com/developerworks/data/library/techarticle/dm-0607wasserman/index.html)  
[DW - DB2 security - 11: security plugin](http://www.ibm.com/developerworks/data/library/techarticle/dm-0802kligerman/)  
[GSS Pluginy](http://www.ibm.com/developerworks/data/library/techarticle/dm-0512patil/) - vysvetleni na IBM DW  
[DW - DB2 security](http://www.ibm.com/developerworks/views/data/libraryview.jsp?search_by=db2%20security%20series) - cely serial  
[DW - nastaveni SSL komunikace](http://www.ibm.com/developerworks/data/library/techarticle/dm-1306securesocketlayers/index.html)  
[Education assistant](http://www-01.ibm.com/support/knowledgecenter/websphere_iea/home_iea.dita)  
[DW - Everything You Wanted to Know About DB2 Universal Database Processes](http://www.ibm.com/developerworks/data/library/techarticle/0304chong/0304chong.html)  
[Recommended AIX Virtual Memory Manager settings for DB2 database product](http://www-01.ibm.com/support/docview.wss?uid=swg21328602)  

## Komponenty

DAS ... database administation service - sluzba, co umoznuje vzdalenou a centralni administraci databazi  
Instalace ... nainstalovane binarky, ktere pak pouzivaji jednotlive instalace
Instance ... vlastnik databazi, procesu, souboru  
Databaze ... soubor nastaveni, tablespace, tabulek, dat a prav  

## Instalace

instance/db2ls ... seznam instanci  
install/db2_deinstall -a ... odinstalace  
db2licm -x ... znovu overi licencni informace  
db2licm -g /tmp/db2licence.txt ... report o licenci  
db2licm -l ... informace o licenci  

## Instance

## Prace s instancemi

db2cmd -i -w db2clpsetcp  ... iniciace promennych ve Windows, aby bylo mozne spoustet DB2 prikazy  
db2greg -g -dump ... Vypise DB2 registry (seznam instanci, cesta k instanci atd)  
$DB2DIR/bin/db2greg -delservrec service=DB2,version=9.7.0.10,installpath=/usr/IBM/db2/v9.7 ... vymaze instanci  
$DB2DIR/instance/db2icrt -s client InstName ... vytvoreni instance (v tomto pripade klienta)  
db2ilist ... seznam vsech instanci  
db2iauto -on db2test ... nastavi automaticke spusteni instance po restartu  
db2idrop instance ... smaze instanci (musi existovat konfiguracni soubory v sqllib)  
db2iset ... nastaveni instanci  
db2iupdt INST1 ... update (zvyseni FP) nebo presouvani instance mezi instalacemi  
db2iupgrade INST1 ... upgrade DB2 instance na istalaci, ze ktere se spousti db2iupgrade  
db2mtrk -i -d -a ... Memory Track - vyuziti pameti DB2 instanci  
db2top -m $WAITTIME -b $1 -o ${DIR}/db2top-${2}.csv ... uklada statistiky db2 instance do csv  
db2fmcd ... DB2 Fault Monitoring components  
db2support c:\windows\temp -o collect-db2support ... kolektivani dat na IBM podporu  
db2support c:\windows\temp -o collect-db2support-xmeta -d XMETA -c ... kolektovani dat na IBM podporu pro databazi XMETA  

## Struktura, konfiguracni soubory, logy

[Popis adresaru pro DB2](http://www-01.ibm.com/support/knowledgecenter/SSEPGG_10.5.0/com.ibm.db2.luw.qb.server.doc/doc/r0024443.html?cp=SSEPGG_10.5.0)  
adsm/db2adutl --- prace s TSM  
adsm/dsmapipw ... meneni hesla na TSM  
db2nodes.cfg ... spustene nody  
$INSTANCE/sqllib/db2systm ... konfigurace dbm  
/var/db2/global.reg ... globalni registry - seznam instalaci, instanci atd  
$INSTANCE/sqllib/db2dump/db2diag.log  

## Procesy

[DW - Everything You Wanted to Know About DB2 Universal Database Processes](http://www.ibm.com/developerworks/data/library/techarticle/0304chong/0304chong.html)  
db2fmp ... proces pro fenced procedures  
db2sysc ... proces database manazeru (db engine)  
db2chpw ... process ktery overuje autentifikaci  

## Database Manager

## Start/stop/status database managera

db2start ... nastartovani DB2 sluzeb  
db2start open keystore using HESLO ... nastartovani zakryptovane databaze (od 10.5.5)  
db2stop ... zastaveni DB2 sluzeb  
db2level ... vypise verzi, fix pack level atd.  
ipclean ... zastavi inter process komunikaci mezi procesama  
db2_kill ... ekvivalent ipclean + kill -9  
db2 get instance ... ukaze pod jakou (DBM) instanci zrovna operuji  
db2val -o ... validatce instalace - projde instalacni soubory a konfigurace  

## konfigurace database managera

db2 attach to INSTANCE ... pripojeni k instanci k "show detail" v get dbm cfg  
db2 get dbm cfg ... vypis konfigurace managementu instance  
db2 update dbm cfg using group_plugin NULL ... nastavi nulovou hodnotu  
db2set -e ... zobrazuje/meni parametry prostredi - soubor sqllib/profile.env  
db2set -i INST ... zobrazuje/meni parametry instance - soubor sqllib/profile.env  
db2set -g ... zobrazuje/meni globalni parametry - soubor /var/db2/global.reg  
db2set DB2COMM=SSL ... nastavi [sitovy parametr](http://www-01.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.db2.luw.admin.regvars.doc/doc/r0005660.html?cp=SSEPGG_9.7.0%2F2-2-7-4-2) pro komunikaci v SSL  

## Nody

db2 catalog tcpip node db2inst2 remote localhost server 60004 ... zakatalogizuje vzdaleny node.  
db2 list node directory  

## Databaze

## pripojeni k DB2

db2 connect ... ukaze info, zda a jako kdo  a do jake DB jsem pripojeny  
db2 connect to DATABASE ... pripoji se do databaze, pokud neni zadne spojeni, stane se db aktivni  
db2 connect to DATABASE user cognosdb using PASSWORD ... pripoji se do DB pod specifickym uzivatelem  
db2 connect reset ... odpoji se z databaze, necha bezet procesy na pozadi  
db2 terminate ... ukonci spojeni k db2 vcetne procesu na pozadi  
db2 disconnect current  

## prace s databazema

db2sampl ... vytvori samle databaze  
db2 uncatalog dv DB ... vyradi databazi z DBM katalogu  
db2 catalog db DB as ALIASDB ... zakatalogizuje databazi do DBM katalogu  
db2 catalog db DB on node db2inst2  
db2 create db MEDB ... vytvori databaze MEDB  
db2 list db directory ... seznam databazi  
db2 drop database mdmdb ... smazani databaze  
db2 -tvsf sample.ddl ... provede DDL definice  
db2 restart db DATABASE ... opravi databazi po nekorektnim zastaveni (rollbackne necommitnute operace)  
db2 quiesce db DB ... zakaze databazi otevirat nove spojeni pro uzivatele co nejsou administratori  
db2 quiesce db sample force connection ... odpoji soucasne spojeni a zakaze spojeni pro neadministratory  
db2 UNQUIESCE DATABASE ... opetovne povoli nove spojeni  
db2 activate db DATABASE ... zaktivuje databazi, i kdyz neni zadne spojeni  
db2 deactivate db DB ... deaktivuje databazi  
db2look -d simple -e ... vygeneruje DDL pro zkopirovani databaze  

## HADR

db2 "restore db SAMPLE from /tmp taken at 20150429145726 on /home/db2inst2/AUTOSTORAGE  
db2 "update db cfg for SAMPLE using HADR_LOCAL_HOST localhost HADR_LOCAL_SVC DB2_HADR_STANDBY HADR_REMOTE_HOST localhost HADR_REMOTE_SVC DB2_HADR_PRIMARY HADR_REMOTE_INST db2inst1"  
db2 "deactivate db SAMPLE"  
db2 "start hadr on db SAMPLE AS STANDBY"  
db2pd -d sample -hadr  
db2 "start hadr on db SAMPLE AS PRIMARY by force"  
db2 "takeover hadr on db SAMPLE"  
db2 "takeover hadr on db SAMPLE by force"  

<3>LOGy</3>
db2 update db cfg using LOGARCHOPT1 '/home/ia2mo/nmda_logarch.cfg' ... zmena nastaveni  
DB2 update db cfg using LOCKTIMEOUT 300 (5 min timeout)  
DB2 update db cfg using LOGFILSIZ 10000 (velikost LOGu 40 MB)  
DB2 update db cfg using LOGARCHMETH1 TSM ()  
db2 update db cfg for DB using TRACKMOD NO immediate ... deaktivace archive logu  
db2 update db cfg for DB using LOGARCHOPT1 NULL immediate ... deaktivace archive logu  
db2 update db cfg for DB using LOGARCHMETH1 OFF immediate ... deaktivace archive logu  
db2 update db cfg for DB using LOGARCHMETH1 "VENDOR:/usr/lib/libnsrdb2.so" logarchopt1 /home/instanceuser/nmda_logarch.cfg immediate  
db2 update db cfg for DB using TRACKMOD YES immediate ...  
db2 update db cfg for DB using LOGARCHMETH1 disk:/logs ... zapne archivaci logu do adresare  
db2pd -d DB -logs ... ukaze aktivni logy  
db2 list history archive log all for ELIXLPDP ... ukaze zaarchivane logy  
db2 archive log for db ELIXLPDP ... zaarchivuje logy  
db2 "rollforward db  ELIXLPDP to end of logs overflow log path ( /elixdb2/db/loga/ELIXLPDP/OWERFLOW )" ... provede znovu operace z transakcnich logu  

## Konfigurace

db2 get db cfg for QDB ... vypis konfigurace pro databazi QDB  
db2 get admin cfg ... vypis konfigurace nastaveni instance  
db2 get database manager configuration  
db2 update db cfg using STMT_CONC LITERALS ... meni soubor sqllib/db2systm  
db2 get db cfg for DB show detail  
**[Logging](http://www.ibm.com/developerworks/data/library/techarticle/0301kline/0301kline.html)**

## Prace s table space

db2 list tablespaces  
db2pd -db testdb -tablespaces ... ukaze v kterych souborech jsou ulozene ktere tabulky  
db2 "select tabname from syscat.tables where TBSPACEID='19'" ... seznam tabulek v tablespace 19  
db2 "select INDNAME from syscat.indexes where TBSPACEID='19'" ... seznam indexu v tablespace 19  
db2 LIST TABLESPACES SHOW DETAIL... seznam tablespaces a jejich parametry  
db2 "select TBSP_ID,TBSP_NAME,TBSP_TOTAL_SIZE_KB,TBSP_USED_SIZE_KB,TBSP_FREE_SIZE_KB,TBSP_UTILIZATION_PERCENT from sysibmadm.TBSP_UTILIZATION" ... velkikost a vyuziti tablespace  
db2 "alter tablespace  TS1 resize (all 85M)" ... zmeni velikost table space  
db2 "alter tablespace for tablespace TS1 reduce (FILE 'file1' 16 M, FILE 'file2' 16 M) ... zmensi tablespace, kazdy soubor o 16 MB  
db2 -v "alter tablepace TS1 lower high water mark" ... presune HWM (high water mark) co dolu, co to jde  
db2 -v "alter tablespace DMSTBSPDATA managed by automatic storage" ... prevede tablespace na automated storage  
db2 "create system temporary tablespace TEMPSPACE2 pagesize 4096 MANAGED BY AUTOMATIC STORAGE" ... vytvori temporary TS managovany automaticky  

## Prace s tabulkama

db2 list tables for all ... vylistuje tabulky pro vsechna schemata  
db2 list tables for schema ABC ... vylistuje tabulky pro schema ABC  
db2 describe table SCHEMA.TABLE ... popise tabulku - sloupce  
db2 "select tabname from syscat.tables where owner = 'DB2INST1'" ... vylistuje tabulky konkretniho uzivatele  
db2 "select distinct owner from syscat.tables" ... vylistuje vlastniky tabulek  
db2 'create table CMDBTEST ( CMID integer, NAME varchar (255) )' ... vytvoreni tabulky  
db2 create table employee2 like employee ... vytvori kopii tabulky (stejne definice sloupcu  
db2 "insert into DB2INST.CMDBTEST (CMID, NAME) values (2, 'hatla patla')"  
db2 reorg table DB2TEST.TABULKA ... reorganizace tabulky (defragmentace) - prepisuje nesouvisle bloky do souvislych  
db2 reorg table DB2TEST.TABULKA inplace ... online reorganizace tabulky  
db2pd -d DB -reorg ... ukaze status reorganizace  
db2 reorg indexes all for table employee  
db2 runstats on table DB2TEST.TABULKA with distribution and sampled detailed indexes all; ... pusti statistiky, ktere pak optimalizuji SQL dotazy  
db2 reorgchk current statistics on schema PIMCPDP ... zjisti statistiky pro cele schema  
db2 "runstats om table db2test.employee on ALL collumns with distribution on all columns and detailed indexes all"  
db2 "select * from sysibmadm.admintabinfo where tabname like 'EMPLOYEE'" ... ukaze velikosti tabulek  
db2 "select  type, substr(tabschema,1,12) as tabschema, substr(tabname,1,30) as tabname,
  substr(base_tabschema,1,12) as base_tabschema, substr(base_tabname,1,30) as base_tabname
  from [syscat.tables](https://www.ibm.com/support/knowledgecenter/SSPT3X_4.0.0/com.ibm.swg.im.infosphere.biginsights.commsql.doc/doc/r0001063.html) where type='A'" ... ukaze jaky alias je na jakou tabulku  

## Aplikace - pripojeni

db2 list applications ... sezanm operaci  
db2 get snapshop for application ... informaci o aplikaci (podle spojeni - operace)  
db2 get snapshot for application agentid 30557 ... ukaze informace o spojeni 30557  
db2 list active databases ... seznam aktivnich databazi a pocet spojeni  

db2 list db directory ... ukaze databaze a adresar, kde se nachazi  
db2 list utilities ... ukaze, jake jedou nastroje (backup atd)  
db2 force application "(23453)" ... ukonci aplikaci s cisle 23453 (appl. hadle)  
db2diag -f ... ukaze logy  
./sqllib/db2dump/db2diag.log ... chyby a statusy DB2 instance  
db2top -d A2MPIMP ... ukaze realtime vyuziti databaze  
db2 list history ALL  for db A2MPIMP ... ukaze historii vsech udalosti  
db2 get snapshot for database manager ... ukaze snapshot (status, informace) o DB manazeru  

## Prace s uzivateli a pravy

[Popis roli v DB2](http://www-01.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.db2.luw.admin.sec.doc/doc/c0055206.html)  
[Graficke znazorneni roli v DB2](http://db2commerce.com/2013/03/01/db2-basics-users-authentication-and-authorization/)  
db2 update dbm cfg using  SYSMAINT_GROUP dbagroup  
db2 "grant createin on testdb COGNOSDB to user cognosdb" ... prida prava vytvaret tabulky  
db2 grant connect,secadm on database to user UZIVATEL ... povoli uzivateli UZIVATEL pripojit se do DB a mit SECADM prave  
db2 revoke dbadm on database from user gene ... odebere prava dbadm uzivateli gene  
db2 select \* from SYSCAT.DBAUTH; ... ukaze prava uzivatelu k databazi  
db2 select \* from SYSCAT.TABAUTH; ... ukaze prava uzivatelu k tabulkam a pohledum (view)  
db2 select \* from SYSCAT.COLAUTH; ... ukaze prava uzivatelu ke sloupcum  
db2 select \* from SYSCAT.PACKAGEAUTH; ... ukaze prava uzivatelu k balickum  
db2 select \* from SYSCAT.INDEXAUTH; ... ukaze prava uzivatelu k indexum  
db2 select \* from SYSCAT.SCHEMAAUTH; ... ukaze prava uzivatelu k schematum  
db2 select \* from SYSCAT.PASSTHRUAUTH; ... ukaze prava uzivatelu k serverum  
db2 select \* from SYSCAT.ROUTINEAUTH; ... ukaze prava uzivatelu k routinam (funkcim, medodam, proceduram)  
db2 "SELECT * FROM TABLE (SYSPROC.AUTH_LIST_GROUPS_FOR_AUTHID('user'))" ... ukaze ke kterym grupam patri uzivatel  
db2 "grabtselect on db2inst.test to user test1 with grant option;"

## Prace s balicky

REBIND PACKAGE (USIBMSTODB22.TEST.DSN8BC81.(MAY_VERSION)) ... napoji baliky aplikace, kdyz se meni balicky ale nemeni se SQL vyrazy (napriklad po resotoru DB na jinou verzi DB2)  

## Backup/restore

Pro backup/resotre jsou potreba DBADM prava na databazi a SYSADM-SYSMAIN prava na instanci

db2 list history backup since 20140809000000 for db DATABAZE1 ... vylistuje vsechny backupy od 8.9.2014 pro databazi DATABAZE1  
db2 list history backup all for db DATABAZE1 ... vylistuje vsechny backupy pro databazi DATABAZE1  
db2 backup db DB1 to /mnt/backup_dir ... provede offline backup  
db2 backup db DB1 load /usr/lib/libnsrdb2.so open 1 sessions options @nmda_db2.manual.cfg ... provede backup, nacte knihovnu a parametry ze souboru  
db2 backup db DB1 online to /mnt/dbbackup/ compress INCLUDE LOGS ... online backup  
db2 restore database QDB  from /mnt/dbbackup/ taken at TIMESTAMP replace existing ... restore databaze  
db2 restore database QDB  logs from /mnt/dbbackup/ taken at TIMESTAMP logtarget /tmp/LOGS replace existing; cp /tmp/LOGS/*LOG /db/log/NODE0000 ... restore databaze s restore LOGU pro rollforward (v pripade online backupu)  
db2 "rollforward db QDB to end of logs and complete" ... po obnoveni LOGU rollforward  
db2 "rollforward db  ELIXLPDP to end of logs overflow log path ( /elixdb2/db/loga/ELIXLPDP/OWERFLOW ) " ... rollforward z obnovenych archivu  
db2 "rollforward db ELIXLPDP query status" ... ukaze info  
db2ckbkp -h DB.0.db2inst.NODE0000.CATN0000.20150415231913.001 ... informace o backupu  
db2 "export to table.csv of del select * from employee" ... export tabulky do souboru  
db2 "export to table.ixf of ixf select * from employee" ... export tabulky do souboru, ixf obsahuje definice sloupcu  
db2 "import from file.del of del replace into employee" ... import do tabulky  
db2 load from /dev/null of del replace into employees noncercoverable ... vycisti tabulku rychleji nez delete  
db2adutl query full db SAMPLE verbose ... Ukaze full backupy pro DB SAMPLE na TSM s detaily  
db2adutl queryaccess for all ... ukaze prava pro db2adutl  
db2 "backup database sample online use tsm" ... backup na TSM  
$DB2INST/sqllib/adsm/dsmapipw ... zmena hesla TSM  
vi dsm.sys ... TSM parametry  
db2 update db cfg using TSM_MGMTCLASS  DWAIX-TAPE ... nastaveni TSM  
db2 update db cfg using TSM_NODENAME  AVSDWAIX ... nastaveni TSM  
db2 update db cfg using TSM_PASSWORD password ... nastaveni TSM  
db2pd -db ELIXCPDP -fvp lam2 ... ukonci bezici backup nebo archivaci  

## Promenne, funkce

db2 set current schema maximo ... nastavi aktualni schema  
db2 "values(current schema)"  
db2 "values(current date)"  

## SQL

db2 ? ... napoveda  
db2 ? recover ... napoveda k prikazu recover  
clpplus ... jako sqlplus  
db2expln -d SAMPLE -t -q "select * from employee where empno='000010'" -g ... vysvetli u zadaneho SQL vyrazu jeho narocnost a cas  
db2expln -d SAMPLE -t -f /tmp/test.sql -z ";" -g ... to same, ale SQL bere ze souboru  
select count(*) from NETDB.TBTELMON ... spocita radky v tabulce  
db2 "select [CAST](http://www-01.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.db2.luw.sql.ref.doc/doc/r0023459.html?cp=SSEPGG_9.7.0%2F2-10-2-10-2)([TRIM](http://www-01.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.db2.luw.sql.ref.doc/doc/r0023198.html?cp=SSEPGG_9.7.0%2F2-10-3-2-165)(TBSP_NAME) as VARCHAR(20)) from sysibmadm.TBSP_UTILIZATION ... zmensi pole sloupce ve vypisu  
db2 "select char(aaa,15) from SCH.TAB;" ... zkrati vypis retezce na 15 znaku  
db2 "select * from employee fetch first 1 row only" ... zobrazi pouze prvni radek dat  
db2 'update "volumes"' "set status='detached' where id ='123'" ... prepise hodnoutu status u tabulky zadane malymi pismeny  
db -x -v "select * from employee" ... -x nevypise hlavicku, -v vypise sql prikaz  
db2 +c -m "delete from acl" ... +c necommitne po provedeni SQL, -m ukaze kolika radku se to tyka  
db2 rollback ... rollabckne necommitnute operace  
db2 commit ... commitne posledni operace  
db2 list command options ... napoveda pro prepinace  
db2 -v is ON ... prepne vychozi chovani pro -v  
db2 -tf createSchema.DLL ... spusti davku DLL (Data Definition Language)  
db2 -x "select TRIM(tabschema)||'.'||TRIM(tabname) from syscat.tables" ... trim smaze mezery na konci, || spoji 2 retezce, vysledek - seznam tabulek  
db2 "select char(tabname,30),stats_time from syscat.tables where (stats_time &lt; current timestamp -1 day) or ( stats_time is NULL ) and tabschema='DB2TEST'"  

## SQL vyrazy specificke pro DB2

SLECT * FROM table FETCH FIRST 10 ROWS ONLY ... privnich 10 radku  

## Autentifikace, GSS pluginy

[JDBC sample k gssapi_simple](https://www.ibm.com/support/knowledgecenter/SSEPGG_9.7.0/com.ibm.db2.luw.apdv.sample.doc/doc/java_jdbc/s-README.html)
