# Mongo DB

Mongo DB patri mezi nerelacni (NoSQL) natabaze, tedy databaze dvojic - (klic, hodnota). Couch DB je databaze, ktera bezi jako sluzba, tedy typu Server - Klient.
Vychozi port pro Couch DB je 27017.

### Externi odkazy

[Inside MongoDB: the Internals of an Open-Source Database](https://www.slideshare.net/mdirolf/inside-mongodb-the-internals-of-an-opensource-database) - prezentace o vnitrni architekture mongodb  

### Start/stop/status

service couchdb start/stop ... start/stop databaze  

### Konfigurace

dig SRV _mongodb._tcp.hk-prod.h8dkbpg.mongodb.net ... informace o serverech, které obsluhují MongoDB cluster na mongodb.com  
dig TXT  dxl-cz-pre.hr9bm.mongodb.net ... informace o replice na mongodb.com  
nslookup -type=srv dxl-cz-pre.hr9bm.mongodb.net  
nslookup -type=txt dxl-cz-pre.hr9bm.mongodb.net  
nslookup -type=srv _mongodb._tcp.dxl-cz-pre.hr9bm.mongodb.net  
### JSON, Ovladani, atd

`%%mongo --quiet dhsreport --eval "db.getCollectionNames().join('\n')"%%` ... spusti mongo prikaz z prikazove radky  
`%%mongo "mongodb+srv://SERVER" --username USER -p HESLO%%` ... pripojeni do interaktivniho modu  

### prikazy v mongo klientovi

`show dbs` ... seznam databazi  
`use testdb` ... prepne se do databaze testdb, i kdyz neexituje (vytvori se prvnim zaznamem)  
`db.dropDatabase()` ... smaze databazi  
`show collections` ... seznam collection - tabulek  
`db.system.namespaces.find()` ... jiny zpusob listovani collections  
`%%db.createCollection("COLLECTION")%%`  
`db.COLLECTION.count()` ... pocet radku v tabulce COLLECTION  
`db.COLLECTION.deleteMany({})` ... smaže všechny řádky  
`db.COLLECTION.deleteOne( { _id: "563237a41a4d68582c2509da" } )` ... smazání řádku  
`%%db.COLLECTION.insert({"name":"tutorials point"})%%` ... vlozi zaznam do collection COLLECTION  
`db.COLLECTION.explain("executionStats").find[^1]

[^1]:  { $and: [ { "userRrole":"owner", "userId":"10022"} ] } ` ... ukáže jak se zpracoval dotaz, kolik času zabral atd.  
`db.COLLECTION.find().pretty()` ... vylistuje všechny dokumenty (záznamy) v databázi COLLECTION v pěkném json zápisu  
`%%db.COLLECTION.find({"item.updated_iso": "2018-03-13T15:54:44+0100"}, {href: 1, "item.updated_iso": 1})%%` ... filtr: jen zaznamy, kde je item.updated_iso rovno danemu retezci, uaze jen "href" zaznam a _id  
`%%db.COLLECTION.find({"item.created": { $gt: 1512054095781 }}).hint( "INDEX1" )%%` ... filtr za pouziti vetsi nez, vynutí hledání pomocí indexu INDEX1  
db.COLLECTION.updateMany({}, {$set: {pozdrav: "Ahoj"}}) ... nastaví na všech záznamech vlastnost pozdrav na Ahoj  
db.COLLECTION.update({}, {$set: {pozdrav: "Ahoj"}}) ... nastaví na prvnímu záznamu vlastnost pozdrav na Ahoj  
db.COLLECTION.update({_id: "127893142751892"},{$set: {pozdrav: "Ahoj"}}) ... uprava záznamu s _id=127893142751892  
`db.COLLECTION.drop()` ... smaze collection  
`db.collection.createIndex({ "userId": 1 }, { unique: true, name: "mujIndex"})` ... vytvoří index setříděný podle userId, unikátní záznamy, index se bude jmenovat mujIndex  
`db.COLLECTION.getIndexes()` ... seznam indexu pro tabulku COLLECTION  
`db.COLLECTION.hideIndex("INDEX")` ... skryje index - nebude se používat  
`db.COLLECTION.unhideIndex("INDEX")` ... znovu aktivuje index  
`%%db.COLLECTION.dropIndex("INDEX")%%` ... smaze index INDEX v tabulce COLLECTION  
db.post.insert([
   {
      title: 'MongoDB Overview',
      description: 'MongoDB is no sql database',
      by: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 100
   },

{
      title: 'NoSQL Database',
      description: "NoSQL database doesn't have tables",
      by: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 20,
      comments: [	
         {
            user:'user1',
            message: 'My first comment',
            dateCreated: new Date(2013,11,10,2,35),
            like: 0
         }
      ]
   }
])  

### Bezpecnost

'db.getUsers()' ... seznam uzivatelu  
db.createUser({user: "reportsUser", pwd: "abcdefgh", roles: [
       { role: "read", db: "reporting" },
       { role: "readWrite", db: "accounts" ]}) ... vytvori uzivatele  
'db.dropUser("reportsUser")' ... smaze uzivatele  

### Backup

%%db.ZDROJ.find().forEach((doc) => {db.CIL.insert(doc);}) && print("HOTOVO!");%% ... záloha kolekce, kopírování kolekce  

### Import/Export

mongoexport -d dbname -c colname | gzip > dump.txt.gz  
zcat dump.txt.gz | mongoimport -d dbname -c colname  
mongoimport -d db -c collection --jsonArray --file soubor.json  
mongodump ... export vsech databazi a tabulek  
mongodump --archive=databaze.gz --gzip --db databaze ... export jedne databaze  
mongorestore ... restore databaze z dumpu  
mongorestore -d 0 ./0 --drop
