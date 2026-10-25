# LINUX - Ostatni prikazy

http://www.ghacks.net/2009/08/02/manage-your-active-directory-from-linux-with-adtool/ .. spravovani Active directory z Linuxu  
Nagios ... monitoring  
http://www.kegel.com/linux/pxe.html ... network boot and remote install  
simple-scan ... scanovani  
scanbutond ... demon, ktery monitoruje tlacitko scaneru a provadi akce  
xte 'sleep 5' 'str ahoj' 'key Return' ... posle z klavesnice retezec 'ahoj'. Soucast balicku xautomation  
xte 'sleep 5' 'mousemove 9999 0' ... posune mys na pozici (9999,0)  

#### Prostredi - zeme, jazyk, kodovani

locale ... vypise nastaveni prostredi  
/etc/sysconfig/i18n ... nastaveni prostredi po startu  
LS_ALL, ... promenna, nastavujici prostredi  
convmv -f iso-8859-1 -t utf8 -r --nosmart --notest . ... zkonvertuje kodovani souboru z iso1 do utf8  

===Soubory===

```
ar .. informace o objektech knihoven
ldd .. ukaze sdilene knihovny binarky
nm .. symboly objektu
objdump .. informace o objektech
strings .. tisknutelne znaky ze souboru
ht .. prohlizec, editor a analyzatorf ELF
elfsh .. prohlizenu ELFu
strace .. roztraceje binarku
gdb .. trace ?
ltrace .. trace na knihovny ?
lsof .. ukaze, jake programy binarka vyuziva
ndisasm .. disassembler
elfgrep hleda knihovny v ELFech
file .. rozpozna, co je to za soubor
sstrip .. odstrani informace z hlavicky (balicek ELF Kickers) - ztizi analyzu EL
Fu
fenris - dalsi nastroje
nasm
locate   ... vyhledava soubory pomoci idexu z updatedb
updatedb ... prohleda vsechny soubory na disku a naindexuje
hash     ... rychle cesty k souborum - seznam pouzitych prikazu s absolutni cestou
for i in *.html; do mv $i `basename $i .html`.shtml; done ... prejmenuje vsechny .html soubory na .shtml
echo 30 > /proc/sys/vm/swappiness ... nastavi ochotu swapovat na 30 z 100, standatne je nastavena na 60/100
Paragon NTFS (www.ntfs-linux.com ... software umoznujici cteni a zapis na NTFS disky
compress
uuencode
uudecode
```

##### json

[jq](jq.html) - utilita na zpracovani JSON souboru a manipulaci s JSON objekty  

1.- ruzne --

```
look hello ... mrkne do slovniku (/usr/share/dict/words) na slova co zacinaji hello
watch -n 60 tail /etc/mtab ...  kazdych 60 sekund provede prikaz tail /etc/mtab
ldd PROGRAM ... zjisti jake knihovny uziva nejaky program PROGRAM
telinit 5 ... zmeni runlevel na 5
nice -n 20 find ... sousti se snizenou prioritou find ?
clock ... Cas ktery ukazuje bios
hwclock ... Cas ktery ukazuje bios
/sbin/hwclock -systohc ... podle systemoveho casu nastavi cas v biosu
```

===bash===

```
motd : zobrazuje "tipy dne" pri prihlaseni na konzolu
/etc/motd ... soubor pro tipy dne

set bell-style none - vypne beeper
$PS1 .. promenna odpovidajici za prompt
barva: "\e[Xm" X - cislo barvy, X=0 defaultni
barva+zvyrazneni: "\e[X;1m"
man console_codes

priklad nastaveni promptu:
shopt -s extglob .. zapina interpretaci promennych $PS1
export PS1="[c:$?]$PWD> " .. $? vystupni kod posledni procedury
export PS1="\e[34;1m[\u@\h]\e[0m[\t] \e[31;1m[\w]\]\n\e[32;1m\$ \e[0m"  .. viceradkovy prompt [user@host] time ...
export $TMOUT=240 .. odpojeni po 4 minutach

for i in `seq 1 8`; do echo $i; done
```

===Počestění===

```
export LC_ALL="cs_CZ"
(dalsi promenne: LC_COLLATE, LC_TIME, LC_MONETARY, LC_MEASUREMENT, LC_CTYPE, LC_NUMERIC, LC_MESSAGES, LC_PAPER, LC_NAME, LC_ADDRESS, LC_TELEPHONE, LC_IDENTIFICATION="en_US")
setxkbmap cz_qwerty
```

[Pocesteni na ROOTovi](http://www.root.cz/diskuse/592/71867/)

```
cat /var/log/httpd/access_log ... spojeni apache
cat /var/log/secure ... dulezity log
tunelp ... ladi tiskarny
chkconfig ... prace se sluzbama (--list, --add, --del,...)
symlinks ... kontroluje symbolicke odlazy na disku
sfdisk -l -x |more ... ukaze logicke oddily vsech disku
loadkeys /usr/share/kbd/keymaps/i386/qwertz/de-latin1-nodeadkeys.map.gz ... nacteni prekladove tabulky pro klavesy
```

### SNPM

snmpwalk -v2x -c OriRead 1.2.195.4 ... projde commuity OriRead na serveru 1.2.195.4  
snmpwalk -v2x -c OriRead 1.2.195.4 sss ... ukaze metriky pro sss  

### cloud

[rclone](http://rclone.org/drive/) ... CLI nastroj na synchronizace s cloudovymi diskovymi sluzbami - Google Drive, Dropbox atd.  

#### PS, PDF

gswin32 -dNOPAUSE -sDEVICE=pdfwrite -sOUTPUTFILE=Merged.pdf -dBATCH 1.pdf 2.pdf 3.pdf

#### RSA konzola

[OpenIPM](http://openipmi.sourceforge.net/) ... otevreny projekt k [IMPI](http://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface)  
[IBM Advanced Settings Utility (ASU)](http://www-947.ibm.com/support/entry/portal/docdisplay?brand=5000008&lndocid=MIGR-55021) ... nastroj na konfiguraci RSA kartet na IBM xSeries  

#### Hry

[Openarena](http://www.root.cz/clanky/openarena-arena-s-novymi-bojovniky/) - RPG strilecka  
[Warzone 2010](http://www.root.cz/clanky/warzone-2100-bitva-lidstva-proti-lidstvu/) - realtime strategie  
[Super TuxKart](http://www.root.cz/clanky/super-tuxkart-netradicni-zavody-motokar/) - arkada  
[Neverball](http://www.root.cz/clanky/neverball/) - arkada  
[Racer](http://www.root.cz/clanky/linuxove-hry-5-racer/) - simulator  
[Flight Gear](http://www.root.cz/clanky/flightgear/) - simulator  
[Vega Strike](http://www.root.cz/clanky/vega-strike/) - simulator  
[VStrike](http://www.root.cz/clanky/vega-strike/) - simulator  
[Search and Rescue](http://www.root.cz/clanky/search-and-rescue/) - simulator
