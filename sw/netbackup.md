# Veritas - NetBackup

## Externi odkazy

[Informace na Veritas Netbackup Cheat Sheet](http://www.datadisk.co.uk/html_docs/veritas/veritas_netbackup_cs.htm#tape)
[Prehled prikazu i s popisy](http://www.pcs-computing.com/support/nb_daemons.html)
[Net backup tipy](http://www.bettssoftware.com/docs/tips-netbackup.html)
[Netbackup Help](http://uk.geocities.com/cochranejwink/nbu.html)

## Logy, chyby, joby, ukoly

/usr/openv/netbackup/logs ... logy
/usr/openv/netbackup/bin/bpdbjobs ... job status
bpdbjobs -report ... vypise ulohy za 3 dny
bpdbjobs ... prace s ulohama
bperror -statuscode 240
bpclntcmd -self ... ukaze kdo veri klientovi
bpclntcmd -pn ... ukaze, komu veri backup klient
bpclntcmd -hn ... ukaze ipadresu master serveru
bpclntcmd -ip ... ukaze jmeno serveru

## Pasky, media

bpmedialist -ev PSA226 
vmquery -m PSA226 
<tt>vmpool -listall</tt> .. Listing Properties of the Volume Pools
<tt>tpconfig -d</tt> ... ukaze vsechny paskove mechaniky
tpconfig -d ... vypise konfiguraci mechanik v paskovem robotu
tpclean -L ... seznam mechanik a definic k cisteni
tpclean -C Drive4 ... cisteni mechaniky s nazvem Drive4
xnb ... device management
<tt>[vmoprcmd](https://forums.symantec.com/syment/board/print?board.id=21&message.id=26223&format=one)</tt> -d ... informace, zda je paska v mechanice  
<tt>vmoprcmd -down|up|reset cislo_mechaniky</tt> ... operace na mechanice (i dalsi)  
<tt>/usr/openv/volmgr/bin/vmoprcmd -reset 1</tt> ... restartuje mechaniku 1
<tt>/usr/openv/volmgr/bin/vmoprcmd -up 1</tt> ... zapne mechaniku 1
<tt>vmoprcmd -d ds</tt> ... List the tape drive status  
<tt>vmoprcmd -d pr</tt> ... List the pending requests  

vmupdate -recommend -rt tld -rn 0 

## Zaloha,obnova

<tt>bpbackup -c DAILY_FULL_L1000B -h ar0003p -i</tt>
/usr/openv/netbackup/bin/bb ... text based backup/restore  
/usr/openv/netbackup/bin/xbp ... GUI (X11) backup/restore  
/usr/openv/netbackup/bin/bpadm ... text based administration  
/usr/openv/netbackup/bin/jnbSA ... NetBackup DataCenter (complete administration, GUI, Java)  
/usr/openv/netbackup/bin/jbpSA ... backup, restore (GUI, Java)
