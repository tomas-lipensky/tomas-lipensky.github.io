---
title: Redis
---

Redis patri mezi nerelacni (NoSQL) natabaze, tedy databaze dvojic - (klic, hodnota). Couch DB je databaze, ktera bezi jako sluzba, tedy typu Server - Klient.
Vychozi port pro Couch DB je 6349. Redis komunikuje pres Redis klienta, nebo pomoci knihoven (napr. pro Ruby). Redis ma silnou stranku v RAM cachingu, tedy dosahuje velmi dobre rychlosti. Diky cachovani zapisu je to rychla DB i na zapis, hrozi vsak riziko ztraty dat havarii.

## Externi odkazy

[code.google.com/p/redis](http://code.google.com/p/redis) - domovske stranky  

## Start/stop/status

/usr/local/bin/resis-server /etc/redis.conf ... start/stop databaze  
redis-cli ... redis klient  

## Konfigurace

/etc/redis.conf:  
save 900 1 ... ulozi po 900 sekundach na disk, pokud je 1 ci vice zmen  

## redis-cli

SET name Tomas ... ulozi do klice name text Tomas  
GET name ... zobrazi hodnotu textu u klice name  
GET Name ... case sensitive, pokud nenajde, vrani (nil)  
setnx Name Tomas ... pokud klic neexistuje, vytvori jej a priradi hodnotu, jinak zadna akce  

set counter 10 ... priradi cislo do klice counter  
inct counter ... zvysi cislo o 1  
dect counter ... snizi cislo o 1  

lpush seznam Chleba ... prida z leva do seznamu text Chleba  
rpush seznam Rohlik ... prida z prave do seznamu text Rohlik  
lrange seznam 0 -1 ... vypise seznam od 1. prvku do posledniho  
lindex seznam 1 ... ukaze druhy prvek  
lpop seznam ... vrati a smaze prvek zleva  
rpop seznam ... vrati a smaze prvek zprava  

sadd mnozina prvekA ... prida do klice mnozina prvekA  
sadd mnozina prvekA ... neprida do klice mnozina prvekA, protoze tam uz je  
smembers monzina ... ukaze mnozinu vsech prvku klice mnozina  
scard monzuna ... (cardinality) pocet prvku v mozine  

## Analyza exportu Redis

choco install python ## Install python  
git clone https://github.com/sripathikrishnan/redis-rdb-tools ## Download rdb-tools  
cd redis-rdb-tools; python setup.py install ## install rdb-tools  
choco install vcbuildtools ## Install Microsoft Visual C++ 14.0/build tools (required by python-lzf)  
pip install python-lzf   ## Install python-lzf  
rdb --command json soubor.rdb > soubor.json ... prevede rdb na json
