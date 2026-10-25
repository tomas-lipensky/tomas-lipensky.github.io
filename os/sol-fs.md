# Disky, LVM, souborove systemy

## odkazy

[Solaris Volume Manager Administration Guide](http://docs.sun.com/app/docs/doc/816-4520)

## Fyzicke/logicke zarizeni

iostat ... info o I/O zarizenich
fmthard ... meni a vytvari VTOC na jednotlivych discich/slice, bacha na chyby, lepsi uzit format
prtvtoc /dev/rdisk/c2t0d0s0|fmthart -s - /dev/rdsk/c2t0d0s0 ... naklonuje oddily podle jednoho disku do druheho
format ... prace s disky
prtvtoc /dev/rdisk/c0d0s0 ... informace o celem disku controler 0 disk 0 z VTOC
sysdef ... info o vsech zarizenich, i o discich

## LVM

metattach d0 c2t3d0s0 ... prida oddil c2t3d0s0 do raid d0
metattach d9 -m d1 ... Prida do mirror raid d9 pole d1
metaclear d0 ... smaze raid d0
metadb ... ukaze vsechny meta replica
metadb -a -c 2 -f c2t1d0s6 c2t2d0s6 ... vytvori 2 data replica na oddilech c2t1d0s6 c2t2d0s6 urcenych pro data state
(force method)
metadb -d c2t1d0s6 ... odstrani meta replica data z oddilu c2t1d0s6
metadb -i ... ukaze podrobne informace o vsech meta replica data
metadetach d9 d0 ... odebere z raid pole d9 pole d0
metadevadm -u c2t2d0 ... update device parametru pro vymeneny disk po devfsadm
metainit -f d0 2 1 c2t1d0s0 1 c2t2d0s0 ... inicializace RAID 0. Vlozi 2 disky, c2t1d0s0 i c2t2d0s0 nejsou
deleny na zadne dily (-f = force ... namountovany FS)
metainit d3 2 2 c2t1d0s0 2 c2t2d0s0 ... inicializace stripovaneho RAID-0
metainit d9 -m d10 ... Vytvori single-mirror raid d9 z pole d0
metainit d5 -p c0d1s1 10m ... vytvori soft-partition
metainit hsp001 c0d2s1 c0d3s1 ... vytvori hotspare pool
metahs -a hsp000 c0d4s1 ... prida c0d4s1 do hsp000
metahs -e c0d4s1 ... povoli disk v hot-spare (po vymene)
metahs -d hsp000 c0d5s1 ... smaze v hsp000 disk c0d5s1
metahs -t -all c0d4s1 c0d5s1 ... vymeni ve vsech hot-spare disk c0d4s1 za c0d5s1
metaparam -h hsp001 h0 ... priasociuje hsp001 poli h0
metaparam -h none h1 ... zhusi hot-spare hro h1
metarecover c0t1d1s1 -d -p ... obnova soft-partitions na vymenenem disku
metareplace -e d0 c2t2d0s0 ... vymena disku v RAID-5 probehla, iniciuje se oprava dat
metareplace d0 c2t2d0s0 c2t1d0s0 ... vymeni se disk c2t2d0s0 v RAID 5 d0 za c2t1d0s0
metaroot d1 (/dev/dsk/c0d0s0) ... prepise /etc/vstab a /etc/system pro root FS
metastat ... statistika o raid
metastat d10 ... statistika o raid d10

## FS

flarcreate ... vytvori bootovatelny obraz FS
ff /dev/dsk/c0d0s0 ... seznam souboru a inode
fsck -F ufs /dev/rdsk/c2t0d0s0 ... kontrola ufs FS /dev/rdsk/c2t0d0s0
fssnap -d /export/home (unmount /dev/rwsnap/0) ... zrusi snapshot
fssnap -l ... ukaze, co je snapovano
fssnap -V ufs -o bs=/tmp /export/home ... udela snapshot FS /export/home do adresare /tmp
fstyp /dev/rdisk/s2t0d0s0 ... ukaze FS typ daneho zarizeni
growfs /dev/md/rdsk/d0 ... rozsireni FS /dev/md/rdsk/d0
installboot /usr/platform/`uname -i`/lib/fs/ufs/bootblk /dev/rdsk/c0t1d0s0 .... nahrani boot sektoru
lockfs ... meni a ukazuje zamky, synchronizuje buffer se stavem disku
mount/umount ... pripojeni, odpojeni FS
mkfile 32m /swapfile ... vytvori soubor o velikosti 32MB urceny k diskovym operacim
mkfs -F ufs /dev/rdisk/s2t0d0s0 65536 ... vytvori ufs FS
mkfs -F ufs -m /dev/rdisk/s2t0d0s0 ... ukaze s jakymi parametry byl vytvoren FS na danem slice
ncheck ... seznam unode a jmen soubory na FS
newfs -v /dev/rdsk/s2t0d0s1 ... vytvori FS ufs na disku s2t0d0s1
newfs -v /dev/vx/rdsk/newDG/vol_01 ... Vytvori FS na veritas volume
newfs -v /dev//rdsk/newDG/vol_01 ... Vytvori FS na veritas volume
quot ... prepocita kvoty uzivatelu na FS
tunefs ... nastaveni FS
swap -l ... seznam swap FS
swap -a /swapfile ... prida soubor /swapfile jako swapovaci zarizeni
swap -d /wsapfile ... odebere soubor /swapfile ze swapovacich zarizeni
swap -s ... statistika swapovacich zarizeni
/etc/vfstab, /etc/mtab, /etc/dfs/dfstab, /etc/dfs/sharetab, /etc/rmtab ... definice FS

### ZFS

zpool create testpool mirrir c0t0d0 c0t1d0 ... vytvori pool testpool se zrcadlovymi disky  
zpool create pool2 /home/ocean/disk1 ... vytvori pool2, datafile bude soubor  
zpool list ... seznam poolu  
zpool destroy pool2 ... zrusi pool2  
zpool status pool2 ... status a informace o pool2  
zpool attach trout /home/ocean/disk2 ... prida dalsi data disk ve forme souboru  
zpool detach trout /home/ocean/disk1 ... odebere jeden datadisk  
zpool add trout mirror /home/ocean/disk3 /home/ocean/disk4 ... prida zrcadlene datadisky  
zpool iostat -v trout ... Vykonnostni statistika  

zfs create testpool/test1 ... vytvori ZFS a namountuje  
zfs set mountpoint=/var/logs techrx/logs ...zmeni mountpoint  
zfs list ... seznam ZFS  
zfs destroy testpool/fs1 ... zrusi ZFS  
zfs unmount testpool/kent ... odmountje ZFS  
zfs mount testpool/kent ... namountuje ZFS  
zfs get all testpool/kent ... ziska parametry ZFS  
zfs set quota=10G testpool/dennisr ... nastavi kvotu na ZFS  
zfs get -rHp -oname,property,value quota testpool ... ziska parametry name,property,value  
zfs set reservation=1G salmon/jeffb ... nastavi vyhrazene misto pro ZFS  

##### snap

coreadm  

## Zalohovani, obnovovani zaloh

ufsdump 0uf /dev/rmt/2cn /var ... zalohovani adresare/FS /var na pasuk
ufsrestore tf /dev/rmt/2cn ... vylistovani souboru v zaloze z pasky
ufsrestore xf /dev/rmt/2cn var/a.txt ... obnoveni souboru var/a.txt v zaloze z pasky
ufsrestore ... obnovovani ze zalohy
[Zalohovani pomoci Veritas NetBackup](/veritas/backup.html)  

##### OpenBoot

banner ... info o OpenBoot, S/N, atd.
boot hisk ... boot z aliasu disk
devalias ... seznam aliasu pro zarizeni
nvalias nextdisk /pci@1d,4/scsi.. ... prirazeni aliasu nextdisk pro zarizeni /pci@1d,4/scsi..
printenv ... vypise promenne
setenv ... nastavuje promenne
show-devs ... seznam zarizeni

==SAN event (Storage Area Network==

```
/var/adm/messages
sd.conf
iostat -El
/kernel/drv/*.conf, *=QLogic or JNI
datapath query adapter
datapath query device
ls -lL /dev/rdsk/*
ls -la /dev/vx/dmp/*
format
```


Danail Staykov Kolev
