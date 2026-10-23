[https://clis.ng.bluemix.net/](https://clis.ng.bluemix.net/) ... CLI API download  
./install_bluemix_cli ... instalace CLI API bx  
bx -v ... verzi bx CLI API  
bx api https://api.eu-gb.bluemix.net ... vyber regionu pod kterym budu pracovat (UK)  
bx login -sso -u USER -o ORG -s PROS ... prihlasine pod uzivatelem USER, organizace ORG, prostor PROS  
bx iam spaces ... seznam prostoru (seskupeni aplikaci)  
bx iam space-create cloud-4-dev ... vytovori novy prostor pro aplikace  
bx target ... ukaze aktualni umisteni (ucet, organizace, prostor)  
bx target -s cloud-4-dev ... zmeni prostor na cloud-4-dev  
bx iam org ORG ... ukaze info o organizaci vcetne kvot  

#### aplikace

bx app push ... nahraje aplikaci v aktualnim adresari  
bx app list ... seznam aplikaci v aktualnim prostoru  
bx app show APP1 ... informace o aplikace APP1  
bx app logs APP1 --recent ... ukaze posledni logy aplikace  
bx app stop APP1 ... zastavi aplikaci APP1  
bx app start APP1 ... nastartuje aplikaci APP1  
bx app delete APP1 ... smaze aplikaci  

#### sluzby

bx service offerings ... seznam nabidek  
bx service create language_translator lite "Language Translator-x1"  
bx service list  
bx service bind APP1 "Language Translator-x1"  
bx app restage APP1 ... prekompiluje aplikaci pro novou sluzby  

### Routy

bx app routes ... 	seznam  

### Cloud foundry

cf target -o "tomas.lipensky@cz.ibm.com" -s "cloud-4-dev" ... prepne to noveho prostoru
