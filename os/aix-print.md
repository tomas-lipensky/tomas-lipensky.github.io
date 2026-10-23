# AIX - Tisk

## [lpd](http://www.ahinc.com/aix/printer.htm)

#### Start:

startsrc -s lpd<br />

#### Stop:

stopsrc -s lpd<br />

#### Status:

lssrc -s lpd<br />
/usr/lib/lpd/pio/etc/piolsvp -p ... vypis vsech tiskaren vcetne ovladace  
/usr/bin/lsallq ... vypis vsech tiskovych front  

#### Konfigurace

smitty print ... prace s tiskarnama<br />
/usr/lib/lpd/pio/etc/piomkjetd mkpq_jetdirect -p 'generic' -D asc -q 'nlp103' -h 'nlp103' -x '9100' ... vytvori tiskovou frontu nlp103 s portem 9100<br />
/usr/lib/lpd/pio/etc/piomkjetd mkpq_jetdirect -p 'generic' -D pcl -q 'PW-HPLJ8000' -h '161.120.232.252' -x '9100'<br />
lsvirprt -qQUEUE -dhp@QUEUE -a _Z ... ukaze parametr _Z tiskarny QUEUE<br />
/usr/sbin/piomisc_base two_devices rmpq  'PW-HPLJ8000' ... smaze tiskovou frontu<br />
/usr/sbin/chvirprt -q PW-HPLJ8000 'hp@'PW-HPLJ8000 -a _d=p<br />
chvirprt -qnlp103 -dhp@nlp103 -a _Z=! ... zmeni parametr _Z tiskarny nlp103<br />
switch.prt -d ... ukaze typ tisku (BSD, SystemV)  
switch.prt -s SystemV ... Zmeni typ tisku na SystemV  

#### konfiguracni soubory

/var/spool/lpd/pio/@local/custom/* ... definice vsech parametru tiskaren  
/etc/qconfig ... konfiguracni soubor tiskaren<br />
/etc/bootptab ... definice boot/ptab  

#### Tiskove fronty

qchk -Pskp044 ... vypise tiskovou frontu tyskarny skp044<br />
lpstat -pskp044 ... vypise tiskovou frontu tyskarny skp044<br />
enq -L ... dlouhy status defaultni fronty  
enq -q -P LP0 ... vypis fronty LP0  
enq -A ... status vsech tiskovych front  
/var/spool/lpd/stat ... kazdy task zde ma soubor se statusem  
/var/spool/qdaemon ... kazdy task zde ma tiskova data  
/var/spool/lpd ... kazdy task zde ma informace o tisku, odkaz na tiskova data atd.  
<br />
qprt -Pprinter /etc/motd ... posle soubor /etc/motd do tiskove fronty "printer"<br />
lpr -P printer /etc/motd ... posle soubor /etc/motd do tiskove fronty "printer"<br />
<br />
cancel 940 ... zrusi tiskovou ulohu 940  
qcan -x 940 -P abu1_1 ... zrusi ulohu 940 v tiskove fronte abul_l<br />
lprm -P abu1_1 940 ... zrusi ulohu 940 v tiskove fronte abul_l<br />
<br />
/usr/bin/enq -U -P HPLJ8000 ... Pripoji tiskovou frontu PW-HPLJ8000 k tiskarne<br />
/usr/bin/enq -D -P HPLJ8000 ... Odpoji tiskovou frontu PW-HPLJ8000 od tiskarny (po dokonceni tisku)<br />
enq -K -P HPLJ8000 ... Odpoji tiskovou frontu PW-HPLJ8000 od tiskarny (zrusi aktualni tiskovou ulohu)  
enq -q -P HPLJ8000 ... ukaze status tiskove fronty  
enq  -Q lp0  -#318 presune tiskovou ulohu 318 do fronty lp0  
enq -h -P hp1111 ... vsechny ulohy ve fronte hp1111 zmeni status na hold (zastavit tisk)<br />
enq -p -u fred ... tiskove ulohy uzivatele fred prepne do stavu release - opetovny tisk  
enq  -X  -P hp1111 ... zrusi vsechny ulohu ve fronte hp1111  
disable HPLJ8000 ... zastavi tisk ve fronte HPLJ8000<br />
enable HPLJ8000 ... spusti tisk ve fronte HPLJ8000<br />
accept HPLJ8000 ... umozni prijmani uloh ve fronte HPLJ8000<br />
reject HPLJ8000 ... zakaze prijimani uloh ve fronte HPLJ8000<br />
qadm ... frontend pro enq  
qadm -Q ... zastavi tiskovy system  
qadm -D FRONTA ... zastavi posilani uloh na tiskarnu  
qadm -U FRONTA ... povoli odesilani uloh na tiskarnu. Dokonci aktualni ulohu  
qadm -K FRONTA ... povoli odesilani uloh na tiskarnu. Zrusi aktualni ulohu  
qadm -X FRONTA ... Zrusi vsechny ulohy ve fronte  
qpri -# 123 -a 18 ... zmeni prioritu ulohy 123 na 18
