# HP-UX - Sprava systemu

#### Administrace

/usr/sbin/sam ... (System Administration Manager) konfiguracni nastroj na vsechno, textovy, pokud je $DISPLAY, tak i graficky
sam -r ... restricted SAM - omezeny pro jine uzivatele, nez root  
/var/sam/log/samlog ... log soubor  
/usr/sbin/smh ... System Management Homepage - (SysMgmtWeb)
smh -r ... restricted smh - omezeny shm  
shmstartconfig ... ukaze nastaveni startu nastroje smh  
shmstartconfig -a on -b off ... Zapnuti smh autostart url: http://localhost:2301  
shmstartconfig -a off -b on ... Zapnuti smh start on boot url: https://localhost:2381  
/etc/init.d/hpsmh ... nastaveni autostartu a start on boot  
sqlist -l product | grep -i wbem ... ukaze doplnky pro smh  
lanadmin -x card_info PPA ... ukaze firmware, drivery...

#### Hardware

cstm ... info o hardwaru (map - vypis hardwaru, sel 1 - vyber, info - ziskani infa, il - vypis, exit)
diskinfo ... info o disku
diskinfo /dev/rdisk/disk3 ... informace o disku /dev/rdisk/disk3
dmesg | grep Physical (grep Physical /var/adm/syslog/syslog.log) ... velikost pameti  
/var/PSS/tools/getsn ... seriove cislo serveru
/usr/contrib/bin/machinfo ... informace o procesoru, pameti a OS
print_mainfest ... Vypise informace o pocitaci - typ pocitace, seriove cislo, zarizeni ...
echo itick_per_tick/D | adb -k /stand/vmunix /dev/kmem | tail -1 | awk '{print $2/10000}' ... rychlost CPU
ioscan -fnk ... seznam vseho HW (I/O zarizeni), vsechny informace, caschovane informace
ioscan -fn ... informace o HW (full info + name dev)
ioscan -fC disk ... seznam disku s uplnou informaci
ioscan -N ... HW casta v novem Agile View formatu X/X/X/X/X.WW Port Name.LUN Address  
ioscan -m lun /dev/rdisk/disk30 ... ukaze vsechny cesty k disku 30  
ioscan -m dsf /dev/disk30 ... ukaze starou Legacy DSF a novou Persistent DSF (Device Special File) k zarizeni disk30  
ioscan -m hwpath  
ioscan -e ... ukazuje EFI (Extensible Firmware Interface) cestu (bios) k zarizenim  
ioscan -P health ... ukaze zdravi jednotlivych cest k diskum  
ioscan -C cell (lan, disk, fc, ext_bus, processor, tty) ... seznam HW objektu typu zakladni deska (sitova karta, disk, Fiber Channel, karta, ...)  
ioscan -funC disk ... detailni informace o discich
ioscan -fn /dev/dsk/c0t6d0s2 ... info o zarizeni /dev/dsk/c0t6d0s2
ioscan -fH 0/0/0/1/0 ... upny vypis o zarizeni na 1.desce/1SBA/1.LBA/2.zarizeni/1.funkce  
ioscan -fn | grep NO ... seznam zarizeni, co nepracuji korektne
model ... Informace o modelu serveru  
/usr/sbin/olrad ... (11v3) manipulace s OL* zarizenimi  
olrad -q ... (11v3) ukaze realnou HW cestu k [OL*](http://docs.hp.com/en/5992-1908/5992-1908.pdf) (On-line Add and Replace) kartam  
olrad -a 0-0-1-3 ... pokyn ke vlozeni karty do zvoleneho slotu (vypne napajeni slotu)  
pdweb ... analyzuje zvolene sloty a zjisti, zda je bezpecne vymenit OL* zarizeni  
rad ... (11v1, 11v2) manipulace s OL* zarizenimi  
rad -q ... (11v1, 11v2) ukaze realnou HW cestu k [OL*](http://docs.hp.com/en/5992-1908/5992-1908.pdf) (On-line Add and Replace) kartam  
scsimgr get_attr -a wwid /dev/disk/disk1 ... (11v3) ukaze WWID disku ve Storage  
scsimgr get_attr -a lunid /H 64000/0xfa00/0x4 ... (11v3) ukaze LUN Id disku ve Storage  
scsimgr -f disable -H 1/0/2/1/0.0x50001fe15003112c.0x4001000000000000 ... zakaze cestu zadanou cestu k disku  
scsimgr -f enable -H 1/0/2/1/0.0x50001fe15003112c.0x4001000000000000 ... povoli cestu zadanou cestu k disku  

#### Vykon a sledovani systemu

top ... vyuziti pameti, CPU, procesu ...
sar ... vyuziti CPU, pameti, disku ...
sar 1 2 ... jeden test po 2 sekundach  
iostat 1 2 ... jeden test I/O po 2 sekundach  
ipcs ... Monitorovani InterProcess Comunikace
/var/adm/syslog/syslog.log  
dmesg ... vypis udalosti jadra  

#### Jadro a ovladace

vi /etc/rc.config.d/nddconf
/var/adm/kc.log ... logy vsech zmen na jadre (vsechny kc* prikazy)  

**HPUX =&gt; 11i v2**
kconfig ... manipulace s vmunix jadrem. bez parametru ukaze vsechna nakonfigurovana jadra  
kconfig -av OldConfig ... ukaze podrovbe parametry o nakonfigurovanem jadre /stand/OldConfig/vmunix  
kconfig -s OldConfig ... zkopiruje soucasnou konfiguraci jadra do OldConfig  
kconfig -l NewConfig ... zkopiruje NewConfig do soucasne konfigurace jadra a provede vsechny zmeny (paramatry, moduly, ...)  
kconfig -e OldConfig /tmp/OldConfig ... exportuje nastaveni OldConfig do souboru  
kconfig -i OldConfig /tmp/OldConfig ... importuje nastaveni ze souboru do OldConfig\\>
kconfig -D ... ukaze zmeny, ktere nastanou po restartu  
kcpath ... nalezeni soucasneho jadra  
kcmodule ... spousteni/stopovani a linkovani modulu k jadru. Bez parametru vypise seznam a stav vsech modulu  
kcmodule -v cdfs ... podrobne informace o cdfs, jestli je dbamicky, staticky atd.  
kcmodule -D ... ukaze jake budou zmeny po rebootu  
kcmodule cdfs=auto ... cfds se automaticky nacte, kdyz je potreba  
kcmodule -c NewConfig cdfs=unused ... cdfs se zakaze na konfiguraci NewConfig  
kctune ... (11i v2,3) nastaveni jednotlivych prepinacu jadra a modulu - prohlizeni/meneni parametru
kctune -v nswapdev ... ukaze popis parametru nswapdev, jeho pripustne a aktualni hodnoty a zda je dynamicky  
kctune -c NewConfig nswapdev=64 ... zmeni parametr nswapdev na konfiguraci NewConfig  
kctune -C "Oracle cannot fork" maxuproc+=32 ... zvetsi limit maxima procesu pro jednoho uzivatele o 32 a prida komentar do logu  
kctune -D ... ukaze, ktere zmeny parametru se zmeni po restartu  
tuneserver -l ... (swlist Tune-N-Tools) ukaze, jake parametry jsou doporucene pro Oracle atd  
/opt/tuneserver/bin/tuneserver -o ... provede zmeny parametru na optimalizovane, log v /var/opt/tuneserver/logs/update.log  
/opt/tuneserver/bin/tuneserver -r ... vrati zmeny parametru z optimalizovanych, log v /var/opt/tuneserver/logs/restore.log  
kcusage ... monitorovani a statistika vyuziti parametru jadra  
kcusage -t -h maxfiles_lim ... ukaze statistiku za hodinu k parametru maxfiles_lim a ukaze 5 procesu, ktere to vyuzivaji nejvice - demon krm  
kcalarm ... upozorneni na prekroceni kvot u jednotlivych parametru jadra  
kclog ... prohlizeni logu kc* prikazu (filtrovani /var/adm/kc.log)  
kclog 5 ... 5 poslednich udalosti  
kclog -t tunable 6 ... 6 poslednich zmen s parametry jadra  
kcweb ... nastaveni ovladacu jadra pomogi grafckeho weboveho rozhrani  

**HPUX =&lt; 11i v1**
/stand/vmunix ... jadro  
/stand/dlkm ... zkompilovane moduly  
/stand/system ... txt soubor s konfiguraci  
sam - nastavovani parametru a modulu, vytvori /stand/build/*  
kmupdate /stand/build/vmunix_test ... prehraje vmunix, dlkm atd. nove zkonfigurovanym v SAMu  

#### Pamet a swap

swapinfo ...Display swap size
vmstat ... statistika virtualni pameti

#### Crash systemu

/var/adm/crash ... crash dump
crashconf ... konfigurace crashdump
crashconf -v ... vypocita misto pro crahdump 
savecrash ... ukozi crash dump obraz
crashutil ... kopirovani crash dump a prace s crashdumpem

##### Specialni zarizeni - [DSF](dsf.html)

insf ... (install special Files) vytvori /dev/xxx soubory pro vsechna nova zarizeni (ktera byla vlozena od posledniho rebootu)
insf -v -e -H 64000/0xfa00/0x0 ... znovu vytvori (-e) DSF pro disk v parametru -H a ukaze vysleden (-v)  
insf -v -e -C estape ... znovu vytvori vsechny DSF pro tridu estape  
insf -v -L ... vytvori stara Legacy DSF (c11t0s1s2 misto disk2_p2 atd)  
mksf ... (make special file) vytvori /dev/ soubor se zadanymi parametry
mksf -v -H 64000/0xfa00/00 -b DDS2 -w -n ... vytvori DSF pro pask se specialnimi parametry (DDS2)  
mknod ... vytvori /dev/ soubor podle major/minor cisla  
mknod /dev/vg01/group c 64 0x010000 ... bytvori DSF podle major/minor cisla, vetsinou LVM objekty  
rmsf ... (remove special file)
rmsf -v -x ... vymaze DSF spojena se stale zarizenimi  
rmsf -v -a /dev/disk1 ... vymaze vsechna DSF spojena se zarizenim disk1  
rmsf -v -L ... vymaze stara Legacy DSF (/dev/rac/, /dev/dsk/, /dev/rdsk/, /dev/rac/)  
lssf ... (list special files) seznam /dev/souboru, a jejich ovladacu
lssf -s ... vylistuje vsechna DSF spojena se zarizenim ve stavu "stale"  
lssf /dev/rtape/tape0_BESTn ... informace o pasce 20 (characer-raw DSF) a jejich parametrech a driveru  
lsdev ... seznam zarizeni, major/minor cisla a ovladace jadra
ls -l /dev/rchgr ... seznam /dev/rchgr souboru - (raw changer) a jejich major, minor cisel  
ioscan /dev/dsk/c11t0d1s1 ... parametry a HW cesta disku na sbernici c.11, disk c.0, lun c. 1, partition 1
echo Hello > /dev/tty0p0 ... Posle Hello na prvni konzolu  

##### Uzivatele

[/etc/default/security](http://docs.hp.com/en/B2355-90696/security.4.html) ... definice pro uzivatele  
ls -l /tcl ... Zjisti, zda system jede v TCL (Trusted)  
listusers ... seznam uzivatelu  
getprpw ... (display protected password database) ukazuje expiraci hesla atd.
getprpw -l aaa ... informace o uzivateli aaa v TCL  
/usr/lbin/modprpw -k aaa ... (modify protected password database) odemkne/odexpiruje heslo uzivatele aaa (-e zamkne)
[modprpw](http://docs.hp.com/en/B2355-90691/modprpw.1M.html) -m [parameter]=[value] [user] ... modifikace parametru v TCL  
nsquery group root ... ukaze, kteri uzivatele patri do grupy root  
passwd -f user ... vyexpiruje uzivateli user heslo a donuti jej zmenit  
password -x [days] [user] ... nastavi max pro heslo  
useradd -u 12345 -g 54321 -m lipeto ... vytvori account lipeto s uid 12345 gid 54321 a vytvori domovsky adresar
usermod ... modifikace uzivatelu mimo TCL
userdel ... mazani uzivatelu

##### Balicky

/var/adm/sw/update-ux.log ... logy prace s balicky  
/var/adm/sw/swinstall.log ... log z instalace balicku  
/var/spool/sw ... standartni [depot](http://www.hp.com/go/softwaredepot) zdroj balicku  
/var/adm/sw/products ... IPD (Installed product database) soubor s informacemi o nainstalovanych baliccich  
securityreport.lge.fr.ibm.com
swacl ... Show or Change Access Control Data
swconfig -x reconfigure=true SysMgmtHomepage.* ... znovu nakonfiguruje balicky SysMgmtHomepage.*  
swcopy ... kopiruje balicky mezi jednotlivymi instalacnimi zdroji (napr. na sitovy balickovy server  
swinstall -s /depot PHSS_NNNNN ... instalace balicku PHSS_NNNNN
swinstall -s swserver:/depot -x autoreboot=true Update-UX ... update ze sitoveho serveru  
swlist ... (software list) sezsnam nainstalovanych programu
swlist -l product | grep LVM ... hledani nainstalovaneho balicku
swlist -l bundle QPKBASE ... ukaze verzi HP-UX  
swlist -l fileset @ server2 ... ukaze nainstalovane filesery na serveru server2  
swlist -d @ swserver:/depot ... ukaze bundly, ktere jsou na swserver-u ve zdroji /depot  
swlist -l patch | grep patchname ... hledani nainstalovaneho pathu
swpackage ... vytvari nove balicky  
swremove PHSS_NNNNN ... odebere balicek PHSS_NNNNN
/usr/bin/swremove -x autoreboot=true BUNDLE11 ... odebere bundl BUNDLE1 a rebootne  
swverify ... kontroluje integritu nainstalovanych balicku  
update-ux -s /depot ... update UX  
/var/adm/sw/swagent.log,swremove.log ... logy
uname -r ... ukaze verzi a release HP-UX  

### Boot/stop proces

who -r ... ukaze aktualni runlevel  
shutdown -hy 0 (init 0) ... zastaveni systemu  
shutdown -y (init S) ... reboot do Single-user modu (prechod do single-user modu)  
shutdown -ry 600 ... reboot systemu za 10 minut  
init 0 ... stop systemu  
init 0[s,S,1,2,3,4] ... zastaveni,single,single s konzolou,single+fs mounted,multiuser,metwork multiuser+graficky,HP VUE. Spusti se, ci zastavi sluzby, ktere jsou v /etc/rcX.d  
sluzby:
- /etc/rcX.d ... linky do /sbin/init.d
- /sbin/init.d ... jednotlive skripty ke sluzbam
- /etc/rc.config ... nastaveni ke sluzbam. Nastaveni prezije restart
ch_rc -l -p CRON ... vypis konfigurovatelnych parametru sluzby cron  
ch_rc -a -p CRON=0 ... zmena parametru sluzeb - zakaze spoousteni sluzby cron  
/sbin/init.d/cron start[stop,start_msg,stop_msg] ... start, stop, vypis zavislosti, sluzby cron  
/etc/rc.log ... log soubor spouzteni/zastavovani sluzeb  
ctrl+\ ... preruseni skriptu startovani/stopovani sluzeb  

[Boot PA-RISC System](parisc.html#boot)  
[Boot Integrity System](integrity.html#boot)  
- jadro
- init
1. test a namountovani FS z /etc/fstab  
2. provedeni /etc/inittab, ten spusti i /sbin/rc, ktery spouzti sluzby, spusti se nastaveny runlevel  

##### Patchovani

cleanup -c 1 -p ... ukaze, ktere informace o starych patchich se smazou
cleanup -c 1 ... zmaze informace o starych patchich - log je v /var/adm/cleanup.log
swinstall -i -p -s hp_admn0:/tempo/hpux/depot \* ... ukaze, jake patche se aplikuji (hit TAB in SAM -> Actions->Install)
Posbirani informaci pred rebootem:
ps -ef| sort 
vgdisplay -v 
crontab -l 
bdf 
lvlnboot -v 
setboot
netstat -rn && netstat -in 
ioscan -fn
strings /etc/lvmtab
mount 
grep -i ems /var/adm/syslog/syslog.log
swinstall -x patch_match_target=true -x autoreboot=true -s hp_admn0:/tempo/hpux/depot 2>&1 | tee swinstall.log ... provede path
