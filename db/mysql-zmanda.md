# MySQL/MariaDB - Zmanda

## Externi odkazy

[Zmanda](http://zmanda.com/backup-mysql.html) - zalohovani MySQL - Zmanda Recovery Manager for MySQL  
[Zmanda](http://www.zmanda.com/download-zrmphp) - download komunitni verze  

## Instalace

yum install bsd-mailx, mariadb-client libdbi-perl libxml-parser-perl  
adduser --system --group --home="var/lib/mysql" mysql  
yum install mysql-zrm  
cd /etc/mysql-zrm  
mkdir -v backupsetname  
cp -vi mysql-zrm.conf backupsetname/  
Pridame do mysql serveru uzivatele z mysql-zrm.conf:

```
GRANT select show vie, create view, insert, update, create, drop, reload, shutdown, alter, super, lock tables, replication silent on *.* to 'backu-user'@'backuphost' identified by 'password';
```

echo 'supertajneheslo' > /etc/mysql-zrm/.passphrase  
chmod 600 /etc/mysql-zrm/.passphrase  
mkdir -v /root/.gnupg  
chmod -v 700 /root/.gnupg  

## Konfigurace

/etc/mysql-zrm/*/mysql-zrm.conf

## Start/stop/status

mysql-zrm-scheduler --backup-set backupsetname --backup-level 0 --interval daily --start-time 01:00 ... denni spusteni  
mysql-zrm-scheduler --query ... ukaze naplanovani zaloh  

## Zaloha, zobrazni zaloh a obnova

mysql-zrm-scheduler --backup-set backupsetname --backup-level 0 --now ... okamzite spusteni backupu  
mysql-zrm verify-backup --backup-set backupsetname ... zkontroluje zalohu  
mysql-zrm-reporter --show backup-performance-info ... ukaze posledni zalohu  
mysql-zrm-reporter --show restore-info --where backup-set=backupsetname ... ukaze info potrebne pro obnovu  
mysql-zrm-restore --backup-set backupsetname --source-directory /var/lob/mysql-zrm/20120303121212 ... provede obnoveni dat ze zalohy
