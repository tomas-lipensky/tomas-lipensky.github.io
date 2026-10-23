### Procesy

krm ... demon na ponitorovani parametru jadra, ktery vyuziva kusage  
vhand ... Vybira procesy, ktere bude swapovat (page-in, page-out)  
swagentd ... demon, ktery se stara o balicky. Ceka na swagent-a, nebo spousti swagenta, ktery spousti dotazy a akce  
swapper ... deaktivuje procesy a tim jim zabranuje swapovat (page-in, page-out)  

### sluzby obecne

<a name="skuzby|]]
who -r ... ukaze aktualni runlevel  
init 0[s,S,1,2,3,4] ... zastaveni,single,single s konzolou,single+fs mounted,multiuser,metwork multiuser+graficky,HP VUE. Spusti se, ci zastavi sluzby, ktere jsou v /etc/rcX.d  
sluzby:
<li>/etc/rcX.d ... linky do /sbin/init.d</li>
<li>/sbin/init.d ... jednotlive skripty ke sluzbam</li>
<li>/etc/rc.config.d ... nastaveni ke sluzbam. Nastaveni prezije restart</li>
ch_rc -l -p CRON ... vypis konfigurovatelnych parametru sluzby cron  
ch_rc -a -p CRON=0 ... zmena parametru sluzeb - zakaze spoousteni sluzby cron  
grep -il cron /etc/rc.config.d/* hledani konfiguracniho souboru pro cron  
/sbin/init.d/cron start[stop,start_msg,stop_msg] ... start, stop, vypis zavislosti, sluzby cron  
/sbin/init.d/template ... preddefinovany vzor pro sluzbu  
/etc/rc.log ... log soubor spouzteni/zastavovani sluzeb  
ctrl+\ ... preruseni skriptu startovani/stopovani sluzeb  

### jednotlive sluzby

/sbin/init.d/cron - /etc/rc.config.d/cron - CRON  
/sbin/init.d/nfs.client - /etc/rc.config.d/nfsconf - NFS_CLIENT  
/sbin/init.d/nfs.server - /etc/rc.config.d/nfsconf - NFS_SERVER  
/sbin/init.d/nis.client - /etc/rc.config.d/namesvrs  
/sbin/init.d/nis.server - /etc/rc.config.d/namesvrs  
/sbin/init.d/sendmail - /etc/rc.config.d/mailsvrs  
/sbin/init.d/sshd - /etc/rc.config.d/sshd  
/sbin/init.d/xntpd - /etc/rc.config.d/netdaemons  
/sbin/init.d/dt.login ... CDE graficke rozhrani  

#### lpd

check if printer exists<br />
ls -l /etc/lp/interface/name<br />
grep IP /etc/lp/interface/*<br />
ls -l /etc/lp/interface/model.orig/* (size:1561 for dumb.mag (wincor or ier),18413 for laser.mag (laser))<br />
Create printer:<br />
hppi -aq Enter the network printer name or IP address (q - quit): IP<br />
lpadmin ... konfigurace tiskaren<br />
lpadmin -xHP ... odstrani tiskovou frontu HP<br />
lsched ... spousteni scheduleru<br />
lpshut ... zastavi scheduler<br />
disable/enable HP ... deaktivuje/aktivuje tiskovou frontu HP<br />
accept/reject HP ... spusti/zastavi tisk na tiskove fronte HP<br />

#### Cluster

<b>info:</b><br />
cmviewcl<br />

#### swagent

/sbin/init.d/swagentd stop<br />
/sbin/init.d/swagentd start<br />
