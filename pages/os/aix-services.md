# AIX - Sluzby

lssrc -a - list system resource center - list of services, which are on and off<br />
refresh -s syslogd ... znovun nacte demona syslogd<br />
startsrc -l lpd ... start service lpd<br />
stopsrc -s syslogd ... stop service<br />

#### /etc/inittab

chitab ... zmeni zaznam v inittabu<br />
mkitab ... vytvori zaznam v inittabu<br />
rmitab ... smaze zaznam v inittabu<br />
telinit n ... zmeni runlevel na cislo n<br />

#### nfs

startsrc -g nfs ... start nfs service  
lssrc -g nfs ... list nfs services  
stopsrc ... stop nfs services  
/etc/services (mountd) ... nastavi privilegovany port pro mountd  
mknfs ... make nfs - start nfs<br />
rmnfs ... remove nfs - stop nfs<br />
chnfs ... change nfs - change options of nfs<br />
mknfsexp ... make nfs export<br />
mknfsmnt ... make nfs mount<br />
/usr/sbin/mknfsexp -d '/export/mksysb' '-B' -S 'sys' -t 'rw' -h '10.10.20.0/24' -c '10.10.20.0/24' -r '10.10.20.0/24' ... prida mountpoint do /etc/exports  
/etc/xtab ... FS, ktere jsou namountovane na klienty (ktere pouziva nfs.mountd)  

#### automounter

automount<br />
stopsrc -s automount<br />

#### nis

chypdom - change nis domain<br />
ypset<br />

#### ldap

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

ibmslapd<br />
mksecldap<br />

#### dhcp

startsrc -s hdcpcd<br />

#### nim

lsnim ... (list of Network Installer Manager) vypise seznam definovanych objektu<br />
nimclient ... klient nimu<br />
nim ... master nimu<br />
nimconfig ... nastaveni nim masteru<br />

#### Listener

lsnrctl start<br />
lsnrctl stop<br />
lsnrctl stat<br />
ps eaf | grep LISTENER<br />

#### Oracle

sqlplus / as sysdba<br />
SQL> startup<br />
sqlplus / as sysdba<br />
SQL> shutdown<br />
ps eaf|grep Ť ora_ ť<br />
<br />
sqlplus /as sysdba<br />
SQL> select status, database_status from v$instance ;<br />

#### SAP

<h6>Start:</h6>
startsap_argisdb1_00<br />
startsap_argisas1_01<br />
<h6>Stop:</h6>
stopsap_argisdb1_00<br />
stopsap_argisas1_01<br />
<h6>Status:</h6>
startsap check<br />
<b>Nastaveni a umisteni: </b>
/usr/sap/PS1 ... sap adresar<br />

#### munin

Bezi na portu 4949<br />
<h6>Start</h6>
/munin/sbin/munin-node config /munin/etc/munin-node.conf<br />
<h6>Stop</h6>
kill -9 $(ps -aef|grep munin|grep -v grep|awk '{print $2}')<br />
<h6>informace o sluzbe</h6>
homepage: [http://munin.projects.linpro.no/](http://munin.projects.linpro.no/)

#### ESM

<h6>Start: </h6>
/esm/esmrc start<br />
/etc/rc.esm<br />
<h6>Stop: </h6>
/esm/esmrc stop<br />
<h6>Status: </h6>
/esm/esmrc status<br />

#### CWS

hmmon -GQs 1:0 ... informace o zdroji ?<br />

#### audit

<h6>start:</h6>
/usr/sbin/audit start<br />
<h6>stop:</h6>
/usr/sbin/audit shutdown<br />
<h6>status:</h6>
ps -ef|grep auditbin<br />
<h6>info<h6>
audit query ... ukaze nastaveni  
/etc/security/audit/* ... konfigurace  
auditpr &lt; trail ... vypise systemove udalosti<br />
auditselect -e "event == FILE_Write && date >= 05/03/99" trail | auditpr -h e,l,R,t,c,r,p,P,h,T -v ... vyselektuje jen eventy FILE_Write  

#### Proxy - squid

<h6>Start:</h6>
echo "/usr/sbin/squid -D >/dev/console 2>&1" | at now<br />

#### pcpmm - testovaci software na funkcnost stranek

/usr/lpp/pcpmm/instance/tecad/etc/pcpmmtecad start ... Spousti nejakou cast pcpmm - tecad_logfile<br />

#### [accounting](http://docstore.mik.ua/orelly/networking/puis/ch10_02.htm)

<h6>start/stop</h6>
/usr/lib/acct/startup ... spusteni auditovani procesu  
<h6>configure/info</h6>
lastcomm ... vypis v minulosti spustench procesu s casem spusteni  
acctcom ... vypis v minulosti spustenych procesu s informaci o vyuziti cpu/mem  
/var/adm/pacct ... datovy soubor s informacemi o spustenych procesech v minulosti  
/var/adm/acct  

#### RSCT (real scalar cluster technology)

<h6>start</h6>
startsrc -s ctrmc ... start CSM (Cluste System Management) v /etc/inittab  
<h6>status</h6>
lssrc -g rsct  
lssrc -g rsct_rm  
<h6>zdroje/odkazy</h6>
REDBOOKS: A Practical Guide for Resource Monitoring and Control (RMC)  
http://post.doit.wisc.edu/library/aix51/usr/share/man/info/en_US/a_doc_lib/aixbman/rsct/rsct02.htm  
<h6>popis soucasti<h6>
<h6>CSM resource managers:</h6>
IBM.DMSRM ... Domaind Management System RM (MS) - ridi INM.ManagedNode, IBM.NodeGroup, IBM.NodeAuthentificate, IBM.DmsCtrl  
IBM.HWCTRLRM ... Hardware Control RM (MS)  
IBM.CSMAgentRM ... CSM Client Resource Agent RM (Nodes)  
<h6>Reacting to events</h6>
IBM.ERRM ... Event Esponse RM  
IBM.ServiceRM ... Service RM  
<h6>Monitoring data</h6>
IBM.FSRM ... Filesystem RM  
IBM.HostRM ... Host RM (Lazy daemon)  
IBM.SensorRM ... Sensor RM  
IBM.WLM ... Workload Manager RM  
<h6>Logging</h6>
IBM.AuditRM ... Audit Log RM  
<h6>Further resource managers</h6>
IBM.ConfigRM ... Configuration RM  
<h6>nezarazene</h6>
IBM.DRM ... (Lazy daemon)  

#### Ostatni

[SNA/Communications Server](http://www-01.ibm.com/software/network/commserver/aix/library/publications.html)
