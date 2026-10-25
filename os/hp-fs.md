# HP-UX - File Systemy, LVM, zalohovani, Storage

### Soubory

chacl ... (change access list) meni ACL k souborum  
fuser -u data/data ... ukaze procesy uzivajici soubor /data/data  
fuser -cu /data ... procesy, ktere pristupuji na FS /data  
fuser -ku /dev/vg01/datavol ... zabije procesy, ktere pristupuji na LV datavol  
lsacl ... ukaze ACL souboru  

### FS - souborove systemy

/etc/fstab ... FS, ktere se mountuji pri startu OS  
bdf ... ukaze volne miso na FS  
convertfs ... konverze FS aby podporoval dlouhe nazvy
dcopy ... kopirovani FS
edquota ... edituje kvoty
extendfs -F vxfs /dev/vg01/rdatavol ... (extend file system) zvetsi odmountovany VxFS na LV rdatavol na maximalni velikost LV
fsadm ... (file system administrate) meni namountovany FS (musi byt nainstalovany balicek)
fsadm -F vxfs -E /data ... ukaze statistiku fragmentace extentu (fragmentu) souboru na FS  
fsadm -F vxfs -D /data ... ukaze statistiku fragmentace adresaru  
fsadm -F vxfs -de -t 600 ... defragmentuje soubory i adresare po dobu max. 600 sekund  
fsadm -F vxfs -b 32m /dev/vg01/rdatavol ... Online meni velikost FS na LV rdatavol (Musi byt licence OnlineJFS)  
fsadm -F vxfs /data ... ukaze, zda FS /data podporuje soubory delsi nez 2 GB  
fsadm -F vxfs -o largefiles /data ... zapne podporu velkych souboru  
fsck -F vxfs /dev/vg01/rdatavol... (file system check) oprava poskozeneho, nekonzistentniho FS (zkontroluje podle jurnalu  
fsck -F vxfs -o full,nolog /dev/vg01/rdatavol ... Otestovani a oprava celeho VxFS, ne podle jurnalu  
fsdb ... (file system debugger) prohlizeni jurnalu FS a opravovani FS
fstyp -v /dev/vg00/rlvol1 ... zjisti typ FS na LV lvol1, -v parametry FS  
quotacheck ... otestuje qvoty
mkfs ... make file system
mkfs -m /dev/vg01/rdatavol ... ukaze parametry FS na LV datavol  
mkfs -F vxfs -o ninode=unlimited,bsize=1024,version=6,inosize=265,logsize=2048,largefiles /dev/vg01/rdatavol 16384 ... vytvori FS na datavol s konkretnimi parametry  
mediainit -S -c 0 -t 3 /dev/disk/disk1 ... premaze zarizeni 3x samyma nulama, znici FS a vsechny data  
mount -F cdfs -o ro,cdcase,rr /dev/disk/disk1 /dvd ... namountuje CD/DVD  
mount -F lofs /data /optdata ... pripoji pripojeny FS /data taky na /optdata - podobne jako ln -s /data /optdata (Loopback FS)  
mount -F memfs -o size=1g -o ninode=1024 /tmp ... pripoje FS /tmp typu RAM disk, max. velikost 1g, max 1024 souboru (potrebuje balicek MemFS)  
newfs /dev/rdisk/hdisk3 ... vytvori novy file system HFS, nebo VxFS na hdisk3, to podle definice v /etc/default/fs
newfs_hfs ... Vytvori HFS FS
newfs_vxfs ... Vytvori VxFS (JFS - Journaled FS)  
newfs -F hfs -R 1024 /dev/rdisk/disk2 ... vytvori HFS na zacatku hdisk2 a necha 1024 MB na konci volne pro swap  
pvcreate -B /dev/dsk/c2t6d0; mkboot /dev/dsk/c2t6d0 ... vytvareni bootovaciho zaznamu
swlist -l product OnlineJFS* ... zjisti, zda je nainstalovany online meneni velikosti FS  
tunefs ... nastaveni parametru FS
/sbin/fs/vxfs/vxfsconvert /dev/vg01/rdatavol ... prevede FS HFS na VxFS. Je potreba minimalne 15% volneho mista a po konverzi fsck  
vxtunefs ... nastaveni parametru VxFS FS  
vxumopunt -o force /data ... odmountuje hrubym zpusobem (zabije procesy) FS /data  
vxupdate -n 7 /data ... upgradne verzi specifikace JFS/VxFS FS /data na verzi 7  

### Swap

swapon /dev/rdisk/disk4 ... vytvori swap na hdsik4  
swapon -e /dev/rdisk/disk2 ... predtim jsme nechali na konci 1GB nista. Timto tam udelame ze zbytku swap  
swapon -p 4 -l 1024m /data ... Vytvori swapovaci misto velike az 1024MB, priorita swapovani 4 (standartne 1) v adresari /data  
swapoff /dev/rdisk/disk4 ... (11i v3) zrusi pouzivani disku4 jako swap  
swapinfo ... informace o jednotlivych zarizenich swapu a jejich vyuziti

### LVM - Logical Volume Manager

lvmadm -t ... ukaze, jake verze LVM podporuje OS a jake parametry LVM  
lvmadm -l ... (11i v3) ukaze, ktere disky jsou PV a ve kterych VG jsou  
strings /etc/lbmtab ... ukaze, ktere disky jsou PV a ve kterych VG jsou  
swlist -l fileset -a state LVM.LVM-MIRROR-RUN ... HP < 11i v3 ukaze, zda je koupena licence na mirrorovani  
swlist -l fileset -a state LVM.LVM-MIRROR-RUN LVM-MirrorDisk.LVM-MIRROR ... (11i v3) ukaze, zda je koupena licence na mirrorovani  
swlist B9116* T277[1-7]* ... ukaze, zda je koupena licence na Veritas online LVM  
swlist Base-VxVM-50 Base-VXVM ... zjsiti, zfda jsoun nainstalovane balocky pro Veritas LVM  

### LV - Logical Volume

lvdisplay /dev/vgdata/swapvol ... (logical volume display) ukaze hlavicku v LV swapvol z VG vgdata
lvdisplay -v /dev/vg02/lv02 ... ukaze podrobne informace o LV lv02 z VG vg01  
lvcreate -L 16 -n swapvol vg01 ... (logical volume create) vytvori LV swapvol v VG vg01 o velikosti 16MB
lvcreate vg01 ... vytvori LV lvol0x (x nejmensi nepouzite cislo ve VG) ve VG vg01 o velikost 0MB  
lvlnboot 
lvextend -L 16 /dev/vg01/datavol /dev/disk/disk1 ... (logical volume extend) zvetsi LV datavol v vg01 **na** 16MB, prida misto z PV disk1
lvreduce -L 8 /dev/vg01/rdatavol ... (logical volume reduce) zmensi LV na 8 MB, nebo ubere mirror
lvremove /dev/vg01/datavol ... smaze LV datavol
lvrmboot

### VG - Volume group

vgcfgrestore -n vg00 /dev/dsk/c2t0d0 ... Obnovi nastaveni nove vymeneneho PV (musi byt neaktivni)
vgchange -a y datavg ... Prepne grupu do vary on (aktivni VG) VG datavg
vgcreate vgoracle /dev/disk/disk2 /dev/disk/disk3 ... (volume group create) vytvori VGDA na discich disk2, disk3 a priradi je do vg01. Na 11i v3 vytvori i DSF soubory
mkdir /dev/vg02; mknod /dev/vg02/group c 64 0x020000; chown -R root:sys /dev/vg02; chmod -R 755 /dev/vg02; vgcreate vg02 /dev/dsk/c0t1d1 /dev/dsk/c1t1d1... na HP < v3 pripravi DSF a vytvori VG. 0xXX je poradi VG. Pokud je vice cest k disku, pridaji se vsechny  
vgchange
vgchange -a n vg01 ... deaktivuje VG vg01
vgcreate -V 2.1 -S 1t -s 4 vg01 /dev/disk/disk1 ... vytvori VG verze LVM 2.1, maximalni velikos VG 1TB, velikost Physical Excent 4 MB  
vgdisplay ... (volume group display) ukaze vsechny VG (jen hlavicky)
vgdisplay -v vg02 ... ukaze vsechny informace o VG vg02, vcetne LV a PV  
vgexport vg01 ... exportuje (zrusi definice v OS) VG vg01, da se opet importovat
vgextend vg01 /dev/disk/disk3 ... Prida do VG vg01 disk disk3
vgimport
vgreduce vg01 /dev/dsik/disk3 ... odebere disk 3 z VG vg01  
vgremove vg01; rm -ir /dev/vg01 ... smaze VG vg01 (je treba vymazat i DSF, v 11i v3 prepinac -X)
vgscan -apv ... oscanuje PV vsech VG a znovu vytvori /etc/lvmtab
vgsync vg00 ... synchronizuje VG vg00

### PV - Physical Volume

pvchange -a n /dev/dsk/c2t0d0 ... nastavi PV c2t0d0 jako neaktivni
pvcreate /dev/rdisk/disk5 ... (physical volume create) vytvori PV (na zacatku disku LVM hlavicky) a pripravi disk na vlozeni do VG  
pvcreate -f /dev/rdsk/c1d1t1 ... vytvori PV, pokud na disku uz nekdy PV existoval (prepise jej)  
pvdisplay /dev/disk/disk1 ... (physical volume display) ukaze hlavicku PV disk1
pvdisplay -v /dev/dsk/c1t1d1 ... ukaze podrobne informace o PV c1t1d1 vcetne jednotlivych excentu z LV  
pvmode /dev/disk/disk3 /dev/disk/disk2 ... presune vsechny fyzicke excenty z disku3 na disk2  

### [Veritas LVM](/veritas/fs.html)

vxinstall ... nastartuje Veritas VXVM moduly - startuje se poprve, kdyz se instaluje VXVM  
/opt/VRTSob/bin/vea ... graficke nastavovani VXVM  
vxdisk list ... seznam PV (disku v Veritas VM)  
vxprint -g rootdg ... informace o rootdg  

### Storage

scsimgr get_attr -a wwid -H 64000/0xfs00/0x4 ... vypise WWID (HP-UX 11r3)  
scsimgr get_attr -a lunid -H 1/0/2/1/0.0x50001fe15003112c.0x4001000000000000 ... vypise LUNID (HP-UX 11r3)  
spmgr  
autopath  

### boot disk

[boot proces](manage.html#boot), [MP - Manangement processor](mp)  
lvlboot -v ... ukaze boot definice spousteciho disku  
lifls /dev/rdisk/diska ... u PA-RISC ukaze obsah bootovaci oblasti  
lifcp /dev/rdisk/diska:AUTO - ... ukaze obsah AUTO souboru ve startovaci LIF oblasti disku  
idisk /dev/rdisk/diska ... ukaze jednotlive EFI oddily disku a  
idisk -wf /tmp/[idf](idf.txt) /dev/rdsk/c0t1d0 ... prepise EFI strukturu disku (100 MB 1. EFI oddil, 400MB 3. EFI oddil)  
idisk -e -l /dev/rdsk/c0t1d0 ... prekopiruje HP strukturu (hpux.efi) z /usr/lib/efi do 1. systemoveho EFI oddilu  
efi_ls -d /dev/rdisk/diska_p1 /efi/hpux ... vylistuje soubory v 1. EFI oddilu v adresari \efi\hpux  
efi_cp -d /dev/rdisk/diska_p1 -u /efi/hpux/auto /dev/tty ... zobrazi obsah souboru auto  
efi_cp -d /dev/rdisk/diska_p1 [/tmp/ftp.efi](http://www.intel.com/technology/efi) /efi/hp/tools/network/ftp.efi ... zkopiruje soubor ftp.efi s FS do 1. EFI oblasti  
mkboot -a "boot vmunix -lq" /dev/rdisk/diska_p1 ... zmeni obsah souboru auto ci AUTO v bootsektoru (PA-RISC i Integrity)  
setboot ... ukaze obsah NVRAM, z ktereho disku se bude startovat system (PA-RISC i Integrity)  
setboot -a x/x.x.x ... zmeni alternativni cestu k boot disku (PA-RISC i Integrity)  
setboot -h x/x.x.x ... zmeni HA alternativni cestu k boot disku (PA-RISC i Integrity)  
setboot -p x/x.x.x ... zmeni primarni cestu k boot disku (PA-RISC i Integrity)  

### System backup

fbackup -f - -i /var ... zazalohuje /var, vystup jde na standartni vystup
frecover -R -f /dev/rmt0 ... obnoveni vsech souboru ze zalohy na pasce

dump /usr ... zazalohuje FS /usr na pasku
restore ... obnovi FS z pasky

rdump, rrestore 
vgcfgdump, vgcfgrestore 

tar cf /dev/rmt/0m /var ...
mt -f /dev/rmt/0mn rew
mt -f /dev/rmt/0mn fsf 1
tar xvf /dev/rmt/0m soubor

### Omniback

mc -r DS ... (media changer) vypise stav menice medii
omniabort -ses 2008/08/05-28 ... prerusi backup
omnistat ... (omnibackup status) Vypise stav backupu
omnidb ... pristup k databazi Omnibackupu  
omnidb -ses 2008/08/05-28 -rep | more ... Vypise stati
omnidatalist
omnidatashedule
omnidbcheck -extended
omnimm ... ovladani medii Omnibackupu  
omnimm -eject ESL9322 42 86 37 10 ... (omniback media manager
xomni

### Ignite backup - bootovatelny backup

swlist IGNITE ... zjisti, zda je nainstalovany ignite  
/opt/ignite/recovery/mnt_essentials ... defaultni definice include - co je zahrnuto v backupu  
/var/opt/ignite/recovery/archive_content ... dalsi definice pro ignite paskovy backup  
/var/opt/ignite/client/recovery/archive_content ... dalsi definice pro ignite sitovy backup  
/var/opt/ignite/recovery/latest/recovery/latest/recovery.log ... log ignite  
/var/opt/ignite/clients/clients/client/recovery/latest/recovery.log ... log pro net ingite backup  
crontab -l | grep -i sauv_ignite
crontab -l | grep -i /usr/local/bin/sauv_system
/opt/ignite/bin/make_tape_recovery ... Vytvoreni ignite backupu na pasku
make_tape_recovery -x include=/home/root -x inc_cross /data ... vytvori ignite backup vcetne /home/root, a vcetne FS /data  
make_tape_recovery -x inc_entire=vg00 -x exclude=/tmp ... zazalohuje cely VG vg00 krome /tmp  
make_tape_recovery -a /dev/rtape/tape00_BESTn -d "Nazev archivu" ... zazalohuje na pasku tape00, nastavi neprevijet, popis bude "Nazev archivu"  
make_net_recovery -s server.com -n3 -d "popis" ... vytvori zalohu na server server.com, necha na serveru 3 posledni zalohy, popis bude "popis"  
make_media_install ... vytvori bootovatelne DVD z net ignite backupu  
make_sys_image ... klonovani systemu na jiny server  

### [DRD](http://docs.hp.com/en/5992-6590/index.html) - Dynamic Root Disk - 11i v2, 11i v3

swinstall -s /tmp/DynRootDisk*.depot DynRootDisk ... nainstaluje DRD  
/var/opt/drd/drd.log ... logy drd  
ftp://ftp.itrc.hp.com/export/DRD/drd_unsafe_patch_list ... nebezpecne balicky, ktere se nedoporucuje patchovat na klonech pres DRD  
drd clone -t /dev/dsk/c1d1t1 -x overwrite=true ... Udela klon vg00 na c1d1t1, prepise, kdyz tam je LVM, nebo klon  
drd clone -t /dev/disk/disk2 -x mirror_disk=/dev/disk/disk3 ... vytvori mirrorovany klon vg00 na disk2 a disk3  
drd status ... ukaze informace o klonech vg00, co je aktivni, datum klonu atd  
drd mount ... namountuje klod VG00 do /var/opt/drd/mnts/sysimage_001  
drd umount ... odmountuje klon vg00  
drd activate ... aktivuje klon soucasne nabootovaneho vg00 - po restartu se nastartuje z klonu a ten bude vg00  
drd deactivate ... deaktivuje aktivovany klon - po restartu nabootuje socasne vg00  
drd runcmd [swinstall|swremove|swlist|swmodify|swverify|swjob|kctune|update-ux|view] ... spusti specifikovane prikazy na klonu  
drd runcmd swinstall -s server:/mydepot PHSS_NNNNN ... nainstaluje na klonu soubory z /mydepot (ne z klonu)  
drd mode -? ... ukaze volitelne prepinace  

### Rozsireni LV:

/usr/sbin/cmviewcl ... check up cluster
bdf /opt
lvdisplay /dev/vg00/lvol6
vgdisplay /dev/vg00
swlist -l product | grep -i online ... Can I do it online
lvextend  -l 239 /dev/vg00/lvol6
fsadm -F vxfs -b 978944 /opt ... if I can do it online
umount /dev/vg00/lvol6; extendfs /dev/vg00/lvol6; mount /dev/vg00/lvol6 ... if I'm not able to do it online
**if cluster:**
vgexport -v -s -p -m vg01.map vg01 ... on node A and copy vg01.map to node B
ll /dev/vg01 ... on node B ( check minor number for vg01. ex : 0x010000)
vgexport vg01 ... on node B
mkdir /dev/vg01 ... on node B
mknod /dev/vg01/group c 64 0x010000 ... on node B
vgimport -v -s -m /tmp/vg01.map vg01 ... on node B
check /etc/lvmtab. make sure vg01 already change. ... on node B

### Zrcadleni VG00 - PA-RISC

pvcreate -fB /dev/rdisk/diskb ... vytvori PV s mistem pro LIF (boot sektor)  
vgextend vg00 /dev/disk/diskb ... rozsiri VG o PV  
mkboot /dev/rdisk/diskb ... vytvori LIF boot sektor  
lifls /dev/rdisk/diskb ... overi, ze LIF byl vytvoren  
mkboot -a "hpux -lq" /dev/rdisk/diska ... vypne quorum na diska  
mkboot -a "hpux -lq" /dev/rdisk/diskb ... vypne quorum na diskb  
lifcp /dev/rdisk/diska:AUTO - ... overi, zda je quorum vypnute  
for lv in /dev/vg00/lvol*; do lvextend -m 1 $lv; done ... zazrcadleni jednotlivych LV  
lvlnboor -R /dev/vg00 ... zaktualiuje se LVM Boot Disk Reserved Area (BDRA)  
lvlnboot -v ... zobrazi obzah BDRA  
echo "1 /dev/disk/diskb" >> /stand/bootconf ... prida zaznam do souboru bootconf, ktery vyuziva swinstall pri update jadra  
setboot -h 0/0/10/0/0.0.0xa.0x0 ... nastavi diskb v NVRAM jako druhy bootovatelny disk  
setboot ... zobrazi NVRAM  
reboot -ry 0 ... reboot  
echo boot_string/S | abd /stand/vmunix /dev/kmem ... overi, ze se booovalo z noveho zrcadla  

### Zrcadleni VG00 - Integrity

idisk -wf /tmp/[idf](idf.txt) /dev/rdisk/diskb ... vytvori EFI oddily na disku b  
idisk /dev/rdisk/diskb ... ukaze EFI oddily na disku b  
insf -eC disk ... vytvori se SDF device files pro nove oddily  
ioscan -fun /dev/dsk/cxtxdx ... Vylistuje nova zarizeni 11i v1,2  
ioscan -m lun /dev/disk/diskb ... Vylistuje nova zarizeni 11i v3  
mkboot -e -l /dev/rdisk/diskb ... nahraje HPUN soubory do \efi\hpux  
efi_ls -d /dev/rdisk/diskb_p1 /efi/hpux ... vylistuje hpux soubory  
mkboot -a boot vmunix -lq /dev/rdisk/diska[b] ... nastavi \efi\hpux\auto parametr na disku a [b]  
efi_cp -d /dev/rdisk/diska_p1 -u /efi/hpux/auto /dev/tty ... ukaze nastaveni \efi\hpux\auto  
pvcreate -fB /dev/rdisk/diskb_p2 ... vytvori PV s mistem pro LIF (boot sektor)  
vgextend vg00 /dev/disk/diskb ... rozsiri VG o PV  
for lv in /dev/vg00/lvol*; do lvextend -m 1 $lv; done ... zazrcadleni jednotlivych LV  
lvlnboor -R ... zaktualiuje se LVM Boot Disk Reserved Area (BDRA)  
lvlnboot -v ... zobrazi obzah BDRA  
echo "1 /dev/disk/diskb_p2" >> /stand/bootconf ... prida zaznam do souboru bootconf, ktery vyuziva swinstall pri update jadra  
setboot -h 0/0/10/0/0.0.0xa.0x0 ... nastavi diskb v NVRAM jako druhy bootovatelny disk  
setboot ... zobrazi NVRAM  
reboot -ry 0 ... reboot  
echo boot_string/S | abd /stand/vmunix /dev/kmem ... overi, ze se booovalo z noveho zrcadla  

### zruseni zrcadleni VG00 - Integrity

for lv in /dev/vg00/lvol*; do lvextend -m 0 $lv; done ... zruseni zazrcadleni jednotlivych LV  
vgreduce vg00 /dev/disk/diskb_p2  
pvremove /dev/rdisk/diskb_p2  
rmsf /dev/*disk/diskb_p*  
lvlnboot -R  
mkboot -a "boot vmlinux" /dev/rdisk/diska  
grep -v "diskb" /stand/bootconf > a; mv a /stand/bootconf\\>
