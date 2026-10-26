---
title: LINUX - Souborove systemy, disky, LVM, ...
---

## Soubory

stat soubor ... informace o souboru - cas modifikace, pristupu atd.  

### Pristup k souborum procesama

fuser /mnt/a ... seznam procesu, tere vyuzivatji /mnt/a  
fuser -vk /mnt/a ... vypise vsechny procesy, ktere pristupovaly na /mnt/a a zabije je  
lsof ... vypis otevrenych souboru  
ls -l /proc/*/fd/* ... dalsi zpusob jak vylistovat otevrene soubory  

### Prava k souborum

chown -R root:root /etc ... zmeni vlastnika adresare a souboru rekurzivne  
chgrp root /etc/hosts ... zmeni skupinu vlastnika souboru  
chmod 755 aaa.txt ... zmeni pristupova prava k souboru  
tune2fs -l /dev/sda3  ... zapne ACL funkcionalitu na FS  
mount -o acl /dev/sda ... namountovani s ACL funkcionalitou  
getfacl ... ukaze ACL (Access Control List) pristupy  
setfacl -m u:visitor:rx /home/schedule.txt ... nastavi ACL na soubor /home/schedule.txt, ze uzivatel visitor ma pristup rx  
setfacl -x g:visitors /home/schedule.txt ... zrusi ACL na soubor /home/schedule.txt pro skupinu visitors  
setfacl -m d:u:student:rw /home ... nastavi defaultni ACL pro adresar /home pro studenta na rw  
setfacl --remove-default /home ... zrusi defaultni prava k adresari home  

## Souborove systemy

[Filesystemy](http://www.lissot.net/partition/) - [ext2](http://www.freesoftware.fsf.org/ext2-doc/), ext3, ext4, RaiserFS, BrtFS  

/etc/fstab ... seznam nadefinovanych FS  
/etc/mtab ... seznam aktualne pripojenych FS  
/etc/crypttab ... seznam FS k rozsifrovani behem startu  
badblocks /dev/fd01440 1440 ... kontrola povrchu diskety  
badblocks -n /dev/hda8 ... po odmountovani /dev/hda8 nedestruktivni kontrola povrchu disku  
blkid ... precte FS a identifikuje je (typ FS, UUID)  
blobfuse ... mounovani BLOB zarizeni (Napriklad [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-how-to-mount-container-linux)  
cat /proc/filesystems  ... fileseystemy, co jsou k dispozici  
cat /proc/partitions ... seznam zarizeni, ktere jsou k dispozizi  
cfdisk /dev/sda  ... vice uzivatelsky prijemny fdisk  
cryptsetup luksOpen /dev/mapper/VG-LV FSname ... Odemkne zakryptovany fs /dev/VG/LV a vytvori z nej odemlke zarizeni /dev/mapper/FSname  
cryptsetup luksClose FSname ... zamkne zakodovany FS (lsblk - vylistuje)  
cryptsetup -y create luks-data /dev/vgTL/lv.data ... vytvori kryptovani na LV  
cryptsetup -v -c "aes-cbc-essiv:sha256" -q --verify-passphrase luksFormat /dev/mydev/zipdisk ... vytvori zformatuje zarizeni na sptavny LUKS format a oznaci zarizeni  
cryptsetup resize sdb1_crypt -v ... zmeneni velikosti  
cryptsetup hash /dev/mapper/VG-LV ... informace o zakryptovanem FS  
dd if=/dev/zero of=/dev/fda obs=512 count=200k  ... low level formatovani  
dd if=/dev/hda of=/dev/null .. test sektoru  
dd if=/dev/zero of=aa count=2000000 .. test rychlosti zapisu  
dmsetup ls ... seznam disku namapovanych pomoci device mapperu (/dev/mapper)  
dmsetup info ... informace o jednotlivych discich namapovanych pomoci device mapperu (v /dev/mapper)  
dmsetup table ... tabulka zarizeni mapperu  
debugfs /dev/hda2 .. obnoveni smazanych souboru  
dumpe2fs /dev/sda6 ... podrobne informace o FS  
e2fsadm -L+2G /dev/Volume00/mylv ... Rozsiri LV + FS o 2G (Musi byt odmountovany FS)  
e2fsck -c /dev/hda8 ... oznaceni vadnych sektoru  
e2label /dev/hda1 root_disk ... zmeni LABEL pro /dev/hda1 na root_disk  
e2label /dec/hda1 ... ukaze label zarizeni /dev/hda1  
edquota ... meni vzoroveho udivatele pro quota a aplikuje pravidla na jine uzivatele  
edquota -t ... meni dobu, kdy se ze soft kvoty stane hard kvota  
[encfs](https://www.root.cz/clanky/encfs-sifrovani-souboru-jinak-a-bez-problemu/) ... mountovani zakryptovaneho adresare, umount pomoci fusermount -u  
extundelete --restoreall /dev/hd1 ... restoruje ([undelete](http://extundelete.sourceforge.net/index.html)) vsechny soubory z /dev/hda1 na ext4/ext3 do ./RESTORE_FILES  
fdisk /dev/hda  ... vytvareni/meneni/ruseni FS na /dev/hda  
fdisk -l /dev/sda1 ... seznam oddilu na /dev/sda  
fdisk -1 /dev/sda1 ... pocet sektory na oddilu /dev/sda1  
fdformat /dev/fd0H1440 ... (floppy disk format) formatovani disket  
findfs LABEL=label ... rozpozna, jaky FS ma jmenovku label  
fsck -t ext2 /dev/hda2 ... kontrola a oprava FS  
losetup /dev/loop0 /path/to/container1 ... vytvori loop zarizeni /dev/loop0 ze souboru /path/to/container1  
losetup -d /dev/loop0 ... zrusi zarizeni /dev/loop0  
lsscsi - zobrazi scasi disky  
ls /dev/disk/* ... vypis FS, jeich UUID a jine  
lsblk --fs ... vylistuje cryptovane (LUKS) blokove zarizeni  
mkbootdisk --device /dev/fd0 2.4.2-3 ... vytvoreni bootovaci diskety  
mkdosfs -cv -F 32 /dev/fd0 ... vytvori DOS Filesystem na diskete  
mke2fs ... vytvori ext2/ext3 FS  
mkfs -c -t ext2 /dev/fd0 ... vytvoreni FS EXT2 na diskete  
mkfs.ext2 fs1 ... zformatuje fs1 na ext2  
mkfs.ext2 -c -c /dev/hdc1 .. naformatuje hdc1, pouzije nekolikanasobny zapis - test zapisu  
mount -t usbfs usbfs /proc/bus/usb   - ukaze, jake usb porty jsou na pocitaci, a  take v kterem jsou usb zarizeni  
mount -t iso9660 -o loop image.iso /mnt/isoimage .. namountuje iso do adresare  
mount -o noatime,nodirtime /dev/hda1 /mount  ... mountovani bez zaznamu acces time  
mount -o remount,rw,acl,usrquota,grpguota /mnt/a ... premountuje fs /mnt/a s read-write,acl,quota parametry  
mount -t ext3 /dev/sda1 /mnt/crypto/ -oencryption=aes-256 ... mountovani zakodovaneho FS  
mount -t [ecryptfs](https://www.howtoforge.com/tutorial/how-to-encrypt-directories-with-ecryptfs-on-ubuntu-16-04/) /home/secure /home/secure ... mountovani zakryptovaneho adresare pomoci eCryptFS  
mount fs1 ~/a -o loop ... pripoji soubor jako disk  
mount LABEL=data-disk /mnt/data ... pripoji disk s popiskem data-disk  
parted /dev/hda ... Programek na praci s ext2/FAT/FAT32 (zmensovani,zvetsovani,presunovani,..)  
partprobe ... informuje OS o zmene FS  
[photorec](http://www.cgsecurity.org/wiki/PhotoRec_Step_By_Step) ... undelete pro FAT, EXT2/3/4 atd. - obnoveni smazanych souboru  
quotacheck -cugm / ... vytvori user a group quota soubor pro FS /  
quotaon -g / ... zapne skupinove kvoty pro FS /  
quotaoff -a ... vypne quoty pro vsechny FS  
quota -g users ... ukaze uziti disku a kvotu pro grupu users  
quotarep -u -a ... shromazdi quoty pro vsechy filesystemy a pro vsechny uzivatele  
repquota -a ... ukaze vsechny kvoty  
resize2fs -p /dev/vg0/data ... rozsiri FS /dev/vg0/data na maximum, napise vyuziti disku (FS muze byt namountovany)  
setquota -g users 20000 100000 100 200 / ... meni nastaveni kvot pro konkretniho uzivatele,grupu  
sfdisk -l -x ... (jako root) seznam vsech FS, ktere jsou k dispozici  
sfdisk -d /dev/sda > /zaloha_sda ... zazalohuje informace o FS  
sfdisk < /zaloha_sda ... obnoveni oddilu ze zalohy  
tune2fs -j /dev/hda2 ... nastavovani parametru FS. Prida zurnal (ext2 -> ext3)  
tune2fs -l /dev/sda7 ... ukaze nastaveni FS  
warnquota ... varuje uzivatele o prekrceni kvoty  

## Kodovane FS

[Truecrypt](http://www.truecrypt.org) + [popis](https://help.ubuntu.com/community/TruecryptHiddenVolume)
truecrypt data.ts ... namapuje data.ts na /dev/mapper/truecrypt1, textovy rezim  
truecrypt --mount --fs-options=rw,nosuid,nodev,umask=077,uid=501,gid=501 -k data.tc.key -p HESLO /mnt/data.ts /mnt/aaa ... namountuje FS  
truecrypt -d /mnt/aaa ... odmountuje FS  
realcrypt -t -d ... od,puntuje vsechna TC zarizeni  
realcrypt -t -c ... vytvoreni noveho zakryptovaneho kontejneru v textovem rezimu  
realcrypt -t -l ... vylistuje vsechny truecryptova namountovana zarizeni  
realcrypt -t --mount --filesystem=none data.tc ... rozkoduje a namapuje souborovy kontejner data.tc na zarizeni /dev/truecryptX  
cryptsetup - LUKS kodovani disku  
[kodovani disku a instalace Ubuntu](https://medium.com/@chrishantha/encrypting-disks-on-ubuntu-19-04-b50bfc65182a)  

## Boot sektor, bootovani

mkinitrd /boot/initrd ... vytvori initrd RamDisk s modulama  
**GRUB**  
grub-install --root-directory=/mnt /dev/sda ... nahraje grub do bootovaciho sektoru disku  
dd if=stage1 of=/dev/fd0 bs=512 count=1;dd if=stage2 of=/dev/fd0 bs=512 seek=1 ... manualni nahrani grubu do boot sektoru  
**GRUB2**  
/boot/grub/grub.cfg ... konfigurace, needituje se primo  
/etc/default/grub ... edituji se globalni parametry grubu. Musi se aplikovat zmeny prikazem /usr/sbin/update-grub  
/etc/grub.d/* ... posloupnost akci provadenych programem grub-mkconfig. Ten tuto posloupnost prevadi do /boot/grub/grub.cfg  
/usr/sbin/grub-install ... doporucena cesta jak zavest grub2 na zarizeni  
/usr/sbin/update-grub ... doporucena cesta jak updatovat konfiguraci grubu2, napr.  po zmenach parametru v /etc/default/grub. Spousti grub-mkconfig  
/usr/sbin/grub-mkconfig ... provadi prevod definic v /etc/grub.d/* do grub.cfg  

## Swap disk

mkswap -L SWAP-hda6 /dev/hda6 ... naformatuje FS /dev/hda6 jako swap FS s popiskem  
mkswap /tmp/swap ... naformatuhe soubor pro swap FS  
swapon -a ... pouzije vechny nadefinovane disky v /etc/fstab ke swapovani  
swapon -s ... ukaze status vsech swapovacich zarizeni  
swapon /tmp/swap ... zapne swapovani i do souboru /tmp/swap  
swapoff -a ... zrusi swapovani na vsechny zarizeni  

## LVM

[dmsetup](http://linux.die.net/man/8/dmsetup) ... low level prikaz pro praci s LV  
vgchange -an designvg ... deaktivuje zmeny na VG  
vgchange -ay designvg ... aktivuje zmeny na VG  
dmsetup info /dev/VG/LV1 ... informace o LV LV1  
e2fsadm -L+2G /dev/Volume00/mylv ... Rozsiri LV + FS o 2G (Musi byt odmountovany FS)  
importvg designvg ... importuje designvg  
lvcreate -L 4G -n mylv Volume00 ... Vytvori LV ve VG o velikosti 4G  
lvcreate --size 200M -s -n mysnap /dev/Volume00/mylv ... Vytvori snapshot LV mylv, 200MB pro zmeny  
lvdisplay ...  
lvextend -L +50M /dev/vg0/data ... rozsiri LV data o 50MB  
lvreduce -L -20M /dev/vg0/data ... zmensi LV na 130MB  
lvremove /dev/Volume00/msnap  ... zrusi LV  
lvs -o +devices ... seznam LV a na kterych jsou zarizenich  
pvmove /dev/hda1 ... presune vsechy bloky (PE=PP) z /dev/hda1, aby byl prazdny  
pvcreate /dev/sda1 ... vytvori PV  
pvdisplay ... ukaze vsechny PV  
pvs -o +lv_name ... seznam PV i s LV ktere na nich jsou  
pvscan ... hleda na oddilech PV vsech LVP (napr. exportovane VG)  
vgcfgbackup aaavg ... zazalohovani VGDA volume grupy aaavg  
vgcfgrestore ... obnovi VGDA ze zalohy  
for i in `vgcfgrestore -f oraclevg.conf.OK -ll|grep "PV UUID"|awk '{ print $3 }'`; do A=`vgcfgrestore -f oraclevg.conf -ll | grep -B11 $i|head -1|awk '{ print $3 }'`; B=`vgcfgrestore -f oraclevg.conf.OK -ll | grep -B11 $i|head -1|awk '{ print $3 }'`;vgcfgrestore -f oraclevg.conf.OK -o $B $A; echo; done  
vgcreate vg0 /dev/sda1 ... vytvori VG vg0 z PV /dev/sda1  
vgdisplay ... informace o VG  
vgexport designVG ... exportune neaktivni VG  
vgextend Volume00 /dev/sda1  ... prida PV do VG  
vgreduce vg0 /dev/hda1 ... odebere /dev/hda1 z VG vg0  
vgs ... seznam VG  

## Softwarovy raid

cat /proc/mdstat ... ukaze konfiguraci softwaroveho RAID  
mdadm ... prace s raid poli  
mdadm -C /dev/md0 -l 1 -n 2 /dev/sda5 /dev/sda8 ... vytvori nove programove raid pole RAID1 z 2 disku  
mdadm -D /dev/md0 ... vypise informace o raid poli /dev/md0  
mdadm /dev/md0 -f /dev/sdm2 ... oznaceni disku /dev/sdm2 jako vadneho  
mdadm /dev/md0 -r /dev/sdm2 ... odebrani disku /dev/sdm2 z pole  
mdadm /dev/md0 -a /dev/sdm2 ... pridani disku /dev/sdm2 do pole  
mdadm -A --scan ... projde vsechny zarizeni a sestavi z nich raid pole, jez bylo drive vytvoreno  
cat /proc/mdstat .. raid pole  

## Multipathing

[Device Mapper Multipathing](http://www.redhat.com/docs/manuals/csgfs/browse/4.6/DM_Multipath/index.html)  

device-mapper-multipah ... balicek  
dm-multipath ... kernel modul podporujici failover atd.  
multipath ... prikaz - listuje a configuruje zarizeni, spousti se bezne v /etc/rs.sysinit, udevem, nebo initramfs  
multipathd ... demon, monitoruje cesty  
kpartx ... prikaz, vytvari DM (/proc) zarizeni potrebne pro souborove systemy (FS)  
/etc/multipath.conf ... konfigurace  
dmsetup ls ... seznam multipath zarizeni  

echo "scsi-qlascan" &gt; /proc/scsi/qla2200/1 ... rescanuje zarizeni na FC  
echo "scsi add-single-device 3 0 0 0" > /proc/scsi/scsi ... prida zarizeni (/dev) podle toho, co nasel qlascan  
echo "scsi remove-single-device" 3 0 1 0 > /proc/scsi/scsi ... odebera zarizeni (/dev)  
### SDD driver

cfgvpath ... rescanuje zarizenipro sdd  
service sdd start/stop/status/restart ... sdd sluzba  
datapath query device ... seznam disku spravovanych sdd  
scli, sclient ... nastroj na konfiguraci FC - Fiber Channel karty  

## Hardware

==INFO - disky:==

```
/proc/ide/ide0/hda/model .. nazev modelu disku
/proc/ide/ide0/hda/capacity .. pocet 512-bajtovych bloku
smartctl -s /dev/hda .. S.M.A.R.T. zaznamy o chybach
smartctl -a /dev/hda .. (smartmontools.sourgeforge.net)
hdparm /dev/hda .. zjisti moznosti disku (dma atd.)
hdparm -c1 -d1 /dev/hda .. zapne dma a IO_support32
hddtemp /dev/hdd .. (www.guzu.net/linux/hddtemp.php) monitorovani teploty disku -s log
hddtemp -d /dev/hda; telnet localhost 7634 .. demon, pres tcp ukazuje teplotu
[[http://www.digipedia.pl/man/doc/view/sg_scan.8/|sg_scan]] ... Soucast balicku sg3_utils) scanuje SCSI disky /dev/sgX, nebo /dev/sdXX
```

==TEST - disky:==

```
dd if=/dev/hda of=/dev/null .. test sektoru
mkfs.ext2 -c -c /dev/hdc1 .. naformatuje hdc1, pouzije nekolikanasobny zapis - test zapisu
dd if=/dev/zero of=aa count=2000000 .. test rychlosti zapisu
debugfs /dev/hda2 .. obnoveni smazanych souboru

lsdev
procinfo

/proc/sys/dev/cdrom/atoeject, autoclose, lock .. vlastnosti cdrom mechaniky: autovysunuti po odmountovani, autozasunuti pro mountovani, zamce pri mountovani
```

==INFO - disky:==

```
/proc/ide/ide0/hda/model .. nazev modelu disku
/proc/ide/ide0/hda/capacity .. pocet 512-bajtovych bloku
smartctl -s /dev/hda .. S.M.A.R.T. zaznamy o chybach
smartctl -a /dev/hda .. (smartmontools.sourgeforge.net)
hdparm /dev/hda .. zjisti moznosti disku (dma atd.)
hdparm -c1 -d1 /dev/hda .. zapne dma a IO_support32
hddtemp /dev/hdd .. (www.guzu.net/linux/hddtemp.php) monitorovani teploty disku -s log
hddtemp -d /dev/hda; telnet localhost 7634 .. demon, pres tcp ukazuje teplotu

Storage - manipulace s disky
echo "scsi-qlascan" > /proc/scsi/qla2200/1 ... scan disku ze Storage
echo "scsi remove-single-device" 3 0 1 0 > /proc/scsi/scsi ... odebrani disku ze storage z /dev
echo "scsi add-single-device 3 0 0 0" > /proc/scsi/scsi ... pridani disku ze storage do /dev
```

## Vypalovani CD

mkisofs -J -r -o output.iso dir_with_files/ ... z adresare idela ISO  
mkisofs -J -r -C 0,145024 -M ATAPI:0,1,0 -o output1.iso dir_with_files/  
mkisofs -J -r -C $(cdrecord dev=ATAPI:0,1,0 -msinfo) -M ATAPI:0,1,0 -o output1.so dir_with_files/  
cdrecord dev=ATAPI:0,1,0 -msinfo .. zjisti, kde se ma zacit dalsi session u multisession  
cdrecord -scanbus ... vypise CD a DVD zarizeni  
cdrecord dev=0,0,0 blank=fast .. vymaze prepisovatelne cd  
cdrecord dev=ATAPI:0,1,0 -v -multi -pad -data output.iso  
cdrecord -v dev=0,0,0 -pad -audio *.wav ... vypali audio stopy  
mkisofs -J -r dir_with_files/ | cdrecord dev=ATAPI:0,1,0 -v -multi -pad -data -  
mkisofs -r -o (image file) (source directory); mount -t iso9660 -o ro,loop=/dev/loop0 (image file)\\ /mnt/cdrom ... namountuje ISO  
growisofs ... kombinace mkisofs a cdrecord  
paketovy zapis na CD (linux+06/3) (packet-cd.sourceforge.net/) (sourceforge.net/projects/linux-udf)  

## SAN Event (Storage Area Network)

date  
/var/log/messages  
dmesg  
uname -a  
sysreport (Red Hat)  
datapath query adapter  
datapath query device  

## Zalohy/obnoveni souboru

[MONDo](http://www.mondorescue.org/) ... bootovatelne zalohy linuxu  
SystemImager ... instalace, zalohy Linuxu  

## Priklady

==Rozsireni FS v LVM s ext2/3==

```
umount /adr
e2fsadm -L+1G /dev/myvg/homevol
mount /adr
```

nebo

```
umount /adr
lvextend -L+1G /dev/myvg/homevol
resize2fs /dev/myvg/homevol
mount /adr
```

### Rozsireni FS v LVM s reiser

mount /adr  
resize_reiserfs -f /dev/myvg/homevol  

### Rozsireni FS v LVM s xfs

mount /adr  
xfs_growfs /home  

### vytvoreni virtualniho FS ze souboru

dd if=/dev/zero of=/dev/fda obs=512 count=200k  ... low level formatovani  
mkfs.ext2 fs1  
mount fs1 ~/a -o loop  

==zaloha disku==

```
dd if=/dev/hda of=/tmp/aaa (nebo cat /dev/hda > /tmp/aaa)
mount -o loop /tmp/aaa
cat /tmp/aaa > /dev/hda1
dd if=/dev/zero of filler_file; snc; rm filler_file ... zaplni zbyvajici misto na diku nulama,
```

==Vypalovani CD==

```
cdrecord -scanbus
mkisofs -J -r -o output.iso dir_with_files/
cdrecord dev=ATAPI:0,1,0 -msinfo .. zjisti, kde se ma zacit dalsi session u multisession
```

nebo

```
mkisofs -J -r dir_with_files/ | cdrecord dev=ATAPI:0,1,0 -v -multi -pad -data -
```

### Vytvoreni RAM-disku - disk z pameni ROM

mknod -m 660 /dev/ram b 1 1  
chown root.disk /dev/ram  
dd if=/dev/zero of=/dev/ram bs=1k count=4k ... vycisti pamet o velikosti 4MB  
/sbin/mkfs -t ext2 -m 0 /dev/ram 4096 ... vytvori ext2 strukturu na 4MB RAM  
mount -t ext2 /dev/ram /mnt/disk ... namountuje pametovy RAM disk  

### Odkazy

[http://www.g-loaded.eu/2005/11/10/encrypt-devices-using-dm-crypt-and-luks/](http://www.g-loaded.eu/2005/11/10/encrypt-devices-using-dm-crypt-and-luks/) moc pekne navody na ruzne veci
