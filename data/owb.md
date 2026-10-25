# Oracle Warehouse Builder

### Externi odkazy

[OWB na wiki](http://en.wikipedia.org/wiki/Oracle_Warehouse_Builder)  
[Seznam tabulek repozitare k auditovani a monitorovani OWB](https://www.db.bme.hu/files/Manuals/Oracle/Oracle11gR2/owb.112/e10584/api_2runviews.htm#CHDHJGBE)  

### Interni odkazy

### Popis

OWB je klientsky nastoroj (klient - GUI program ktery se pripoji k nejake Oracle Repository) na navrhovani datovych skladu.
OWB definuje zdroje dat (databaze, soubory, aplikace atd) a cile - warehouse (DB2, Oracle atd), transformace, dimenze (hierarchie), atd. .
Jako repozitar potrebuje vzdy Oracle DB, kde si uklada metadata a pouziva nastroju Oracle DB na rizeni skladu (scheduler, PLSQL pro transformace atd).  

### Soubory/cesty

$ORACLE_HOME/owb  

### Prikazy

reposinst.sh ... prikaz na vytvoreni repozitare OWB na OracleDB.
