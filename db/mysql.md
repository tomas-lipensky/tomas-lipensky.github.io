# MySQL/MariaDB

MariaDB je komunitni verze MySQL, ktera vznikla po prevzeni projekty MySQL firmou Oracle. Zachovava si prikazovou kompatibilitu.

### Externi odkazy

[Tutorial na linuxsoft](http://www.linuxsoft.cz/article.php?id_article=298)  
Pozor na [SQL injection](http://en.wikipedia.org/wiki/SQL_injection)  
[Zmanda](http;//zmanda.com/backup-mysql.html) - zalohovani MySQL  
[http://www.w3schools.com/sql/default.asp](http://www.w3schools.com/sql/default.asp) ... SQL na w3schools  

### Pripojeni se do databaze a jeji status

mysql -u root -pheslo ... vstup do databaze  
\u mysql ... vstup do DB  

show engines ... ukaze seznam enginu. Napr. NDBCLUSTER pro clustering  

### Databaze

create database DB; ... vytvori datavazi DB  
show databases; ... ukaze seznam databazi  
use DB; ... nastavi, ze se bude momentalne pracovat s databazi DB  
drop database DB; ... smaze databazi DB  

### Tabulky

Definice sloupcu v tabulce je : NAZEV_SLOUPCE PROMENNA VLASTNOSTI, kde:  
PROMENNA muze byt: INT, VARCHAR(10), TIMESTAMP, TIME, DATE  
VLASTNOST muze byt: NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK (ID>1000) - podminka, DEFAULT 'Brno' - specifikuje vychozi hodnotu

show tables; ... ukaze tabulky  
ALTER TABLE aaa ADD INDEX (status, typ, vytvoreno) ... vytvoreni indexu pro rychlejsi hledani  
ALTER TABLE changes ADD (CREATED DATE DEFAULT GETDATE()); ... prida sloupec CREATED do tabulky s aktualnim datem  
ALTER TABLE changes ADD CONSTRAINT ChangeID UNIQUE (Type,Id) ... prida sloupec Change, ktery se sklada z hodnoty Type a Id, napr CH1234  
CREATE TABLE CHANGES (ID int NOT NULL, TICKET VARCHAR(10), CREATED TIMESTAMP, UNIQUE (ID) ); ... vytvoreni tabulky  
CREATE TABLE WO_BACKUP like ipc.WO; ... zkopirovani definice tabulky;

### Zaznamy v tabulce

delete from CHANGES where TICKET="aaa"; smaze zaznamy z tabulky ... smaze zaznamy z tabukly  
insert into CHANGES (TICKET,CREATED) VALUES("BBB", "2014/01/15 20:00:00"); ... vlozi zaznam do tabukly  
insert into T2 select (MESTO,JMENO) select BYDLISTE,ZAKAZNIK from T1; ... prida do sloupci MESTO,JMENO v tabulce T1 zaznamy z T1  
update CHANGES set CREATED="2009/01/14 20:00:00" where TICKET="CH50034486" ... zmeni zaznam CREATED u zaznamu, kde ticket danemu retezci;  
select * from tabulka1 ... vylistuje vse z tabulky  
select ID,NUMBER from TABULKA where NUMBER is NULL and ID like "ID_[012]%"; ... zobrazi hodnoty ID a NUMBER, kde NUMBER neni definovane a ID zacina na "ID, pak jakykoli znam, pak cislo 0-2 a potom cokoli. [^abc] je jakykoli znak krome abc."  
select DATE,MESTO from TABULKA where MESTO in ('Brno','Praha') or DATE between #07/04/1996# AND #07/09/1996# ... jine typy podminek  
select JMENO,PRIJMENI from TABULKA order by PRIJMENI,JMENO desc; ... zobrazi setridene zaznamy JMENO a PRIJMENI v klesavem poradi, trideno podle PRIJMENI a pak JMENO  
select distinct MESTO from TABULKA; ... zobrazi vsechny unikatni zaznamy ve sloupci MESTO z tabulky TABULKA  
select JMENO from TABULKA limit 10; ... zobrazi prvnich 10 zaznamu JMENO z tabulky  
select JMENOZAKAZNIKA as ZAKAZNIK from TABULKA; ... zobrazi sloupec JMENOZAKAZNIKA a zobrazi hlavicku "ZAKAZNIK"  
select T1.JMENO,T1.PRIJMENI,T2.BYDLISTE from LIDE as T1, ADRESAR as T2 where T1.ID=T2.ID; ... pouziti aliasu pro tabukly pro lepsi zobrazeni zaznamu z vice tabulek  
select T1.JMENO,T2.CISLO from T1 full outer join T2.ID=T1.ID; zobrazi jen ty JMENA a CISLA, kde ID v T1 a T2 je slouceni (vsechny hodnoty ID v T1 a T2). Dalsi moznosti LEFT JOIN (vsehny hodnoty z leve tabulky), RIGHT JOIN, INNER JOIN - prunik  
select MESTO from T1 union select MESTO T2; ... vylistuje vsechna mesta (neduplicitni) z T1 a T2. UNION ALL = i duplicitni  

### Uzivatele, Prava

select * from mysql.user;  
GRANT ALL WITH GRANT OPTION ON *.* TO user1@'%' IDENTIFIED BY 'tajne';  ... (vytvori a) da uzivateli user1, ktery se muze pripojit odkudkoli prava na vsechny prikazy i grant  
GRANT INSERT,SELECT,UPDATE,DELETE,CREATE,DROP ON db1.* TO user2@'localhost' IDENTIFIED BY 'tajne'; ... da prava uzivateli user2 na vypsane prikazy na basechny tabulky databaze db1, ktery se pripojuje z localhostu  
REVOKE DROP,DELETE ON db1 FROM user2; ... odebere uzivateli user2 prava na DROP a DELETE  
SET PASSWORD FOR 'user1'@'localhost' = PASSSWORD('heslo'); ... nastavi uzivateli user1 heslo heslo  

### Parametry, optimalizace

[mysqld] query_cache_size=32M ... vyrovnavaci pamet pro query dotazy  
log-sloq-queries = /var/log/slow_query.log ... logovani pomalych dotazu  
log_query_time = 5 ... definice toho, co je pomaly dotaz (delsi jak 5 sekund)  

### Zaloha a obnova ze zalohy

mysqldump -u uzivatel -pheslo db1 db2 &gt; backup.sql ... zaloha databazi db1 a db2 do souboru backup.sql  
mysqldump -u root -pheslo --all-databases &gt; alldb.sql zaloha vsech databazi do txt souboru alldb.sql  
mysql -u root -pheslo db1 &lt; db1.sql ... obnova ze zalohy backup databaze db1  
mysqlimport -u root -pheslo db1 db1.sql ... obnova existujici databaze  
[Zmanda](mysql-zmanda.html) backup  

### Clustering - NDB (Network DataBase)

Architektura Master - Master, kruhy, kde kazdy je Master i slave. Vyhoda - rychlost pri cteni, synchroni data. Nevyhoda - pomalejsi zapis, zavisi na konektivite mezi nodama. CREATE, ALTER tabulky lockuje tabulku lokalne, pak teprve distribuuje. NDB brani uzivani savepointu a vraceni se v case.

my.cnf:

```
[mysqld]
server-id=1 # unikatni cislo pro kazdy node
auto_increment_offset=1
auto_increment_increment=3 # cislo - min. pocet nodu
```

dalsi moznosti:  
log_slave_updates ... loguje updaty tabulek z mastra do vlastniho logu -> muze slouzit zaroven jako master i slave  
slave_exec_mode=IDEMPOTENT ... Umoznuje, ze slave replikace pojede i kdyz budou nejake chyby. Vyhoda - cluster jede, nevyhoda - muzou se desynchronizovat data  

Po konfiguraci kazdeho nodu se musi nastavit prava, aby nody clusteru mely k sobe pristup. Ukazka pro 3 nody:

```
A: GRANT REPLICATION CLIENT, REPLICATION SLAVE, SELECT, FILE, PROCESS, SUPER RELOAD ON *.* TO 'replication'@'%s' identified by 'replpass';
A: flush privileges;
A: change master to  MASTER_HOST="serverB.examble.com", MASTER_USER="replication", MASTER_PASSWORD='replpass';
A: start slave;
B: GRANT REPLICATION CLIENT, REPLICATION SLAVE, SELECT, FILE, PROCESS, SUPER RELOAD ON *.* TO 'replication'@'%s' identified by 'replpass';
B: flush privileges;
B: change master to  MASTER_HOST="serverB.examble.com", MASTER_USER="replication", MASTER_PASSWORD='replpass';
B: start slave;
C: GRANT REPLICATION CLIENT, REPLICATION SLAVE, SELECT, FILE, PROCESS, SUPER RELOAD ON *.* TO 'replication'@'%s' identified by 'replpass';
C: flush privileges;
C: change master to  MASTER_HOST="serverB.examble.com", MASTER_USER="replication", MASTER_PASSWORD='replpass';
C: start slave;
```

### Management node pro NDB

Je to node, ktery provadi konfirgraci a management clusteru. Osvedceny postup je mit kazdy node na jinem serveru

my.cnf na management nodu:

```
[ndb_mgm]
ndb-connectistring=manage.example.com:1186
[ndb_mgmd]
config-file=/etc/config.ini
[ndbd]
ndb-connectstring=manage.example.com:1186
[mysqld]
ndbcluste # zapne cluster
nsb-force-send=1 # okamzite zasilani bufferu
ndb-index-stat-enable=1 # Optimalizuje dotazy s NDB index statistikou
engine-condition-pushdown=1
[mysql_cluste]
ndb-connectstring=manage.example.com:1186
```

a /etc/config.ini:

```
[ndb_mgmd default]
DataDir=/var/lib/mymsqk-cluster #lokace dat management nodu
[ndb-mgmd]
HostName=manage.example.com
[mdbd default]
NoOfReplicas=2 #2 data nody
[ndbd]
HostName=datanode.example.com
[mysqld]
HostName=datanode.example.com
DataDir=/var/mysql
```
