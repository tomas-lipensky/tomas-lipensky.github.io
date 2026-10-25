# Couch DB

Couch DB patri mezi nerelacni (NoSQL) natabaze, tedy databaze dvojic - (klic, hodnota). Couch DB je databaze, ktera bezi jako sluzba, tedy typu Server - Klient.
Vychozi port pro Couch DB je 5984. CouchDB komunikuje pres HTTP/JSON, tedy HTTP je ramec, ve kterem je uzacrena zprava v [JSON](http://json.org) specifikaci.

## Externi odkazy

[couchdb.apache.org](http://couchdb.apache.org/) - domovske stranky  

## Start/stop/status

/etc/init.d/couchdb start/stop ... start/stop databaze  

## Konfigurace

/etc/couchdb/default.ini

## JSON, Ovladani, atd

http://localhost:5984/ - {"couchdb":"Welcome","version":"0.10.0"} ... uvodni JSON zprava  
http://localhost:5984/_utils ... administracni interfejs  
http://localhost:5984/atf ... informace o databazi atf  
http://localhost:5984/atf/05123432fd1234123a41234123d - {"_id":"05123432fd1234123a41234123d","_rev":"4-bea1234123412","first_name":"Tomas","last-name":"Lipensky","prefered_dbs":["couchdb","berkleydb"]} ... vypise prvek o zadanem klici  
curl -X PUT http://localhost:5984/atf/05123432fd1234123a41234123d -d '{"_rev":"4-bea1234123412","first_name":"Tom","last_name":"Mot"} ... zmena polozky, revize je povinna polozka, po updatu se zmeni cislo revize  
curl -X POST http://localhost:5984/atf -d '{"first_name":"Petr","last_name":"Pan"}' ... vytvori novy zaznam  
curl -X GET http://localhost:5984/atf ... ukaze opet informace o databazi atf
