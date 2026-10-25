# AIX - Souborove systemy, LVM, disky, ...

## Pristupy k souborum

aclget soubor ... (Access control get) informace o pristupu k souboru
aclput -i /tmp/acl.txt -R /tmp ... nastavi ACL definovana v /tmp/acl.txt (muze byt vystup z aclget) rekurzivne na /tmp  
[acledit](http://www-01.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.cmds1/acledit.htm)  /tmp ... zapne interaktivni editovani ACL prav pro /tmp  
istat 1235 /dev/lv_cog ... informace o inode 1235
find /Cognos -inum 1235 ... najde jaky soubor je inode 1235  
pg ... vypise obsah souboru s pauzou na konci stranky
fuser ... identifikuje, ktery proces pouziva tento soubor
fuser -dV /var ... ukaze ktere procesy na FS /var maji otevreny nejaky neexistujici soubor  
fuser -cux /var ... ukaze vsechny procesy, co uzivaji /var  
filemon ... monitorovani file systemu - statistika vyuziti (trcstop zastavi filemon)
iostat ... statistika vyuzivani disku
j2edlimit -l -u /PMSASNDF ... zobrazeni, kdo ma jakou kvotu na FS
trcstop ... zastavi filemon monitoring
update ... kazdych 30 sekund sync  
dircmp ... (directory compare) porovnava adresare  
uucp ... kopiruje soubory na jiny unix system  
uuto/uupick ... kopiruje na jiny, z jineho unixu  

## informace o fyzickych discich

ipl_varyon -i ... seznam hdisku, invormace o PVID a jestli jsou bootovatelne  
lsdev -Cc adapter ... seznam radicu
lsdev -Cc disk ... seznam disku
lsdev -p hdisk0 ... ktery adapter ovlada disk hdisk0
lsdev -C -c disk -S a -F 'name class subclass location parent' ... ukaze disky i s rodicema  
lsparent -Pl scsi0 ... ktere disky ovlada radic scsi0
lscfg | grep disk ... nazvy disku
lscfg -vl hdisk0 ... podrobne informace o disku hdisk0
lsattr -El hdisk0 ... nastaveni driveru disku hdsik0
lspath ... ktery radic ovlada ktery disk
/lq  

## Fibre Chanel, [SDD](http://kutngedg.homelinux.org/blog/?cat=5&paged=2) (Storagesystem Device Driver), <a fref="http://doc-tcpip.org/Aix/aix.mpio_sdd.html|SDDPCM]] (Path Control Module) - MPIO

lsattr -El dpo ... informace o DPO (Data Path Optimiser)  
lsattr -El vpath5 ... informace o vpath  

**SDD**

dpovgfix ... opravi volume groupu, ktera ma oboji - hdisky i vpathy  
extendvg4vp ... extenduje volume groupu od vpathy  
fget_config -vA ... informace o discich v diskovych polich
fcstat fscsi0 ... Stav a statistiky radice pro fiber chanel fscsi0
hd2vp ... konvertuje hdisky na vpathy  
lscfg -l fcs0 -vps | grep Network ... vypise WWN cislo Fiber Channel karty (Jako MAC u sitovky)  
lsattr -El fscsi0 | grep attach ... ukaze, zda je pripojeny k FC switchi  
lscfg -l hdisk21 -vps ... ukaze S/N atd. LUN id = posledni 3 cislice z SN a 4 cisla v Z1  
lsvp -a ... Vypis jednotlivych cesta a harddisku ve Fibre chanel
lsvp -d ... seznam pozic v jednotlivych bay ve Fiberchanel
lsvpcfg ... seznam nastaveni virtual path, prirazeni VG, atd.
manage_disk_drivers ... seznam ovladacu pro diskove pole
mkvg4vp - vytvory SDD volume groupu (z vpathu)  
mpio_get_config -vA ... informace o nastaveni MPIO
querysn ... ukaze seriove cisla zarizeni  
/usr/bin/sddpcm_get_config -Av ... informace o discich v diskovych polich
vp2hd ... prevede vpathy na hdisky  

SDclient ... graficke ovladani storage DSxxxx  
/opt/ibm/dscli .. textove ovladani storage DSxxxx

```
2105 ==> ESS (mit FC ==> Fiber Channel connected, sonst SCSI)
2107 ==> DS8000
1750 ==> DS6000
2145 ==> SAN Volume Controller Device
2062 ==> SAN Volume Controller for Cisco MDS 9000
```

addpaths - Fügt einem bestehenden vpath-Device weitere Pfade zu. Das Kommando ist dynamisch, der vpath ist aktiv und im Status "available".
addpaths ... prida nove cesty  
cfallvpath - Legt das SDD Pseudo-Device dpo an sowie alle vpath Devices.
cfallvpath ... Fast-path configure method to configure the SDD pseudo parent dpo and all vpath devices.  
chgvpath - Ändert vpath Attribute.
chgvpath ... meni vpath atributy  
datapath - Eine Administrations-Konsole für den SDD Treiber.
lquerypr - Zeigt und setzt persistente Reservierungen (SCSI Locks).
lsvpcfg - Zeigt die Zuordnung Platte - vpath Device.
querysn - Zeigt die serielle Nummer der Devices.
mkvg4vp - Legt SDD Volume Groups an.
extendvg4vp - Erweitert SDD Volume Groups.
dpovgfix - Repariert eine SDD Volume Group, die gemischte hdisk / vpath Devices aufweist.
pathtest - Umfangreiches Tool zum Testen und Debuggen.
pathtest -d 20 ... otestuje a tracuje cesty  
datapath query device  
datapath query adapter ... (SDD) seznam radicu pro Fiber Chanel
datapath query device ... seznam zarizeni fro FC
datapath query essmap|grep hdisk1667 ... informace o disku v fiber chanel
lquerypr ... Ukazuje a meni rezervacni status (SCSI Locks).  
lquerypr -Vh /dev/hdisk ... ukaze reserved status  
lquerypr -rh /dev/hdisk ... vyprazdni reserved status  

**SDDPCM**
pcmsrv - Deamon, der die Pfade überwacht.  
pcmpath ... info a meneni SDDPCM zarizeni
pcmpath query device ... seznam SDDPCM zarizeni
pcmquerypr - Zeigt und setzt persistente Reservierungen (SCSI Locks).  
sddpcmke - Kernel-Extension. Stellt System-Calls zum Management der Pfade zu Platten auf Storage Boxen zur Verfügung.  
sdduserke - API zu dieser Kernel Extension.  
pcmgenprkey - Generiert Keys zur Reservirung von Platten und zeigt bestehende Keys.  
relbootsrv - Hebt SCSI-2 Reservierungen auf.  
sddpcmgetdata - Sammelt Debug-Information und Traces (File sddpcmdata_hostname_time.tar).  
pdmtest - Umfangreiches Tool zum Testen und Debuggen.  

**ESS**  
[lsess](http://unix.derkeiler.com/Mailing-Lists/AIX-L/2005-10/0037.html)  

**[ssa](http://www.alanward.info/Glossary/S/SSA.html)**
diag -> Task Selection -> SSA Service Aids -> Set Service Mode ... seriove cisla disku  
lsdev -C -t hdisk -c disk -s ssar -H ... ukaze ssa disky
ssaadap -l hdisk59 ... ukaze, na kterem adapteru je zapojen disk 59  
ssaconn -l pdisk59 -a ssa2 ... ukaze, jak je zapojen SSA disk v SSA poli  
ssadisk -a ssa0 -L ... seznam disku na ssa  
ssaxlate -l hdisk5 ... info o ssa disku hdisk5
[ssaload](http://www.alanward.info/Glossary/S/SSA_Commands/ssaload.htm) ... nahraji mikrokod na ssa disk  
ssa_fw_status -a ssa0 ... ukaze stav baretie pro ssa0  

**SCSI X-PCI RAIDs**  
sisraidmgr -L -j1 -l sisioa0 ... vypis raid zarizeni pod radicem sisioa0  
sisraidmgr -h ... help k praci s RAID polema  
ssaraid ... SSA raid

**SVC**  
$SVCCLI svcinfo lsvdisk | grep 600507680190025518000000000009E4 ... zjisti, zda je naasignovany disk z nasledujicim SCSIid  
$SVCCLI svcinfo lsvdiskhostmap vdisk1465 ... infomace o disku 1465  

## Storage

[/tmp/emc/emcgrab/emcgrab.sh](http://www.aixhealthcheck.com/blog?id=48) ... ukaze vsechny informace tykajici se EMC storage - FC, LUNu atd.  

## PV

chpv -a n hdisk1 ... (change of physical volumes) nastavi allocation permission=no
getlvcb -TA hdisk3 ... ziska Logical Volume Control Block - informace o LVM - VGDA/VGSA
lspv ... (list of physical volumes) seznam a informace o PV
migratepv (-l lv01) pv1 pv2 ... (migrate physical volumes) prenese lv01 z pv1 na pv2
readvgda -v3 hdisk19 ... precte VGDA (volume group distinct area) z PV  

## VG

chvg - chance volume group
exportvg - export volume group
extendvg - volume group
extendvg4vp -f datavg vpath32 ... rozsiri VG o virtualni cestu
importvg - import volume group
mirrorvg - mirror volume group
mkvg - make volume group
lsvg - show volume groups
lsvg -p VGrupa ... kuaze PV, ktere pouziva VGrupa  
lsvgfs rootvg ... ukaze filesystemy VG rootvg  
lvmstat -v rootvg ... ukaze statistiky o VG rootvg
reducevg ... reduce volume group
reorgvg ... reorganizuje VG pro lepsi vykon
restvg -q -f /tmp/zaloha hdisk1 ... Obnovi VG ze souboru /tmp/zaloha na hdisk1
splitvg ... snapshoty  
syncvg ... (Synchronize Volume Groups) synchronizuje vg, pv, nebo lv
syncvg -l ... zynchronizuje LV ktere jsou ve stavu "stale" - nesynchronizovane  
synclvodm ... synchronizuje LVM a ODM informace
unmirrorvg - unmirror volume group
varyonvg - aktivuje deaktivovanou volume groupu, nebo ji reaktivuje (synchronizuje)
varyoffvg - deactivate volume group
readvgda / lquerypv / lqueryvg ... Verify VG integrity

## LV

extendlv - extend logical volume
getlvcb -AT lvname ... detailni informace o LV lvname
lslv - show logical volumes
lvmtat -l hd8 ... (statistics of logical volumes) statistiky o hd8
cplv -v newvg -y newlv oldlv ... (copy logical volumes) - zkopiruje LV oldlv na newlv v VG newvg
chlv ... nastavuje parametry  
migratelp ... (migrate logical partition) premisti lp na jinou PV
mklv - make logical volume
mklv -t jfslog -y jlog ... Vytvori zarizeni LV typu jfslog o jmenu /dev/jlog  
mklvcopy ... (make logical voluime copy) mirroring LV (1-3 kopie)
rmlv ... (remove logical volume)
rmlvcopy ... (remove logical volume copy)
synclvodm - synchronize logic volumes informations with ODM (object database model) - Synchronize LVM data and check FS integrity
lquerylv -L $(getlvodm -l hd10opt) -r > /tmp/mapfile ... ulozi prirazeni LV na jednotlive PPcka  
lreducelv -l `getlvodm -l hd10opt` -s 3 /tmp/mapfile ... zruseni vsech PPcek (lowlevel smazani hd10opt)  

===GLVM - Geographical LVM - Metro Mirroring===

```
port: 6192/tcp, muze byt vary on jen na jednom pocitaci
      glvm.rpv.client - Remote Physical Volume Client
      glvm.rpv.server - Remote Physical Volume Server
      glvm.rpv.util - Geographic LVM Utilities
      glvm.rpv.msg.en_US - RPV Messages - U.S. English
/usr/sbin/rpvsitename -a 'SITE_NAME' ... nastavi jmeno GLVM serveru
/usr/sbin/mkdev -c rpvserver -s rpvserver -t rpvstype -a rpvs_pvid='HDISK_PVID' -a client_addr='RPV_CLIENT_IP' -a auto_online='y' ... nastavi server
/usr/sbin/mkdev -c disk -s remote_disk -t rpvclient -a pvid='PVID' -a server_addr='RPV_SERVER_IP' -a local_addr='RPV_CLIENT_IP' -a io_timeout='180' ... nastavi klienta
lsdev -Cc rpvserver ... zarizeni GLVM serveru
lsattr -El rpvserver0 ... atributy
lsdev -Cc disk -t rpvclient ... GLVM disky
mount -t glvm ... namountuje glvm disky
[[https://www.ibm.com/support/knowledgecenter/en/ssw_aix_72/com.ibm.aix.cmds3/mkcifsmnt.htm|
      mkcifsmnt]] -f /mnt -d share1 -h server1 -c user1  ... vytvori CIFS FS /mnt z disku share1 z windows pocitace server1 pod uzivatelem user1
```

## FS

crfs -v jfs -g rootvg -a size=16M -m /home ... (create filesystem) Vytvori FS na rootvg veliky 16MB, vytvori zaznam v /etc/filesystems, bude se mountovat do /home
chfs - change file system
chfs -a log=/dev/jlog /FS ... zmeni u FS /FS parametr log na /dev/jlog  
chnfsmnt ... zmeni zaznam v /etc/filesystems pro NFS FS  
defragfs - defragment file system
fsck - file system check
istat - i node statistics
logform jlog ... , zformatuje, vycisti a reinicializuje journal /dev/jlog (napr. po zvetseni journal fs, ne inline journal log)
lsfs -q /var ... detailni informace o FS /var
mkfs -V jfs2 /dev/lva ... vytvori FS jfs2 na /dev/lva  
mkramdisk  4M ... (make ram disk) vytvori z 4 MB pameti disk /dev/ramdisk0
mknfsmnt -f backups -d backups -h host -a -S -t rw -w bg -g ... vytvori zaznam v /etc/filesystems pro mountovani NFS FS  
rmnfsmnt ... smaze zaznam z /etc/filesystems pro NFS FS  
ulimit ... Shows and sets limits for FS

## paging space

lsps -a ... (list of paging space)
mkps -s 1 -a rootvg ... (make paging space) Vytvori paging space na rootvg veliky 1 PP
chps -s 3 paging00 ... (change paging space) zmeni velikost PS paging00 o 3 LP
chps -d 1 paging00 ... zmensi PS paging00 o 1 LP
rmps paging00 ... smaze PS paging00
swapoff /dev/paging00 ... vypne PS /dev/paging00
swapon
vmo -p -o lru_file_repage=0 ... meni parametry paging space
vmstat 1 ... kazdou sekundu informace a statistiky virtualni pameti

## CD/DVD

/usr/sbin/diag -c -d cd1 -T format -s initialize  
cdeject /dev/cd0 ... vysune CD/DVD  

## system dump

sysdumpdev ... prace s system dump FS
sysdumpdev -P -p /dev/SysDumpP
sysdumpdev -l ... ukaze aktivni sysdump disky
sysdumpdev -e ... ukaze potrebne misto na system dump
/usr/lib/ras/dumpcheck ... test, jestli je sysdompfs dost veliky
kdb soubor ... analyza sysdumpu

## boot

bosboot -a ... vytvori bootovaci obraz a zmeni bootlist
bootlist -m normal -o ... vylistuje bootlist (jinak meni bootlist)
chpv -c hdisk0 ... zrusi bootovaci zaznam na hdisk0  
ipl_varyon -i ... seznam hdisku, invormace o PVID a jestli jsou bootovatelne  

## Magneticke pasky

lsdev -Cc tape</tt> ... Vypise vsachna zarizeni pro praci s magnetickou paskou
lscfg -vl rmt*</tt> ... Vypise informcae o vsech mechanikach (serial number, ...)
lsattr -El rmt0</tt> ... Vypise informace o prvni pasce a mechanice
tapeutil -f /dev/smc0 devids</tt> ... Collects the WWN as recorded in the special device file for the given device (e.g. 'rmt5').

tctl -f smc0 status ... informace o mechanice/pasce
tctl ... controls the tape recorder
mt ... jako mctl  
tapechk 2 ... precte 2 blok z pasky
tcopy /dev/rmt0.1 /dev/rmt1.1 ... prekopiruje rmt0 na rmt0  

## zalohovani

ald_disk_copy ... vytvari klony rootvg  
alt_rootvg_op -q -d hdisk0 ... nastavi jako boot disk hdisk0 z ald_rootvg managementu  
backup -0 -u -f /tmp/zaloha /usr ... zazalohuje poprve (-0) FS /usr do /tmp/zaloha (aktualizuje casy v /etc/dumpdates)
backup -1 -u -f /tmp/zaloha /usr ... udela inkrementalni zalohu FS /usr do /tmp/zaloha oproti prvni zaloze -0
find /usr -print | backup -i -v -f /dev/rmt0  
mksysb ... Vytvori instalovatelny obraz rootvg do souboru, ci na bootovatelnou pasku
mkszfile ... posbira data do /image.data  
savevg -f /tmp/zaloha -i datavg ... Vytvori zalohu VG datavg do souboru /tmp/zaloha
mkcd ... (Make CD) vytvori vicesvazkovy CD ze zalohy mksysb a savevg
mkvgdata ... udela soubor s nastavenim pro savevg (/tmp/vgdata/datavg/datavg/data)
listvgbackup ... Ukaze soubory v existujicim backupu na /dev/rmt0
listvgbackup -f /tmp/mksysb.file -l ... ukaze informace o VG  
listvgbackup -f /tmp/mksysb.file -r ./etc/resolv.conf ... obnovi souvor /etc/resolv.conf ze zalohy  
lsmksysb -d /dev/rmt0 ... ukaze obsah zahlohy na pasce  
restorevgfiles ... Obnovi data ze zalohy
restore -T -f /tmp/zaloha ... vylistuje soubory ze zalohy /tmp/zaloh
restore -xvf /tmp/zaloha ... obnovi soubory ze zalohy /tmp/zaloh a vypise informace o souborech
restvg -q -f /tmp/zaloha hdisk1 ... Obnovi VG ze souboru /tmp/zaloha na hdisk1
nim -o define -t mksysb -a server=master -a location=/NIM_filesystem/NIM_client_sysb -a source=NIM_client -a mksysb_flags=eiX -a mk_image=yes NIM_client_sysb ... nimbackup  
nim -o lslpp -a filesets='bos.alt_disk_install.rte' ... ukaze verzi filesetu ve spotu  
nim -o update -a packages='bos.alt_disk_install.rte' -a source='[full_path]' -a show_progress=yes [lpp_source] ... upgrade filesetu ve spotu  
nim -o cust -a lpp_source=[lpp_source] -a filesets=bos.alt_disk_install.rte [spot]  
lsnim -a if master To see NIM master hostname  

## Storage, datova uloziste

[MPIO](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.baseadmn/doc/baseadmndita/devmpio.htm)

```
1724-100 = DS4100 = FAStT 100

1722-600 = DS4300 = FAStT 600

1742-900 = DS4500 = FAStT 900

1814 = DS4700/DS4200

1815 = DS4800

FC 2105 ==> ESS (mit FC ==> Fiber Channel connected, sonst SCSI)
FC 2107 ==> DS8000
FC 1750 ==> DS6000
FC 2145 ==> SAN Volume Controller Device
FC 2062 ==> SAN Volume Controller for Cisco MDS 9000

pcmpath (devices.sddpcm.53.rte)
datapath (devices.sdd.53.rte) - existuji zarizeni vpathX, ktere zastupuji cesty+disky na Storage

/usr/sbin/pathtest
```

## dos

dosdir
dosread
doswrite
dosdelete (dosdel)
dosformat

format ... (format diskette)
flcopy ... (flopy copy)

### Rozsireni­ LV

*Zjistit, zda se nejedna o cluster, napr. smitty clverify. Vice v kapitole [manage_diagnose](manage_diagnose.html)*
lsvg -l rootvg
lsvg rootvg | grep FREE
extendlv hd4 3
lslv hd4
**X**=1024*1024*(PP SIZE)*(LPs)/512
(extendlv pokud je aix v. <= 5.2)  
chfs -a size=**X** /dev/hd4
*Jde-li o cluster zvetsime* smitty hacmp

### Mirrorovani VG vg01 na jiny PV hdisk3

mirrorvg vg01 hdisk3

### Odstraneni/vymena PV hdisk3 ve VG vg01 za pouziti nahradni PV hdisk6

mkdev -c disk -l hdisk6
extendfs vg01 hdisk6
mirrorvg vg01 hdisk6
unmirror vg01 hdisk3
reducevg vg01 hdisk3

### Nalezeni souboru k danemu i nodu

find /home -xdev -inum 25 -print

### SAN Event (Storage Area Network)

date
errpt
errpt -a
snap -gfiLc
datapath query adapter
datapath query device
fget_config -Av ... jak je ktery SAN disk zapojen
lsdev -l dac0 -F parent

==Rozsireni VG o disk v Clusteru==

```
clRGinfo
chdev -l hdisk95 -a pv=yes
extendvg aaa hdisk95
varyonvg -ub aaa
ssh node2 "importvg -L aaa hdisk43" (nebo extendvg aaa hdisk95)
varyon
```

**nebo**

```
HACMP smitty:
---------------------
smitty hacmp
System Management (C-SPOC)
HACMP Logical Volume Management
Shared Volume Groups
Set Characteristics of a Shared Volume Group
Add a Volume to a Shared Volume Group
---------------------
---------------------
smitty hacmp
System Management (C-SPOC)
HACMP Logical Volume Management
Synchronize a Shared Volume Group Definition
---------------------
```

### Rozsireni LV v clusteru

smitty hacmp -> System management -> HACMP Logical Volume Manager -> Shared Logical Volumes -> Change a shared LV
smitty hacmp -> System management -> HACMP Logical Volume Manager -> Shared Logical Volumes -> Set Characteristics of Shared LV -> Increase the Size of a Shared LV
nebo

```bash
lslv aaa
chlv -x 14000 aaa
chlv -u 8 aaa
extendlv aaa 1000 hdisk95 hdisk96
varyonvg -ub aaa
ssh node2 "importvg -L aaa hdisk43" (nebo extendvg aaa hdisk95)
varyon
```

==Rozsireni FS v clusteru==

```bash
lsfs -q /abc
smitty hacmp -> System management -> HACMP Volume Manager -> Shared File Systems -> Enhanced JFS -> Change / Show ...
```

==Obnoveni smazaneho souboru==

```bash
istat 1243 /dev/lv_cog # Block Pointer d0450
echo "ibase=16;D0459 | bc # 853072
lsfs -q /Cognos # block size: 4096
echo "853072 * 4096" | bc # 3494182912
dd if=/dev/lv_cog of=/tmp/lost_file skip=3494182912 bs=1 count=41450
```
