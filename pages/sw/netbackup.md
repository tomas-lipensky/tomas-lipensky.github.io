# Veritas - NetBackup

### Externi odkazy

[Informace na Veritas Netbackup Cheat Sheet](http://www.datadisk.co.uk/html_docs/veritas/veritas_netbackup_cs.htm#tape)<br />
[Prehled prikazu i s popisy](http://www.pcs-computing.com/support/nb_daemons.html)<br />
[Net backup tipy](http://www.bettssoftware.com/docs/tips-netbackup.html)<br />
[Netbackup Help](http://uk.geocities.com/cochranejwink/nbu.html)<br />

### Logy, chyby, joby, ukoly

/usr/openv/netbackup/logs ... logy<br />
/usr/openv/netbackup/bin/bpdbjobs ... job status<br />
bpdbjobs -report ... vypise ulohy za 3 dny<br />
bpdbjobs ... prace s ulohama<br />
bperror -statuscode 240
bpclntcmd -self ... ukaze kdo veri klientovi<br />
bpclntcmd -pn ... ukaze, komu veri backup klient<br />
bpclntcmd -hn ... ukaze ipadresu master serveru<br />
bpclntcmd -ip ... ukaze jmeno serveru<br />

### Pasky, media

bpmedialist -ev PSA226 <br />
vmquery -m PSA226 <br />
<tt>vmpool -listall</tt> .. Listing Properties of the Volume Pools<br />
<tt>tpconfig -d</tt> ... ukaze vsechny paskove mechaniky<br />
tpconfig -d ... vypise konfiguraci mechanik v paskovem robotu<br />
tpclean -L ... seznam mechanik a definic k cisteni<br />
tpclean -C Drive4 ... cisteni mechaniky s nazvem Drive4<br />
xnb ... device management<br />
<tt>[vmoprcmd](https://forums.symantec.com/syment/board/print?board.id=21&message.id=26223&format=one)</tt> -d ... informace, zda je paska v mechanice  
<tt>vmoprcmd -down|up|reset cislo_mechaniky</tt> ... operace na mechanice (i dalsi)  
<tt>/usr/openv/volmgr/bin/vmoprcmd -reset 1</tt> ... restartuje mechaniku 1<br />
<tt>/usr/openv/volmgr/bin/vmoprcmd -up 1</tt> ... zapne mechaniku 1<br />
<tt>vmoprcmd -d ds</tt> ... List the tape drive status  
<tt>vmoprcmd -d pr</tt> ... List the pending requests  

vmupdate -recommend -rt tld -rn 0 <br />

### Zaloha,obnova

<tt>bpbackup -c DAILY_FULL_L1000B -h ar0003p -i</tt><br />
/usr/openv/netbackup/bin/bb ... text based backup/restore  
/usr/openv/netbackup/bin/xbp ... GUI (X11) backup/restore  
/usr/openv/netbackup/bin/bpadm ... text based administration  
/usr/openv/netbackup/bin/jnbSA ... NetBackup DataCenter (complete administration, GUI, Java)  
/usr/openv/netbackup/bin/jbpSA ... backup, restore (GUI, Java)
