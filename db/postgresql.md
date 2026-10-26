---
title: PgSQL (Postgre SQL)
---

## Odkazy

[Clanek na linuxsoft](http://www.linuxsoft.cz/article.php?id_article=1398)  

## Příkazová řádla

### zaloha / obnoveni zalohy databaze

pg_dump dbname > outfile  
pg_dump -h db_server -U db_user -W db_name > db.20070725.dump  

psql dbname > infile  
pg_dumpall > vse.sql ... zazalohuje vse do txt souboru vse.sql  
psql -f vse.sql postgres ... obnovi vse z txt soubotu vse.txt  

### klient

psql -h HOSTNAME -p 5432 -U UZIVATEL DATABAZE ... připojení klientem do databáze  

## Postgre SQL příkazy a SQL jazyk

### Uzivatele/skupiny

SYSID skupina USER uzivatel1, uzivatel 2 ... bytvori skupinu skupina s uzivateli uzivatel1, uzivatel2  
ALTER GROUP skupina ADD USER uzivatel3 , uzivatel4 ... prida uzivatele uzivatel3, uzivatel4  
ALTER GROUP skupina DROP USER uzivatel3, uzivatel4 ... odebere uzivatele uzivatel3, uzivatel4  
ALTER GROUP skupina RENAME TO skupinaa ... prejmenuje skupinu skupina na skupnaa  
createuser --help ... konzolovy prikaz  
SYSID uzivatel1 CREATEUSER ... vytvori uzivatele uzivatel1 pomoci SQL prikazu  

### Prava

\z mytable ... vylistuje prava mytable  
GRANT INSERT ON uzivatele TO PUBLIC; ... prida funkce INSERT na tabulku insert vsem uzivatelum  
GRANT ALL PRIVILEGES ON uzivatele TO tomas; ... prida vsechny prava na tabuklu uzivatele uzivateli tomas  
GRANT SELECT, UPDATE, INSERT ON uzivatele TO GROUP admins; ... prida SELECT, UPDATE, INSERT do tabulky uzivatele skupine admins  
CREATE ROLE role1 NOLOGIN ENCRYPTED PASSWORD '123mzdy';  
ALTER ROLE role1 WITH LOGIN; ... povolí uživateli role1 se připojovat  
GRANT SELECT, INSERT, UPDATE, DELETE ON uzivatele TO role1;  
GRANT role1 TO petr; ... prida uzivatele petr ke clenum role role1  

### Tabulky

\d ... seznam vsech tabulek  
\d uzivatele ... popis tabukly uzivatele  
CREATE TABLE uzivatele (id bigserial NOT NULL, name char(50),  pwd char(32));... vytvoří tabulku uzivatele s hodnotami id, name, password  
CREATE TABLE tabulka1 OWNER vlastnik1; ... vytvoří tabulku tabulka1, kterou vlastní vlastnik1  
ALTER TABLE uzivatele ADD COLUMN preznivka character varying(50) DEFAULT 'bez prezdivky'; ... prida sloupec do tabulky  
ALTER TABLE uzivatele ALTER COLUMN prezdivka SET NOT NULL; ... zmodifikyje sloupec  
ALTER TABLE uzivatele ALTER COLUMN prezdivka DROP DEFAULT; ... odebere sloupec z tabulky  
alter table changes ALTER COLUMN owner set data type varchar(40); ... zmeni datovy typ sloupce  

### Data v tabulkach

INSERT INTO uzivatele VALUES(0,'marek', `) ... vlozi radek 0,marek,` do tabulky uzivatele  
UPDATE uzivatele SET id=1, pwd='123' WHERE login='marek'; ... zmeni radek 0,marek,'' na 1,marek,123  
UPDATE table SET email = title; ... zkopiruje hodnoty sloupre title do sloupce email  
DELETE FROM uzivatele WHERE id=1 ... zmaze radek v tabulce, u ktereho je id=1  
SELECT * FROM uzivatele; ... vylistuje radky z tabulky uzivatele  
SELECT DISTINCT name FROM uzivatele; ... vylistuje jen sloupec name ze vsech radku v tabulce uzivatele, ukaze jen unikatni hodnoty (pokud 2 hodnoty jsou stejne, ukaze jen jedu)  
SELECT ud, name FROM uzivatele where id&gt;3; ... vylistuje jen hodnoty id a name ze vsech radku v tabulce uzivatele, u kterych je id&gt;3  
SELECT ud, name FROM uzivatele where id&gt;3 ORDER BY id DESC; ... jako v predchozim, seradi hodnoty sestupne (ASC - vzestupne)  
UPDATE tickets set owner=sub.email from ( select email, user_id from users ) as sub where tickets.admin_id=sub.user_id;  ; ... slozeny update ze sekeltu  

### Vnitrni funkce psql

timeofday(); ... dnesni den  

## SQL

select t1.a, t2.b FROM t1 inner join t2 ON t1.c=t2.c WHERE t2.c=0;
