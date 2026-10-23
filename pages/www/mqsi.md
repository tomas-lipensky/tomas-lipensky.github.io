# WebSphere Message Broker

Puvodni produkt byl MQ Series Integrator

```
dspmq ... ukaze q managery
mqsilist ? ... help k prikazu
mqsilist ... ukaze infrastrukturu brokeru
mqsilist MB65 ... info o brku
mqsilist MB65 -e EG3 ... info o grupe, seznam BARu atd.
mqsilist DEVBROKER -d2 ... vice informaci o brokeru
ps -ef | grep bib
- bipservice 1 pro cfgmgr 1 pro brk, bipbroker, bipconfigmgr, biphttplistener, DataflowEngine - execuiion group
mqsidmgr???trace
mqsichangetrace DEVBROKER -t -e EXGRP -l debug -r ... zmeni tracovani u DEVBROKERa, ex.sk. EXGRP na debug a resetne tracovani
mqsireporttrace DEVBROKER -t -e EXGRP ... ukaze uroven tracovani u DEVBROKERa, ex.sk. EXGRP
mqsichangeproperties DEVBROKER -e EXGRP -o ComIbmJVMManager -n jvmDebugPort -v 9997 ... nastavi debug port
mqsibackupconfig QM65 -d /home/brk6 -a a.zip
mqsireportflowstat DEVBROKER -e default -s -g -j ... ukaze statistiky toku zprav
setmqout?
mqsicreatebroker MBNAME -i USER -a HESLO -q QM65_qmanager  -n WBRK ... Vytvori brokera MBNAME pristupneho pod uzivatelem USER, heslo HESLO pripojeneho na MQmanazera QM65_qmanager
mqsideletebroker BROKERNAME ... smaze brokera
mqsichangebroker DEVBROKER -g 60 -k 15 ... zmeni timeout z 300 na 60 config delay z 60 na 15
mqsichangebroker DEVBROKER -s active ... aktivuje bezpecnost (ACL) u broker
mqsireportbroker DEVBROKER ... ukaze vlastnosti brokera
mqsibackupbroker DEVBROKER -d C:\MQSIBroker ... zazalohuje brokera
mqsicreateexecutiongroup DEVBROKER -e EXGRP1 ... bytvoru exekucni skupinu EXGRP1 v brokeru DEVBROKE
mqsicreateexecutiongroup -i localhost -p 1416 -q DEVQMGR -b DEVBROKER -e DEVEX3
mqsicreateexecutiongroup -i localhost  -p 1415 -q QM61  -w 300 ... nespusti se, dokud nenadeplojujeme nejaky bar - hodi chybu

mqsideploy -i localhost -p 1415 -q QM61 -w 300 -b MB65 -a pager.bar
mqsideploy -i localhost -p 1416 -q DEVQMGR -b DEVBROKER -e DEVEX3 -a Admin1.bar ... Nadeployujeme BAR soubor do Exekucni skupiny
mqsireadbar -a Admin1.bar ... ukaze obsah BAR souboru
mqsideploy -i localhost -p 1416 -q DEVQMGR -b DEVBROKER -e DEVEX3 -d Admin1 ... odstrani BAR Admin1 z exekucni skupiny

mqsistartmsgflow -i localhost -p 1415 -q QM65 -w 300 -B MB65 -e EG3 -m DEFINED_FLOW ... spusti message flow DEFINED_FLOW
mqsistartmsgflow -i localhost -p 1415 -q QM65 -w 300 -B MB65 -e EG3 ... spusti vsechny message flow
mqsistopmsgflow -i localhost -p 1415 -q QM65 -w 300 -B MB65 -e EG3 -m DEFINED_FLOW ... zastavi message flow
mqsistopmsgflow -i localhost -p 1415 -q QM65 -w 300 -B MB65 -e EG3 ... zastavi vsechny message flow
mqsireload MB65 -e EG3 ... znovu nacte execution grupy
mqsilistaclentry
mqsimode -i localhost -p 1415 -q QM65 -w 300 
lslpp -a | grep mqsi
mqsivp ... installation verification
/opt/IBM/mqsi/6.1/bin/mqsiprofile ..., nadefinovane promenne potrebne pro beh brokeru
mqsistop ... zastavi config managera
mqsiservice -v .. ukaze verzi brokera
mqsicvp DEVBROKER ... otestuje brokera

mqsisetsecurity ... nastroj na konfiuraci bezpoecnosti
mqsiserdbparms ... nastaveni hesla do DB a jine parametry
```

mqsichangebroker BROKERNAME -s active ... zapne autentifikaci v Brokeru  
mqsiwebuseradmin BROKERNAME -c -u USER -a PASSWD -r ... nastavi autentifikaci k webovemu pristupu k Brokeru v MB 8+ (port 4414)  

### Web services

"Service requester" se zepta "Service registy" pomoci WSDL (Web Service Description Language). V "Service registry" jsou sluzby ulozene v UDDI (Undiversal Descriptor, Discovery and Integrator). Ten odpovi a klient najde poskytovatele.
WebSphere Registry and Repository - "Disrectory Service" = "Service Registry"
