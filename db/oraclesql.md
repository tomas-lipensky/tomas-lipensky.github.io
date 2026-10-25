# oraclesql

Administrace Oracle se nachazi na strankach [Oracle](oracle.html).

## Externi odkazy

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

### Spusteni SQL skriptu v sqlplus

@/tmp/createtable.sql  

## Tabulky

### Datove typy pro tabulky

<dl>
	CHAR(20) ... pole pro retezec dlouhy 20 znaku
	VARCHAR(20) ... pole pro retezec dlouhy az 20 znaku
	DATE ... datum a cas
	INTEGER ... cele cislo
	NUMBER ... Realne cislo, az 38 znaku dlouhe. NUMBER(6,2) je omezeni cisla na max delku xxxx.xx
	BINARY_FLOAT ... (Oracle >= 10) binarni reprezentace realneho cisla - 32-bitu - uspornejsi a rychlejsi nez NUMBER. Hodnoty napr. 96.56f, BINARY_FLOAT_NAN, BINARY_FLOAT_INFINITY
	BINARY_DOUBLE ... (Oracle >= 10) binarni reprezentace realneho cisla - 64-bitu - uspornejsi a rychlejsi nez NUMBER. Hodnoty napr. 96.56D, BINARY_DOUBLE_NAN, BINARY_DOUBLE_INFINITY
</dl>

### Vytvareni tabulek

CREATE TABLE zakaznici (  
  id_zakaznika INTEGER CONSTRAINT zakaznicky_pk PRIMARY KEY ... cislo pro id zakaznika - primarni klic (PRIMARY KEY - musi byt unikatni cislo, nesmi existovat stejne)  
  jmeno VARCHAR(10) NOT NULL ... neprazdny udaj pro jmeno - az 10 znaku  
  prijmeni VARCHAR(10) NOT NULL  
  narozeni DATE  
  telefon VARCHAR(20)  
); ... vytvoreni tabulky  
id_zakaznika INTEGER CONSTRAINT zakaznicky_pk PRIMARY KEY ... cislo pro id zakaznika - primarni klic (PRIMARY KEY - musi byt unikatni cislo, nesmi existovat stejne)  

CREATE TABLE nakupy (  
  id_zakaznika INTEGER CONSTRAINT zakaznicky_pk PRIMARY KEY  
  datum DATE
  zakaznik INTEGER CONSTRAINT zakanik_fk REFERENCES ZAKAZNICI(id_zakaznika) ... vzdaleny klic (froreign key) - odkaz na zaznam jine tabukly (na primarni klic id_zakaznika)  
  zaplaceno NUMBER(8,2)
);  

### Popis tabulky

DESCRIBE zakaznici; popise sloupce, promenne a podminky nenulovosti tabulky zakaznici  

## Zaznamy v tabulce

### Vkladani

INSERT INTO zakaznici (id_zakaznika, jmeno, prijmeni) VALUES (1, 'Alois', 'Skrivanek');  

### mazani

DELETE FROM zakaznici WHERE id_zakaznika = 1; ... smaze cely radek s polozkou id_zakaznika 1  

### modifikace

UPDATE zakaznici SET jmeno = 'Albert' WHERE id_zakaznika = 1; ... modifikuje zaznam jmeno u radku s id_zakaznika 1  

### vypis

SELECT * FROM zakaznici;  

## PL/SQL

PL/SQL (Procedural Laguage) rozsiruje moznosti SQL o bloky, deklarace promennych, podminky, smycky, kursory a definice procedur a funkci

<tt>CREATE OR REPLACE PROCEDURE update_zakaznika (
 p_id_zakaznika IN zakaznici.id_zakaznika%TYPE
 p_faktor IN NUMBER
) AS pocet_nakupu INTEGER;
BEGIN
1.- popis
 SELECT COUNT(*) INTO pocet_nakupu FROM nakupy WHERE zakaznik=p_id_zakaznika;
 IF pocet_nakupu &lt; p_faktor THEN
  UPDATE zakaznici SET popis = "malo nakupuje" WHERE id_zakaznika = p_id_zakaznika;
  COMMIT
 END IF;
EXCEPTION
 WHEN OTHERS THEN
  ROLLBACK;
END update_zakaznika;
</tt>
