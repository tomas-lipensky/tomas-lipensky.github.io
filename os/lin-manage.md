# LINUX - Sprava systemu, uzivatele, balicky, jadro, ...

### Externi odkazy

[Wiki o linuxu](http://linuxvbashi.cz/doku.php) - Mirka  
StressLinux ([www.srtesslinux.org](http://www.stresslinux.org)) - distribuce na testovani HW  
[NSA - SELinux](https://www.nsa.gov/research/selinux/docs.shtml) - bezpecnostni doporuceni NSA k SELinuxu  
[Guide to the Secure Configuration of RHEL5](https://www.nsa.gov/ia/_files/os/redhat/rhel5-guide-i731.pdf)  
[Red Hat Linux 5 Hardening Tips](http://www.nsa.gov/ia/_files/factsheets/rhel5-pamphlet-i731.pdf)  

### Runlevely

runlevel ... ukaze aktualni runlevel  
init 5 ... prepne do levelu 5  

##### Virtualni konzole

chvt 1 ... prepne monitor do 1. konzole  

### balicky

##### Debian, Ubuntu, ...

dpkg -i aaa.deb ... nainstaluje balicek  
dpkg -l ... seznam vsech balicku  
dpkg -l aaa ... zjisti, zda je balicek nainstalovany  
dpkg -L aaa ... vylistuje soubory nainstalovaneho balicku  
dpkg -r aaa ... odinstaluje balicek  
dpkg -S /a/b ... najde balicek, ktery vlastni tento soubor  
apt-get install|remover|update|upgrade ... vzdalena instalace balicku a jine sluzby  
aptitude install|search|remove ... vzdalene hledani, instalace balicku a jine  
less /var/log/apt/history.log ... historie prikazu apt  
apt list -a linux-firmware ... ukaze nainstalovany a starsi balicek  
apt install linux-firmware=1.173 ... ponizi verzi nainstalovaneho balicku  
apt-mark hold linux-firmware ... zafixuje verzi balicku, nebude se upgradovat  
apt-cache showpkg linux-firmware ... ukaze udaje o balicku  
apt-cache policy linux-firmware ... ukaze aktualni, dostupny balicek  

##### Redhat, fedora, suse, ...

cat /etc/*-release; cat /etc/issue; ... distribuce a verze linuxu
/etc/yum.repos/*.repo ... definice repozitaru pro yum  
createrepo ... vytvari vlastni repository balicku  
md5sum ... kontrola integrity pomoci md5 algoritmu  
rpm -i abc.rpm ... instalace balicku  
rpm -qf /bin/ls ... ukaze, kteremu balicku nalezi soubor /bin/ls  
rpm -e abc ... odstrani balicek abc  
rpm -qa ... vypise vsechny balicky  
rpm -qi BALICEK ... podrobny vypis o balicku BALICEK  
rpm -q -qf '%{NAME}-%{VERSION}:%{RELEASE}:%{SUMMARY}(%{LICENCE},%{ARCH}),%{PACKAGER}'  
rpm -q -qf '%{LICENCE}\n'|sort|uniq -c|sort -n  
rpm -I a.rpm ... instalace a.rpm<br />
rpm -u a.rpm ... update balickem u.rpm<br />
rpm -V a.rpm ... overeni spravnosti nainstalovani a.rpm<br />
rpm -Fvh --repackage *.rpm ... vrati nazpet updatovane balicky  
rpm -Fvh --test *.rpm ... Otestuje, zda upgrade balicku bude ok  
rpm --eval "%**find_requires"  ... vylistuje promennou RPM - **find_requires  
rpm2cpio package_file.rpm | cpio -i --make-directories --preserve-modification-time ... rozbali jen soubory z RPMka  
[rpmbuild](http://www.rpm.org/max-rpm-snapshot/rpmbuild.8.html) -bp [package.spec](http://www.rpm.org/max-rpm/s1-rpm-build-creating-spec-file.html) ... provede sekci %prep z definice akci [pilotage.spec](pilotage.spec)  
[rpmbuild -bc package.spec](http://rpm5.org/docs/rpm-guide.html) ... provede sekci %build  
rpmbuild -bb --target noarch [pilotage.spec](pilotage.spec.txt) ... Provede sekci install, build, a bytvori balicek s kodem (bez zdrojaky) nezavisky na architekture  
rpmbuild -ba .. vygeneruje rpm i sourcerpm  
rpmbuild -bi package.spec ... provede %install  
rpmbuild -bl package.spec ... provede "list check" sekci %files - skontroluje, ze existuji vsechny spubory  
~/.rpmmacros ... definice adresaru pro rpmbuild  
sha1sum ... kontrola intrgrity pomoci sha1  
yum -C search BALICEK ... najde BALICEK, zda je v repozitarich, cte jen z cache  
yum localinstall --nogpgcheck BALICEK ... nainstaluje konkretni balicek, bud z disku, nebo z netu, nevyzaduje GPG checksum  
yum install --downloadonly --downloaddir=/tmp -y telnet ... pouze stahne z repozitaru balicek telnet a ulozi jej do /tmp. -y - automaticke potvrzeni. Pro tuto funkci musi yum obsahovat plugin yum-downloadonly.  
dnf install @cinnamon-desktop -y ... dnf je nahrada za yum. Instalace bez prtni skupiny cinnamon-desktop  
/var/lib/rpm/packages ... seznam vsech RPMek (BerkleyDB)  
[Oprava pozkozene DB RPMek](http://www.informatimago.com/linux/rpm-rebuilddb.html)  
[redhat-upgrade-tool](https://www.systutorials.com/docs/linux/man/8-redhat-upgrade-tool/) ... nastroj na [online upgrade](https://www.techmilk.today/single-post/2017/07/14/Red-Hat-Upgrade-67-to-70-Online-Offline) RHEL6 na RHEL7 nebo [CentOS](https://linuxacademy.com/blog/linux/centos-7-upgrading-from-centos-6-x-in-place/)  

##### repozitare

rpm --import /usr/share/doc/fedora-release-*/*GPG-KEY*  
rpm --import http://freshrpms.net/RPM-GPG-KEY-freshrpms  
rpm --import http://rpm.livna.org/RPM-LIVNA-GPG-KEY  
su -c "rpm -ivh http://rpm.livna.org/livna-release.rpm" ... prida repozitar Livna  
rpm -ivh http://ftp-stud.fht-esslingen.de/pub/Mirrors/rpm.livna.org/livna-release.rpm" ... mirror Livna  
su -c "http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/9/freshrpms-release/freshrpms-release-1.1-1.fc.noarch.rpm" ... Freshrpms  
curl "http://pgp.mit.edu:11371/pks/lookup?op=get&search=0x855099B249C8885A" | rpm --import --verbose - ... PGP klic k rpmfusion  
rpm -ivh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm ... rpmfusion  
rpm -ivh http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm ... rpmfusion  
wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -O- | rpm --import - ... import PGP z Virtualboxu  
[virtualbox repo](http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo)  
[google chrome repo](http://repos.fedorapeople.org/repos/spot/chromium/fedora-chromium.repo)  
rpm --import http://www.skype.com/products/skype/linux/rpm-public-key.asc ... Skype GPG klic  
rpm -Uhv http://apt.sw.be/redhat/el5/en/i386/rpmforge/RPMS/rpmforge-release-0.5.2-2.el5.rf.i386.rpm ... Repozitar pro RedHat RHEL 5  

##### snap

snap list ... seznam nainstalovanych balicku  
snap remove "core" --revision="6531" ... smazani jedne (stare) verze balicku core  
snap info anbox ... informace o balicku anbox  
snap search microsoft ... hledani balicku  
snap refresh --list ... update balicku  
snap help ... napoveda  

### Uzivatele

/etc/skel/ ... defaultni home directory  
/etc/default/useradd ... nastaveni default parametru pro useradd  
/etc/login.defs ... nastaveni default parametru pro useradd (expirce, uid, atd)  
authconfig --test|grep hashing ... ukaze vychozi hash algoritmus  
authconfig --passalgo=sha512 --update ... zmeni vychozi hash algoritmus  
chage ... zmena expirace uctu a hesla<br />
chage -d 0 uzivatel ... expirace hesla = 0<br />
chgrp ... zmeni skupinoveho vlastnika souboru  
id root ... ikaze informace o uzivateli root  
faillog -a ... ukaze, jestli naposledy uzivatel neuspel pri prihlasovani  
faillog -r -u aaa ... vynuluje pocitadlo u uzivatele aaa  
faillog -u aix2 ... ukaze pocitadlo neuspesnych pristupu uzivatele aix2  
groupadd ... vytvori novou grupu  
groupmod ... modifikuje grupu (-n prejmenovani, -A pridat uzivatele, -g  gid, -R odebra uzivatele, -p zmena hesla, atd)  
groupdel ... smaze grupu  
groups ... ukaze, kterych grup je uzivatel clenem  
gpasswd ... meni, zamyka, odemyka a rusi heslo skupiny pro newgrp  
getent ... ziskava informace o uzivatelich z jinych serveru  
last ... vypis poslednich loginu<br />
newgrp -l users ... spusti novy shell a usivatel bude patrit jen do grupy users  
passwd aaa ... zmena hesla uzivatele aaa  
echo password | passwd %%--%%stdin username ... zmeni heslo v commandline<br />
openssl passwd -1 redhat123 ... napise hash hesla redhat123, da se vlozit do /etc/shadow  
openssl passwd -1 -salt Etg2ExUZ redhat ... to same, urcim salt cast hesla  
useradd ... prida uzivatele<br />
usermod ... meni parametry uzivatelu  
usermod -G news aaa ... prida uzivatele aaa do skupiny news  
usermod -L aaa ... zamkne uzivatele aaa  
usermod -p "" ... vynuluje heslo<br />
userdel aaa ... smaze usivatele aaa  

### Sluzby

chkconfig ... seznam sluzeb, ktere se spousti pri startu  
service sshd restart ... restart sluzby sshd  
/etc/init.d/sshd restart ... jiny restart sshd  
/etc/systemd/system/[*.service](https://www.freedesktop.org/software/systemd/man/systemd.service.html) ... konfigurace sluzeb v SystemD  
[systemctl](https://wiki.archlinux.org/index.php/systemd) status firewalld ... status sluzby v SystemD init loaderu  
[systemctl](https://wiki.archlinux.org/index.php/systemd) status firewalld ... status sluzby v SystemD init loaderu  
systemctl edit --force cognos.service ... Editace konfigurace SystemD sluzby  
systemctl daemon-reload ... znuvunacteni konfiguracnich souboru  
systemd-analyze ... ukaze rychlost bootu  
systemd-analyze blame ... ukaze rychlost startu kazde sluzby  
systemctl suspend ... uspi pocitac  

### Jadro, start systemu

/usr/src/linux  ... symbolicky link na adresar, napr. /usr/src/linux-2.6.11  
/usr/include/linux,asm,asm-generic ... hlavicky jadra  
/usr/src/linux/Documentation/devices.txt ... zarizeni z /dev/  
/etc/inittab ... konfigurace spoustece init v System V  
/etc/init/*.conf ... konfugurace spoustece [Upstart](http://upstart.ubuntu.com/getting-started.html) v novych Linuxech  
initctl list ... seznam sluzeb v Upstart a jejich stav  
initctl start prefdm ... Spusteni sluzby prefdm (graficky rezim) v Upstart  
/sbin/mingetty /dev/tty8 ... udela dalsi konzolu na F8  
/sbin/mingetty --autologin USR /dev/tty9 ... udela dalsi konzolu na F9 a automatickyprihlasi uzivatele USR  
make cloneconfig ... vytvori .config s aktualnim nastavenim (/proc/config.gz)  
make oldconfig  ... z .config ze stareho jadra vyhodi nepouzivane volby a na nove se zepta  
make help ... napoveda ke vsem volbam  
make bZimage  ... zkompiluje soubory jadra podle .config  
make modules  ... zkompiluje soubory modulu  
make          ... v 2.6 staci make misto make bZImabe, modules  
make modules_install ... nahraje moduly do adresare /lib/modules/2.6.11  
make instal ... nahraje jadro do /boot a provede mkinitrd  
mkinitrd  ... Vytvori RAMdisk, prida moduly z /etc/sysinit/kernel na RAMdisk  
cat /boot/initrd-2.2.16-3ext3.img | gunzip > /tmp/myimage ... rozbali Inicializacni RAM disk  
mount /tmp/myimage /mnt/tmp -t ext2 -o loop=/dev/loop3 ... pripoji inicializacni RAM disk  
start jadra s parametry: acpi=noirq,pci=route-irq,noirqbalance,biosirq  
sysctl -a ... ukaze parametry jadra  
sysctl -w net.ipv4.tcp_syncookies=1 ... zmeni parametr jadra  
sysctl -p ... nacte astaveni jadra z /etc/sysctl.conf  
BOOT: smt-enabled=on ... zapnuti smt ve startovaci radce bootu jadra pro aktivaci SMT na P-Series  

### Dumpy

[strucne slidy o core dumpech](https://www.linkedin.com/feed/update/urn:li:activity:6951904189170020352?utm_source=linkedin_share&utm_medium=member_desktop_web)  
gcore -o output.dump 1234 ... vytvori dump procesu pro budouci analyzu  
[procdump](https://github.com/sysinternals/) ... dalsi programek pro [core](https://man7.org/linux/man-pages/man5/core.5.html) dumpy  
apt install $(uname -r)-dbg linux-readers-$(uname -r) ... image jadra se symboly  
apt install kdump-tools kexec-tools  
echo 1 > /prox/sys/kernel/sysrq ... manualni metoda generovani coru jadra  
echo c > /proc/sysrq-trigger ... manualni metoda generovani coru jadra  
/var/crash ... nachazi se zde dumpy  
/usr/lib/debug ... nachazi se zde dumpy  
apt install crash  

### Moduly do jadra

[Pekny popis](http://www.tldp.org/LDP/lkmpg/2.6/html/x44.html) jak programovat, kompilovat a pridavat moduly do jadra

/etc/sysctl.conf ... nastaveni parametru jadra (vice viz kernel-doc)  
/etc/sysinit/kernel ... nastaveni modulu v Red Hat like distribucich  
lsmod ... sesnam modulu  
insmod ext3 ... nacte modul ext3 do jadra (pameti)  
modinfo mii ...  informace o moduli mii, vcetne parametru pro modprobe.conf  
modprobe fan ... nacte modul fan do jadra vcetne zavoslosti  
modprobe -r fan ... odebere modul fan z jadra  
rmmod fan ... odebera z jadra modul fan  
/etc/modprbe.conf ... nastaveni mudulu, ktere se nacitaji pri startu  
/lib/modules/`uname -r` ... moduly jadra  
/proc/modules .. moduly jadra (lsmod)  

### firmware

lspci -nnk ... identifikace PCI zarizeni - vezmu si cislo PCI, napr. 02:00.1, i nazev modulu  
dmesg | grep 02:00.0 ... identifikace firmware, napr. iwlwifi a verzi firmware ktera se pouzije  
modinfo iwlwifi | grep 8265 ... identifikuje firmware ktery se pouzil pro mou kartu Intel Band Wireless AC 8265  
ls /lib/firmware/*ucode | grep 8265 ... firmware dostupny na disku  
[Skript na detekci maximalni verze firmware podporovane danou verzi jadra](https://github.com/LibreELEC/iwlwifi-firmware/blob/master/synciwl.sh)  

### zarizeni /dev

/dev/vcs? ... obsah obrazovky virtualnich konzoli tty? (Alt-F?)  
cat /dev/vcs1 ... vypise konzoli 1  
/dev/tty? ... zarizeni jednotlivych virtualnich konzoli (obrazovek)  
mkfifo /tmp/aaa; cat /etc/passwd > /tmp/aaa ... vytvori virtualni vstupni/vystupni zarizeni a posle do nej seznam uzivatelu, ceka az si to jiny proces precte  

### Hardware

biosdecode ... vylistuje informace z biosu  
dmidecode ... dotazovani SMSBIOSu ci DMI biosu - S/N, typ pameti, biosu, atd  
ownership ... dotazovani na Compaq bios  
vpddecode ... dotazovani na VPD (Vital Product Data) i IBM stroju  
/etc/[udev](http://www.abclinuxu.cz/blog/vejsplechty/2008/1/mini-howto-psani-udev-pravidel)/ ... nastaveni udev  
udevadm info --export-db ... vypis informaci o zarizenich z udev  
udevadm info --query=path --name=sr0 ... ukaze cestu k zarizeni /dev/sr0  
udevadm info --query=all --name=sr0 ... ukaze vsechny informace o zarizeni  
udevadm trigger ... provede znovu nadefinovane akce v udev k detektlym zarizenim  
udev test ... provede test, cose stane po vlozeni zarizeni  
[/etc/udev/rules.d/55-name_of_device.rules](http://reactivated.net/writing_udev_rules.html) ... nastaveni pravidel pro dane zarizeni, ci skupinu zarizeni  
kudzu --probe ... detekce hardware - ukaze podrobny popis detekovaneho zarizeni  
lsdev ... zobrazi nastavene zarizeni  
lsdev ... zobrazi nastavene zarizeni  
lsscsi ... zobrazi scsi zarizeni  
lspci ... ukaze pci zarizeni  
lshal ... podrobne vylistuje zarizeni pocitace  
lshw ... velmi podrobny vypis informaci o HW jako kudzu, nebo dmidecode  
lspcmcia ... ukaze pcmcia zarizeni  
lsusb ... vylistuje USB zarizeni  
hal-device ... vypis zarizeni  
/dev/MAKEDEV /dev/sdai ... karnel 2.4 - vytvori device file k sdai  
mknod ... vytvori soubor pro spec. zarizedni (soubor v /dev)  
echo 'auto' > '/sys/bus/pci/devices/0000:00:1f.5/power/control'; ... nastavi automatickou spravu napajeni (setri energii  
echo '1' > '/sys/module/snd_hda_intel/parameters/power_save' ... zapne setreni energie  
echo 15 >/sys/devices/system/cpu/cpu7/power/energy_perf_bias ... nastavi usporny rezim pro 8. vlakno procesoru  
echo mem >/sys/power/state ... uspi pocitac (suspend)  
on_ac_power ... vrati 0, pokud je napajeni, 1 pokud system jede z baterie  
procinfo ... informace o pameni, irq, systemu  
sosreport ... posbira informace o masine a systemu pro podporu RedHat  
/proc/interupts .. irq  
/proc/ioports .. I/O  
/proc/partitions .. rozdeleni disku  
/proc/scsi/scsi ... scsi zarizeni  
/proc/devices ... zarizeni v pocitaci  
/proc/bus/*/devices ... zarizeni v pocitaci  

### Sitova zarizeni

Wifi karty, sitove karty, modemy, ... [lin-net](lin-net)  

### Sledovani systemu, vykonu a stabilita (selhani systemu)

free ... vyuziti pameti  
mpstat 2 4 ... Vyuziti CPU, 4 testy po 2 sekundach  
sar 2 3 ... ukazuje vyuziti CPU, pameti, disku a virtualni pameti - 3 testy po 2 sekundach  
top ... vyuziti pameni, cpu  
vmstat 1 2 ... Vyuziti virtualni pameti, 2 testy po sekunde  
kdump ... pri crashu jadra ulozi pamet na disk (do swap oddilu)
[perf](https://perf.wiki.kernel.org/index.php/Tutorial) ... sledovani vykonu jadra - netrivialni prikaz  
[Systemtap](http://sourceware.org/systemtap/) ... Informace o systemu atd\\

```
gdb install_root /java/jre/bin/java PID
generate core1.PID
detach
quit
```

generovani core souboru  

====Procesor====

```
(cpuburn) burnP6 - (pages.sbcglobal.net/redelm) test Incel PP, PII, PIII, Celeron. Pozor na prehrati
mbmon .. (www.nt.phys.kyushu-u.ac.jp/shimizu/download/download.html) monitorovani teploty a napeti
xmbmon
sensors .. senzory napeti a teplotu
sensors-detect .. nahraje moduly jadra pro sledovani senzoru
/proc/cpuinfo ... procesor
/usr/share/doc/packages/sensors/prog/init/lm_sensors.init.suse start .. inicializace
stress -c 3 -i 2 -m3 --vm-bytes 128M -d1 --hdd-noclean --hdd-bytes 3G --timeout 30s .. (weather.ou.edu/%7Eapw/projects/stress) test procesoru, pameti i hdd zarov
en, 30 sekud
```


### Pamet

vmstat ... velikost virtualni pameti a jeji vyuziti  
free ... velikost a vyuziti pameti  
/proc/meminfo .. velikost pameti  
pmap PID ... ukaze informace o procesu, jake knihovny zabiraji kolik mista v pameti  
swapon ... ukaze swap oddily, ktere se uzivaji  
memtest86 ... (www.memtest86.com)  
memtest86+ ... (www.memtest86.org)  
memtester ... (pyropus.cz/software/memtester)  
strings /proc/$PID/environ ... ukaze promenne prostredi pro jedouci proces  

### DISKY

/proc/ide/ide0/hda/model .. nazev modelu disku  
/proc/ide/ide0/hda/capacity .. pocet 512-bajtovych bloku  
fdisk -l ... vylistuje disky a diskove oddily  
hdparm /dev/hda .. zjisti moznosti disku (dma atd.)  
hdparm -c1 -d1 /dev/hda .. zapne dma a IO_support32  
hddtemp /dev/hdd .. (www.guzu.net/linux/hddtemp.php) monitorovani teploty disku -s log  
hddtemp -d /dev/hda; telnet localhost 7634 .. demon, pres tcp ukazuje teplotu  
smartctl -s /dev/hda .. S.M.A.R.T. zaznamy o chybach  
smartctl -a /dev/hda .. (smartmontools.sourgeforge.net)  
/proc/sys/dev/cdrom/atoeject, autoclose, lock .. vlastnosti cdrom mechaniky: autovysunuti po odmountovani, autozasunuti pro mountovani, zamce pri mountovani  
echo 1 > /sys/bus/scsi/drivers/sd/block/device/rescan  

ll /sys/bus/scsi/drivers/sd/0\:0\:1\:0/  
lsscsi  
echo "- - -" > /sys/class/scsi_host/host0/scan .. pridani scsi zarizeni  
lsscsi  
echo 1 > /sys/bus/scsi/drivers/sd/0\:0\:6\:0/delete .. delete scsi zarizeni  
lsscsi  

### Zvukova karta

/proc/asount/cards  
aplay -l .. seznam zariceni, co mohou prehravat zvuk  
alsamixer  
aplay aaa.wav  
aplay -D plug:surround51 chan-ad.wav - (ftp://ling.ll.hawaii.edu/pub/greg/Surround-SDL-testfiles.tgs) test surround zvuku  

### Monitor, graficka karta, klavesnice, mys

get-edit | parse-edit ... (john.fremlin.de/programos/linux/read-edit) info o monitoru, vystup text pro xorg.conf  
screen-test ... (www.fi.muni.cz/~kar/screentest) graficky test monitoru  
xev ... test mysi a klavesnice  

### Logy, sledovani udalost

tail -f /var/log/messages  
dmesg ... vypisy jadra  
dbus-monitor --system ... realtimove sledovani udalosti [D-Bus](https://www.freedesktop.org/wiki/Software/dbus/)u system (wifi, sitova karta, zarizeni atd).  
dbus-monitor --session ... sledovani session, napriklad [screensaver](https://people.gnome.org/~mccann/gnome-screensaver/docs/gnome-screensaver.html#gs-signal-ActiveChanged)  
/etc/dbus-1/ ... konfigurace dbusu  
/bin/dbus-daemon, dbus-launch ... spusteni sluzby D-Bus - smernice udalosti pro vymenu informaci mezi aplikacemi  
journalctl ... /var/log/messages na SystemD (RH6, Fedora 20 atd)  
journalctl --vacuum-time=10d ... vycisti logy (/var/log/journal), necha jen 10 dni logu  
journalctl --vacuum-size=2G ... vycisti logy (/var/log/journal), necha jen 2 GB  

### Napoveda, dokumentace

export MANPATH=/usr/share/man ... nastavi cestu k MAN strankam  
man -k disk ... vypise vsechny man stranky, kde je v popisu obsazen "disk"  
nrofl -man [manpage.1](manpage.txt) ... zobrazi, jak bude manualova stranka vypadat  
groff -man -Tascii page.txt ... zobrazi z ascii souboru manualovou stranku (jako nroff)  
groff -man manpage.txt > file.ps ... vytvori post skiptovy soubor z manualove stranky  
man2html -title 'Titulek' < Ascii_soubor.txt > html_soubor.html  ... prevede soubor s definici manualovych stranek do html  

### Konzole - RSA

[RSA](http://en.wikipedia.org/wiki/IBM_Remote_Supervisor_Adapter)  
[OpenIPM](http://openipmi.sourceforge.net/) ... otevreny projekt k [IMPI](http://en.wikipedia.org/wiki/Intelligent_Platform_Management_Interface)  
[IBM Advanced Settings Utility (ASU)](http://www-947.ibm.com/support/entry/portal/docdisplay?brand=5000008&lndocid=MIGR-55021) ... nastroj na konfiguraci RSA kartet na IBM xSeries
