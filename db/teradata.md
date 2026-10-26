---
title: Teradate
---

## odkazy

[Viewpoint](http://developer.teradata.com/viewpoint) - webova aplikace na sledovani a managovani Teradata databaze  

## Start/stop

## Prikazy z prikazove radky

## PDE

PDE - Parallel Database Extension - aplikacni vrstva na OS (Suse linux) ktera provozuje databazi  
AMP - Access Module Procesor - Proces ktery spolu s jinymi AMPy provadi SQL dotazy, nebo jejich casti. Nekolik (i tisic) AMPu spracovava paralelne 1 SQL dotaz  
PE - Parsing Engine - prijima a optimalizuje SQL dotazy, potom dispatchyje vysledek AMPum  
BYNET - BanYan NETwork - sitova vrstva (ktera pusobi i jako aplikacni na spojovani AMP vysledku) na proposeni PE s AMP

## SQL

SELECT USER, DATABASE, CURRENT_TIME, CURRENT_DATE, SESSION, PROFILE, ROLE; ... ukaze info o aktualnim uzivateli a session  
HELP 'sql'; ... reference prikazu  
HELP 'sql grant'; ... info k prikazu sql grant  
HELP DATABASE student102; ... ukaze databazi student102  
HELP TABLE student102.employee; ... ukaze tabulku student102.employee  
SHOW TABLE student102.employee; ... ukaze definici tabulky student102.employee  
CREATER USER student102_a AS PERM 2e6 PASSWORD=heslo102;  
CREATE DATABASE student102_a1 FROM student102_a AS PERM 1e6;  
GIVE student102_a1 to student102_b;  
DROP DATABASE student102_a1;  

## Utility

### BTeq

I support TQL (Teradata Query Language). Uses datime Teradata native driver, not like TD studio etc (odbc, jdbc)

.connect 1.2.3.4  
retrieve employe.*  
explain select * from employe  

pdestate  
/etc/init.d/tpa restart .. Trusted Parallel application - PDE  
xdbw - supervisor window -> help -> get config -> restart tpa ... nebo pomoci viewpoint  
tail -f25   /var/log/messages - kdyz TPA nenastartuje

```
HELP 'HELP';

CREATE DATABASE student102_a1 FROM student102_a AS PERM=1e6;
give student102_a1 to student102_b;
DROP DATABASE student102_a1;

REPLACE MACRO student102.MyDiskSpace
AS
(
  SELECT
   USER    (CHAR(15))
  ,PROFILE (CHAR(15))
  ,SUM(currentperm) / 1000000 (DECIMAL(8,2)) AS "MB Usr//CurPerm"
  ,SUM(maxperm) / 1000000  (DECIMAL(8,2)) AS "MB Usr//Perm"
  ,"MB Usr//Perm" - "MB Usr//CurPerm"  (DECIMAL(8,2)) AS "MB Perm//available"
  ,SUM(maxspool) / 1000000   (DECIMAL(8,2)) AS "MB Usr//Spool"
  ,SUM(maxprofilespool) / 1000000  (DECIMAL(8,2)) AS "MB Prfl//Spool"
  ,SUM(maxtemp) / 1000000  (DECIMAL(8,2)) AS "MB Usr//Temp"
  ,SUM(maxprofiletemp) / 1000000  (DECIMAL(8,2)) AS "MB Prfl//Temp"
  FROM dbc.diskspacev
  WHERE databasename = USER
  ;
)
;

EXEC student102.MyDiskSpace;

CREATE MACRO student112.MyTableSizes
AS
(
  SELECT 
     databasename || '.' || tablename (CHAR(40)) AS "Table" 
    ,SUM(currentperm) (INTEGER)
  FROM dbc.tablesizev
  WHERE databasename = USER
  GROUP BY 1
  ;
)
;

EXEC  student102.MyTableSizes;

------------ Excercise 3 --------------

CREATE PROFILE STUDENT102_P AS ACCOUNT = '$M0+FACT&S&D&H',
DEFAULT DATABASE = student102,
SPOOL = 50E6,
TEMPORARY = 50E6,
PASSWORD = (EXPIRE = 91, MINCHAR = 6, MAXLOGONATTEMPTS = 3, LOCKEDUSEREXPIRE = 5, REUSE = 365, DIGITS ='R', RESTRICTWORDS = 'Y', SPECCHAR ='P');

SELECT * FROM dbc.profileinfov;

SELECT * FROM dbc.accountinfo WHERE USERNAME='student102_p';

SELECT * FROM dbc.accountinfo WHERE userorprofile='profile';

SELECT * FROM dbc.accountinfo WHERE userorprofile='user' ORDER BY 1;

CREATE USER STUDENT102_C AS PERM=0, PASSWORD =abcd12, PROFILE = student102_p;

DROP PROFILE STUDENT102_P;

------------ Excercise 4 ----------

HELP TABLE empolyee;

SELECT DISTINCT TYPE(last_name), DEFAULT(salary_amount), FORMAT(salary_amount) FROM employee;

HELP INDEX employee;

SELECT * from DBC.DatabasesV;
SELECT * FROM DBC.DatabasesV WHERE DatabaseName='student102';

SELECT * FROM DBC.dbcinfoV;

SELECT * FROM dbc.childrenv WHERE child='student102';

SELECT * FROM DBC.UsersV;
SELECT * FROM DBC.UsersV WHERE USERNAME LIKE 'student102';

SELECT COUNT(ProtectionType) FROM DBC.DatabasesV WHERE ProtectionType='F';

SELECT count(*) FROM DBC.ColumnsV WHERE DefaultValue is not NULL;

SELECT COUNT(DISTINCT(TABLENAME)) FROM DBC.ColumnsV WHERE DefaultValue IS NOT NULL;
SELECT COUNT(DISTINCT(TABLENAME || '.' || DatabaseName)) FROM DBC.ColumnsV WHERE DefaultValue IS NOT NULL;

SELECT * FROM DBC.IndexConstraintsV;

TCP/1025 ... DB port
xdbw ... na serveru spusti prehled treminalu - 6. terminal je superuser, 5. je system out
cnsterm 1 &lt;&lt; fere

select * from DBC.SysSecDefaults; ... defaultni bezpecnostni politika

select * from dbc.ProfileInfoVX; ... Ukaze aktualni profil info

SELECT PROFILE; ... ukaze profil

SELECT COUNT(*) FROM DBC.LogonoffV WHERE event LIKE 'BAD%' AND LOGDATE > CURRENT_DATE - 10; ... pocet spatnych prihlaseni za poslednich 10 dni

select count(*) from DBC.SessionInfoV; ... ukaze pocet aktualnich pripojeni

SELECT * FROM DBC.SessionInfoV WHERE USERNAME='sysdba'; ... ukaze pocet pripojeni uzivatele sysdba

SELECT * FROM DBC.DBQLRulesV WHERE USERNAME='student102'; ... ukaze pravidla z Query logu pro uziovatele student102

SELECT * FROM DBC.QryLogV WHERE USERNAME='student102'; ... Ukaze vsechny radky z query logu pro uzivatele

/*
** comment
*/
.errorout stdout;
.run file= logon_student102.bteq;
nebo
.logon 192.168.2.59/student101,teradata101;
.errorlevel 3807 severity 0;
DROP TABLE student101.accounts;
CREATE TABLE student101.accounts as ap.accounts WITH DATA;
DROP TABLE student101.customer;
CREATE TABLE student101.customer as ap.accounts WITH DATA;
DROP TABLE student101.trans;
CREATE TABLE student101.trans as ap.accounts WITH DATA;
SELECT count(*) FROM student101.accounts;
SELECT count(*) FROM student101.customer;
SELECT count(*) FROM student101.trans;
.logoff;
.quit;

LOGON 192.168.2.59/student101,teradata101;
ARCHIVE DATA TABLES (student101.accounts), (student101.trans), (student101.customer), RELEASE LOCK, FILE=myarc;
LOGOFF;

bteq &lt; prepare.bteq &gt; prepare.txt
arcmain &lt; backup.arc &gt; backup.arc

LOGON 192.168.2.59/student102/teradata102;
RESTORE DATA TABLES (), RELEASE LOCK, FILE=myarc;
LOGOFF;

LOGON 192.168.2.59/student102/teradata102;
ANALYZE DATA TABLES *, DISPLAY LONG, FILE=myarc;
LOGOFF;

LOGON 192.168.2.59/student102/teradata102;
RESTORE DATA TABLES (student102.customer_copy) ( FROM (student102.customer) ), RELEASE LOCK, FILE=myarc;
LOGOFF;

google : teradata Dieter Noeth - odkazy na internetu, kde radi Dieter Noeth, TD expert
Klaus Stock - skolitel
```
