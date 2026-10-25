# AIX - Sluzby

lssrc -a - list system resource center - list of services, which are on and off
refresh -s syslogd ... znovun nacte demona syslogd
startsrc -l lpd ... start service lpd
stopsrc -s syslogd ... stop service

## /etc/inittab

chitab ... zmeni zaznam v inittabu
mkitab ... vytvori zaznam v inittabu
rmitab ... smaze zaznam v inittabu
telinit n ... zmeni runlevel na cislo n

## nfs

startsrc -g nfs ... start nfs service  
lssrc -g nfs ... list nfs services  
stopsrc ... stop nfs services  
/etc/services (mountd) ... nastavi privilegovany port pro mountd  
mknfs ... make nfs - start nfs
rmnfs ... remove nfs - stop nfs
chnfs ... change nfs - change options of nfs
mknfsexp ... make nfs export
mknfsmnt ... make nfs mount
/usr/sbin/mknfsexp -d '/export/mksysb' '-B' -S 'sys' -t 'rw' -h '10.10.20.0/24' -c '10.10.20.0/24' -r '10.10.20.0/24' ... prida mountpoint do /etc/exports  
/etc/xtab ... FS, ktere jsou namountovane na klienty (ktere pouziva nfs.mountd)  

## automounter

automount
stopsrc -s automount

## nis

chypdom - change nis domain
ypset

## ldap

start-secldapclntd  
stop-secldapclntd  
restart-secldapclntd  
ls-secldapclntd  

/etc/security/ldap/ldap.cfg ... knfiguracni soubor LDAP klienta  
/etc/ldap.conf ... konfiguracni soubor sudosasu  

gsk7cmd -keydb -create -db /usr/ldap/etc/clientkey.kdb -pw PASSWD -type cms ... Vytvori certifikacni soubor s klicem  
gsk7cmd -keydb -stashpw -db /usr/ldap/etc/clientkey.kdb -pw PASSWD  
gsk7cmd -cert -add -db /usr/ldap/etc/clientkey.kdb -pw PASSWD -file FILE.cer -format ascii -label gsnixldap1 -trust enable ... prida certifikat duveryhodneho serveru  
gsk7cmd -cert -list -db /usr/ldap/etc/clientkey.kdb -pw PASSWD ... vylistuje duveryhodne servery  

idsldapsearch -h gsnixldap1 -D "cn=SI4,cn=Clients,ou=unix,ou=SI4,dc=customers,dc=fr,dc=ibm,dc=com" -w ANTKaf4! -p 636 -Z -K /usr/ldap/etc/clientkey.kdb -P PASSWD -s sub  -b "" objectclass=* ... vylistuje data z ldap serveru  
mksecldap -c -h gsnixldap1,gsnixldap2 -p 389 -a "cn=SI4,cn=Clients,ou=unix,ou=SI4,dc=customers,dc=fr,dc=ibm,dc=com" -p PASSWD -d "cn=aixdata,ou=unix,ou=SI4,dc=customers,dc=fr,dc=ibm,dc=com" -t 60 -A ldap_auth ... zmeni nastaveni ldap klienta  

ibmslapd
mksecldap

## dhcp

startsrc -s hdcpcd

## nim

lsnim ... (list of Network Installer Manager) vypise seznam definovanych objektu
nimclient ... klient nimu
nim ... master nimu
nimconfig ... nastaveni nim masteru

## Listener

lsnrctl start
lsnrctl stop
lsnrctl stat
ps eaf | grep LISTENER

## Oracle

sqlplus / as sysdba
SQL> startup
sqlplus / as sysdba
SQL> shutdown
ps eaf|grep Ť ora_ ť

sqlplus /as sysdba
SQL> select status, database_status from v$instance ;

## SAP

**Start:**
startsap_argisdb1_00
startsap_argisas1_01
**Stop:**
stopsap_argisdb1_00
stopsap_argisas1_01
**Status:**
startsap check
**Nastaveni a umisteni:**
/usr/sap/PS1 ... sap adresar

## munin

Bezi na portu 4949
**Start**
/munin/sbin/munin-node config /munin/etc/munin-node.conf
**Stop**
kill -9 $(ps -aef|grep munin|grep -v grep|awk '{print $2}')
**informace o sluzbe**
homepage: [http://munin.projects.linpro.no/](http://munin.projects.linpro.no/)

## ESM

**Start:**
/esm/esmrc start
/etc/rc.esm
**Stop:**
/esm/esmrc stop
**Status:**
/esm/esmrc status

## CWS

hmmon -GQs 1:0 ... informace o zdroji ?

## audit

**start:**
/usr/sbin/audit start
**stop:**
/usr/sbin/audit shutdown
**status:**
ps -ef|grep auditbin
**info**
audit query ... ukaze nastaveni  
/etc/security/audit/* ... konfigurace  
auditpr &lt; trail ... vypise systemove udalosti
auditselect -e "event == FILE_Write && date >= 05/03/99" trail | auditpr -h e,l,R,t,c,r,p,P,h,T -v ... vyselektuje jen eventy FILE_Write  

## Proxy - squid

**Start:**
echo "/usr/sbin/squid -D >/dev/console 2>&1" | at now

## pcpmm - testovaci software na funkcnost stranek

/usr/lpp/pcpmm/instance/tecad/etc/pcpmmtecad start ... Spousti nejakou cast pcpmm - tecad_logfile

## [accounting](http://docstore.mik.ua/orelly/networking/puis/ch10_02.htm)

**start/stop**
/usr/lib/acct/startup ... spusteni auditovani procesu  
**configure/info**
lastcomm ... vypis v minulosti spustench procesu s casem spusteni  
acctcom ... vypis v minulosti spustenych procesu s informaci o vyuziti cpu/mem  
/var/adm/pacct ... datovy soubor s informacemi o spustenych procesech v minulosti  
/var/adm/acct  

## RSCT (real scalar cluster technology)

**start**
startsrc -s ctrmc ... start CSM (Cluste System Management) v /etc/inittab  
**status**
lssrc -g rsct  
lssrc -g rsct_rm  
**zdroje/odkazy**
REDBOOKS: A Practical Guide for Resource Monitoring and Control (RMC)  
http://post.doit.wisc.edu/library/aix51/usr/share/man/info/en_US/a_doc_lib/aixbman/rsct/rsct02.htm  
**popis soucasti**
**CSM resource managers:**
IBM.DMSRM ... Domaind Management System RM (MS) - ridi INM.ManagedNode, IBM.NodeGroup, IBM.NodeAuthentificate, IBM.DmsCtrl  
IBM.HWCTRLRM ... Hardware Control RM (MS)  
IBM.CSMAgentRM ... CSM Client Resource Agent RM (Nodes)  
**Reacting to events**
IBM.ERRM ... Event Esponse RM  
IBM.ServiceRM ... Service RM  
**Monitoring data**
IBM.FSRM ... Filesystem RM  
IBM.HostRM ... Host RM (Lazy daemon)  
IBM.SensorRM ... Sensor RM  
IBM.WLM ... Workload Manager RM  
**Logging**
IBM.AuditRM ... Audit Log RM  
**Further resource managers**
IBM.ConfigRM ... Configuration RM  
**nezarazene**
IBM.DRM ... (Lazy daemon)  

## Ostatni

[SNA/Communications Server](http://www-01.ibm.com/software/network/commserver/aix/library/publications.html)
