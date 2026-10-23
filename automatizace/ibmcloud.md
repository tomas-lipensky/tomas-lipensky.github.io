### Odkazy

[automatizace/softlayer](automatizace/softlayer)  
[automatizace/bluemix](automatizace/bluemix)  
[https://www.ibm.com/cloud/](https://www.ibm.com/cloud/) ... IBM Cloud  

### Portal

[https://console.bluemix.net/](https://console.bluemix.net/) ... Portal IBM Cloudu (byvala komponenta BlueMix)  
[https://control.softlayer.com](https://control.softlayer.com) ... Portal na na SL softlayer cast IBM Cloudu  
[http://www.softlayer.com/VPN-Access](http://www.softlayer.com/VPN-Access) ... rozcestinik na geograficke weby umoznujici VPN pristup  

#### Lockbox - jen pro baremetal stroje zrizene pred 2014

misto na ukladani souboru dostupnych z SL sluzeb.  
priklad na nahrani obrazu OS do lockboxu a instalaci vlastniho OS: [http://www.benmccann.com/custom-os-install-softlayer/](http://www.benmccann.com/custom-os-install-softlayer/)  

#### IPMIView

Nastroj na vzdaleni pripojeni k SL a managovani masin, vzdalene pripojeni k KVM, [mountovani ISO obrazu atd](http://knowledgelayer.softlayer.com/procedure/mount-iso-bare-metal-server).

### Bluemix

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

[ftp://ftp.supermicro.com/utility/IPMIView/](ftp://ftp.supermicro.com/utility/IPMIView/) ... stazeni IPMIView, heslo k pripojeni viditelne v portalu <a href+"http://knowledgelayer.softlayer.com/procedure/view-ipmi-credentials|takto]]  

#### API

[softlayer.github.io](https://softlayer.github.io/) - portal Softlayeru na githubu k API  
[API k Perlu](https://github.com/softlayer/softlayer-api-perl-client)  
[API k Pythonu](http://softlayer-python.readthedocs.io/en/latest/install.html)  
[Pouziti slcli](https://softlayerslayers.wordpress.com/api/command-line-interface/)  
[http://sldn.softlayer.com/reference/](http://sldn.softlayer.com/reference) ... popis API prikazu  
[Pouziti API pomoci https](http://stackoverflow.com/questions/35171114/load-from-private-image-in-softlayer)  

#### Bare Metal servers

Pro vzdaleny pristup k managovani serveru se pouziva: [BMC Client Management](https://docs.bmc.com/docs/display/public/BCM120/Introducing+Remote+Management)
