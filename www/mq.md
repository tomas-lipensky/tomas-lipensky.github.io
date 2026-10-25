# WebSphere MQ

## Externi odkazy

[Infocentral o MQ 6.0](http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/index.jsp?topic=/com.ibm.mq.branding.doc/help_home_wmq.htm)  
[Websphere MQ v6 na Linuxu](http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/index.jsp?topic=/com.ibm.mq.amq1ac.doc/lq10120_.htm)  
[Infocentral o MQ 7.0](http://publib.boulder.ibm.com/infocenter/wmqv7/v7r0/index.jsp?)  
[Websphere MQ Supprot](http://www-947.ibm.com/support/entry/portal/Overview/Software/WebSphere/WebSphere_MQ)  
[Doporucene FIXy pro MQ](http://www-01.ibm.com/support/docview.wss?uid=swg27006037)  
[MQ SupportPacs](http://www-01.ibm.com/support/docview.wss?uid=swg27007205)  
[Product overview](http://www-01.ibm.com/software/integration/wmq/)  
[WebSphere MQ Explorer](http://www-01.ibm.com/software/integration/wmq/explorer/downloads/) ... GUI na nastavovani a ovladani MQ  
[Top 15 best practice for MQ](http://www.ibm.com/developerworks/websphere/library/techarticles/0807_hsieh/0807_hsieh.html)  
[MQ cheat sheet](http://bencane.com/2013/04/22/websphere-mq-cheat-sheet-for-system-administrators/)  
[MQ read only nastaveni pro uzivatele](https://www.ibm.com/support/knowledgecenter/SSFKSJ_8.0.0/com.ibm.mq.sec.doc/q013740_.htm)  

## Soubory, adresare, konfigurace

/opt/mqm ... adresar s MQ  
/var/mqm/qmgrs ... Fronty MQ Manazeru  
/var/mqm/mqs.ini ... konfigurace MQ  
/var/mqm/mqclient.ini  
/var/mqm/qmgrs/QM_ELIX_PRD1/qm.ini  

## Stop/Start

endmqlsr ... stop MQ literenu  
endmqm QM_DEV ... zastavi MQ manazera  

## Informace

dspmqver ... napise verzi MQ  
mqrc 2009 ... unformace o Reason Codu RC 2009  

## [Procesy](https://www.ibm.com/developerworks/community/blogs/messaging/entry/an_introduction_to_websphere_mq_queue_manager_processes30?lang=en)

amqzxma0 ... Execution controler - rodicovsky proces queue manageru  
amqzlaa0 ... Agent - prijma dotazy od aplikaci, odpovida na ne, soucast queue manageru  
amqzmur0 ... restartable (mur0) - logovaci proces transakcnich informaci do log souboru  
amqzmuc0 ... critical (muc0) - logovaci proces transakcnich informaci do log souboru  
amqzfuma ... Object Authority Manager - autorizuje pripojujici aplikacni procesy  
amqrmppa ... Channel pooler - prebira dotazy od listeneru and predava je agentovi  
amqrrmfa ... repository process - proces starajici se v clusteru o sluzby v ramci repository queue  
runmqlsr ... listener - nasloucha na TCP prichozi spojeni do Queue managera  

## Logy

Zapnuti rozsireneho logovani: [http://www-01.ibm.com/support/docview.wss?uid=swg21660642](http://www-01.ibm.com/support/docview.wss?uid=swg21660642)  
/var/mqm/qmgrs/*/errors/*.LOG  
/var/mqm/errors/*.LOG  

## Prace se MQ Managerem

crtmqm test ... (Create MQ Manager) Vytvori lokalni MQ manager "test" a nadefinuje prislusne objekty  
crtmqm -sa -u DEVQMGR.DLQ DEVQMGR ... vytvori frontu DEVQMGR a Deadletter frontou DEVQMGR.DLQ  
strmqm test ... (Start MQ Manager) Spusti MQ Manager  
dspmq ... ukaze bezici MQ manazery  
endmqm test ... (End MQ Manager) Ukonci beziciho MQ Managera  
dltmqm test ... (Delete MQ Manager) Smaze MQ manazera  

dspmqcsv test ... ukaze stav Command Serveru i MQM test  
endmqcsv test ... zastavi Command Server i MQM test  
strmqcsv test ... spusti Command Server i MQM test  

setmqaut -m QM1 -n QM1.QUEUE -t queue -g users +put ... nastaci MTA autoritu pro query manager QM1, frontu QM1.QUEUE typu "queue" pro grupu users tak, ze prida pravo na "put"  
setmqaut -m QM1 -n QM1.QUEUE -t queue -g users -all +put ... nastaci MTA autoritu pro query manager QM1, frontu QM1.QUEUE typu "queue" pro grupu users tak, ze prida pravo na "put" a vypne ostatni  

jmsadmin ... ovladani JMS  

### run MQ Script Commands - [runmqsc](mqsc.html)

[runmqsc](mqsc.html) test ... (Run MQ's commands) administracni konzola pro MQM test, neco jako wsadmin  
echo "dis qmgr" | [runmqsc](mqsc.html) ... zadani prikazu pro runmqsc  
echo "dis q(*)" | [runmqsc](mqsc.html) ... seznam front v MQM  
[runmqsc](mqsc.html) QM1 &lt; commands.mqrc ... spusteni prikazu ze souboru  

## MQSeriesSamples - utility pro MQ v ramci balicku samples

/opt/mqm/samp/bin/amqsput test QM1 &lt; messages.txt ... Vlozi zpravu do fronty test v query manageru QM1  
/opt/mqm/samp/bin/amqsget test QM1 ... Vezme zpravu z fronty test v query manageru QM1  
amqsspx -m QM2 -w unlimited -t /global/recipes ... Zapne udebirani (subscribe) diskuze (topic) /global/recipes v QM2  
amqsmon -m QM2 -t statistics &gt; stat.txt ... zapise nasbirane statistiky do souboru  
amqsmon -m QM2 -t accounting &gt; acc.txt ... zapise nasbirany accounting (operace) do souboru  

## pojmy

MCA ... Message Channel Agent - posila zpravy z front do jinych, napriklad z remote front do local fron na jinych QM  
TQ ... Transmission Queue  
MQMD ... MQ Message Detail - Hlavicka zpravy  
XMQH ... Transmission queue header - rozsireni MQMD hlavicky o zpravy behem prenosu  
CCSID ... Coded Character Set ID - informace o kondovani, spolu s "Encoding" a "Format" jsou informace o formatu zpravy v MQMD - pouziva se pro konverze na zacatku nebo na konci retezce  

## MQ klient

SET MQSERVER=CHANNEL1/TCM/localhost(9002)
SET MQCHLLIB=C:\m1m ... nastaveni promenne MQCHLLIB pro MQ klienta  
SET MQSSLKEYR=C:\KEYS\key ... nastaveni lokace KDB klicenky (C:\KEYS\key.kdb)  
amqsgbrc QUEUE ... otestuje klienta - vylistuje obsah fronty QUEUE  

## Ostatni

amqiclen ... clear mqm owned IPC resource  
ipcrm ... clear any resources not cleared  by amqiclen  
crtmqcvx ... provadi konverze na prevod kodovani, formatu atd
