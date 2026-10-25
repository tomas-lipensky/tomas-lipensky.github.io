# LINUX - Sluzby

### Externi odkazy

[Seznam a popis sluzeb ve Fedore 13](http://www.mjmwired.net/resources/mjm-services-f13.html)  
[cgconfig](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Resource_Management_Guide/ch-Using_Control_Groups.html)  
[dmks_autoinstaller](http://lists.us.dell.com/pipermail/dkms-devel/2003-September/000007.html)  

### DHCP

[DHCP](http://interperson.ic.cz/dhcp.php)  

iptables -I INPUT -p udp --dport 67 -j ACCEPT  
rpm -i dhcp  
service dhcpd start/stop/status/configtest  
/etc/dhcpd.conf  
/etc/sysconfig/dhcpd  
/var/lib/dhcpd/dhcpd.leases .. historie pridelenych adres  

### DNS - Domain Name Server - named - BIND

[DNS](http://interperson.ic.cz/dns.php) -  BIND (berkley Internet Name Domain)

rpm -i bind system-config-bind  
iptables -t udp,tcp --dports 53,921,953 ... port pro preklad adres, pro lightwight resolving a pro ovladani Bindu pomoci rndc  
service named start/stop/status/restart/reload  
/etc/sysconfig/named  
/etc/named.conf  
/etc/rndc.conf  
dig a.b.c ... otestuje dotaz - podrobny vypis  
host a.c.v ... dotaz na server uvedeny v /etc/resolv.conf  
nslookup a.b.c ... dotaz na DNS server  
rndc-confgen > rndc.conf ... generovani klice pro rnd  
rndc reload ... povi Bindu, ze ma znovu nacist konfiguracni soubory  

### NTP - Network Time Protocol

rpm -i ntp ntpd  
iptables -p udp --dport 123  
service ntp start/stop/status  
/etc/ntp.conf  
ntpdate tik.cesnet.cz ... synchronizuje cas, pokud nejede ntp demon  
ntpdate -q tik.cesnet.cz ... zjisti odstupnost ntp serveru a zjisti rozdil  
ntpq -c peer ... ukaze prehled synchronizace  
rdate tik.cesnet.cz ... zjisti rozdil casu  
rdate -s tik.cesnet.cz ... provede zmenu  

### loadbalancer - pulse

[service pulse start/stop](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Load_Balancer_Administration/s1-lvs-block-diagram-VSA.html)  

### Apache2 - httpd

service httpd|apache2 start/stop/status  
/etc/httpd|apache2/conf/httpd.conf  
/etc/httpd|apache2/conf.d  
htpasswd -nb aaa bbb ... ukaze radek, jez je treba pro passwd soubor pro uzivatele aaa a heslo bbb pro .htaccess  
htpasswd ~/htpasswd ccc ... zepta se na heslo pro uzivatele ccc a prida novy radek do ~/htpasswd  
openssl genrsa -des3 -out server.key 1024 ... vytvori ssl key  
openssl req -new -key server.key -out server.csr ... vytvori ssl csr  
cp server.key server.key.org;openssl rsa -in server.key.org -out server.key ... odstrani passphrase  
openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt ... vytvori ssl crt  
openssl s_client -connect localhost:403 ... pripoji se na port 403 jako klient SSL a otestuje SSL sluzbu  

### squid

service squid start/stop/service  
/etc/squit/squid.conf  

### sshd

rpm -i openssh-server  
iptables -p tcp --dports 22 -j ACCEPT  
service sshd start/stop/status  
/etc/ssh/sshd_config ... nastaveni serveru sshd  
/etc/ssh/ssh_config ... nastaveni klienta ssh  
[~/.ssh/config](config.txt) ... individualni nastaveni pro uzivatele  
eval `[ssh-agent](http://mah.everybody.org/docs/ssh) -s` ... spusti ssh agenta, pote je mozne naimportovat klic  
ssd-add ~/.ssh/id_abc ... naimportuje do pameti klic abc  
ssh-keygen -t dsa ... vygeneruje dsa klic  
ssh-keyscan  
ssh-copy-id -i ~/.ssh/id_das a@b.c ... nakopiruje dsa klic na vzdaleny server do authorized_keys  
scp  
ssh, slogin, sftp  
ssh -Y aaa.cz ... Prepinac -Y zapne X11 forwarding. Musi byt zapnuty i na serveru (X11Forwarding)  
xhost +;ssh -R6000:localhost:6000 aaa; export DISPLAY=localhost:0 ... zapne forwarding portu 6000->6000, jedou X aplikace  
ssh -R1234:localhost:22 aaa; ssh -R1234:localhost:1234 bbb; scp -P 1234 a.txt localhost:. ... kopirovani souboru pres ine servery  
ssh -L23:aaa.cz:123 a@aaa.cz; telnet localhost 123 ... sifrovane telnet spojeni  
ssh ... klavesy ~C - moznost psat dalsi volby, treba -R 10101:localhost:10102 pro reverzni tunel  
[ssh](http://linux.byexamples.com/archives/115/ssh-dynamic-tunneling/) -p8332 -D4445 -N mysurface@1.2.3.4 ... Pripoji se na na 1.2.3.4:8332 a na portu 4445 udela socks5 proxy  

### SMTP - odchozi posta

SMTP (simple message transfer protocol) - odchozi posta

mail -vs "pozdrav" a@b.c ... odesle zpravu s nadpisem Pozdrav na adresu a@b.c, ukaze komunikaci  
mailq ... ukaze maily ve fronte na doruceni (muze jich byt hodne, kdyz vzdaleny MTA odmita spojeni)  
mailq -Ac ... ukaze maily ve fronte na doruceni do na lokalni server  
alternatives --display mta ... ukaze, ktery program obsluhuje MTA (Mail transport agent)  
alternatives --config mta ... vyber programu, ktery obsluhuje mta  
alternatives --set mta /usr/sbin/sendmail.postfix ... nastavi jako vychozi MTA postfic  
telnet 1.2.3.4 25 ... odeslani zpravy pomoci telnetu:

```
HELO mynet.com
MAIL From: a@aaa.com
RCPT To: b@bbb.com
DATA
test
.
QUIT
```

##### sendmail

rpm -i sendmail sendmail-cf sendmail-doc  
iptables -p tcp --dport 25 -j ACCEPT ... smtp  
iptables -p tcp --dport 465 -j ACCEPT ... smtps  
service start/stop/status/restart/reload  
/usr/sbin/sendmail  
/usr/sbin/sendmail -d0</dev/null ... ukaze verzi sendmailu a zakladni informace  
sendmail -q ... znovu projede maily ve fronte  
/etc/mail/sendmail.cf ... konfiguracni soubor - nesrozumitelny  
/etc/mail/sendmail.mc ... konfiguracni soubor - srozumitelny  
/etc/mail/access ... nastaveni, od jakeho pocitace se zpravy prijmaji a od jakeho ne  
/etc/aliases ... aliasy  
/etc/mail/local-host-names ... vsechny nazvy mistniho serveru, pro doruceni mistnim uzivatelum  
cd /etc/mail; make ... znovu nacte konfiguracni soubory  
newaliases ... znovu nacte aliasy ze souboru /etc/aliases  
mailstats -f /var/log/mail/statistics ... statistika o poctu mailu  
makemap ... znovu nacte konfiguracni soubory v /etc/mail/  
/etx/pki/tls/certs: make sendmail.pem ... vytvori klic pro smtps a zbytek se nastavi v sendmail.mc  

##### postfix

service postfix start/stop/status  
/usr/libexec/postfix/master  
/etc/postfix/mail.cf  
/etc/postfix/generic ... preklad adres obdrzenych zprav na jiny nazev, ktery se odesila dal  
/etc/postfix/access ... urcuje, od ktereho serveru zpravy prijma a od jakeho ne  
/etc/aliases ... aliasy pro postfix  
newaliases ... nacte deficnice z /etc/aliases  
postmap ... nacitani a ukazani definic  
postmap -s /etc/postfix/access ... ukaze vsechny pristupy  
postmap -q aaa /etc/postfix/access ... ukaze aaa v pristupech  
postmap /etc/postfix/generic ... znovu nacte generic definice  
postconf ... vypis nastaveni postfixu  
postqueue -p ... ukaze maily ve fronte  
postqueue -f ... Vycisti frontu  
postsuper ... prace s frontou  
postsuper -r ALL ... vycisti frontu  

### POP3/IMAP - prichozi posta

POP3 = Post Office Protocol, IMAP=Internet Mail Access Protocol

rpm -i dovecot  
iptables -p tcp --dports 110,143,993,995 -j ACCEPT ... pop, imap, imaps, pop3s  
service dovecot start/stop/status/restart/reload  
/usr/sbin/dovecot  
/etc/dovecot.conf  
/usr/share/doc/dovecot-*/examples/mkcert.sh ... skript na vytvoreni certifikatu (Nastaveni je v /etc/pli/dovecot/dovecot-openssl.cnf)  
make -C /etc/pkt/tls/certs dovecot.pem ... vytvori ssl klic  

### FTP

service inetd start/stop/status  
service vsftpd status  
/etc/inetd ... nastaveni FTP - zakazat, povolit  
/etc/vsftpd/vsftpd.conf ... parametry FTP  

### NFS

service nfs start/stop/status  
service nfslock status ... lock demon (lockd) - automaticky se spusti s nfs  
service portmap status ... portmaper - automatiky se spusti s nfs  
procesy: statd, mountd, rquotad, nlockmgr (lockd)  
/etc/sysconfig/nfs ... nastaveni portu atd.  
/etc/exports ... konfigurace sdilenych FS  
exportfs ... nacteni konfigurace z konf. souboru  
rpcinfo -p ... seznam protokolu, ktere jedou v portmapu  
showmount -d server1 ... ukaze vsechny exportovane adresare na serveru server1  
showmount --all ... ukaze kdo ma naexportovany jaky adresar  
man nfs ... napoveda k parametrum FS nfs  

### Samba

rpm -i samba samba-common smbclient  
iptables -A INPUT -p udp --dport 137,139 -j ACCEPT ... povoleni Netbios Name service a Netbios Datagram Service (Klient)  
iptables -A INPUT -p tcp --dport 139,445 -j ACCEPT ... povoleni Netbios session service a Microsoft Domain Service, navic pro server  
service smb start/stop/status  
service nmb start/stop/status ... spusti Netbios  
/etc/samba/smb.conf  
/etc/samba/smbusers ... nastaveni samba uzivatelu jako lokalni uzivatele  
/etc/samba/passdb.tdb  
winbind ... vyuziti uctu z WIndows domeny na siti  
findsmb ... projde okolni netbiosy a vypise seznam serveru  
mount -t cifs //station/share /mnt -o user=user,dom=dom,uid=500,file_mode=644 ... FS k pripojeni Samba/Windows FS  
mount -t smbfs //station/share /mnt -o creditials=/etc/samba/cred.txt ... autentifikace ze souboru (username=XXX\npassword=YYY)  
net ... utilita pro praci s WINS a NETBIOS protokoly  
net -l user -S server -U user ... ukaze vsechny uzivatele na serveru server  
net -l share -S server ... ukaze sdilene polozky  
nmblookup IDC01 ... pripoji se k nmbd IDC01 a zjisti IP adresu Netbios serveru IDC01  
pdbedit -L ... seznam uzivatelu samby  
rpcclient ... prace s windows rpc  
smbcacl ... prace s pristupovymi pravy (ACL  
smbpasswd -a joe .. prida uzivatele joe do /etx/samba/passdb.tdb  
smbclient ... klient na vyuzivani sluzeb Windows a Samba serveru smbd  
smbclient -L server -U 'bob' ... pripoji se k serveru server uzivatelskym jmenem bob  
smbclient //hostname/share  
smbmount //192.168.1.2/Music /home/dbott/music -o username=dbott,password=mysecretpassword,uid=1000,mask=000 ... namountuje samba disk  
smbumount /home/dbott/music ... odmountuje disk  
smbspool ... prace s windows tiskarnami  
smbstatus ... vypise, kdo vyuziva jake samba sluzby  
smbtree ... prozkouma celou Windwos skupinu a napise cleny  
tdbdump ... prohlizeni /etc/samba/passdb/tdb  
testparam smb.conf ... otestuje spravnost konfiguracniho souboru  
wbinfo ... informace o bezicim winbind demonu  
Dokumentace: /usr/share/doc/samba-*/*  

### CUPS - tisk

cupd - Common Unix Printing System (IPP: port 631)

iptables -p tcp --dport 631 -j ACCEPT  
service cups start/stop/status ... cups klient  
service cups-lpd start/stop/status ... cups server  
##### konfiguracni soubory

/etc/cups/cups.conf  
/etc/cups/printers.conf  
##### tiskove fronty

lpadmin ... konfigurace cups  
lpadmin -d lj4 ... nastavi tiskarnu lj4 jako vychozi  
lpadmin -x lj4 ... zmaze tiskovou frontu (tiskarnu)  
lpadmin -p lj4 -v parallel:/dev/lp0 -m laserjet.ppd.gz ... prida mistni tiskarnu  
lpadmin -p DeskJet -E -v socket://11.22.33.44 -m deskjet.ppd ... prida sitovou tiskarnu, prenos sifrovany  
lpadmin -p Tiskarna1 -v "lpd://localhost/dummy" -m textonly.ppd ... vytvori falesnou tiskarnu - text only  
lpadmin -P Tiskarna -E ... povoli tiskovou frontu  
lpoptions ...ukaze a meni parametry tiskarny  
lpoptions -d PRINTER ... nastavi tiskovou frontu PRINTER jako vychozi  
lpstat -a ... informace o vsech frontach  
lpinfo -l ... ukaze dostupne zarizeni a ovladace  
cupsenable lj4 ... povoli tisk uloh z tiskove fronty  
accept ... povoli prijmani uloh do tiskove fronty  
reject ... zakaze prijmani uloh do tiskove fronty  
##### tiskove ulohy

ls | lp -d lj4 -n ... posle vystup ls do fronjy lj4, a.ps se vytiskne 2x  
lpr -P lj4 -3 help.ps ... vytiskne help.ps ve trech kopiich na lj4  
lprm -P lj4 32 ... odstrani tiskovou ulohu 32 z fronty lj4  
lpmove lj5 lj4 ... presune ulohy z lj5 do lj4  
cancel lj4 23 ... zrusi tiskovou ulohu 23 v tiskove fronte 23  

### syslogd

service syslogd start/stop/status  
/etc/sysconfig/syslog  
/etc/syslog.conf  
logger -i -t USER "Message for syslog" ... posle zpravu "Message for syslog" syslod demonovi s informaci, ze je to od uzivatele USER  

### Matahari

Nastroj na vzdalene ovladani pocitacu pomoci sluzbe zprav bezicich na pocitacich

yum install [matahari](http://fedoraproject.org/wiki/Features/Matahari)  

### SPICE

Protokol pro vzdalenou (virtualni) plochu

yum install spice-client  

#### deltacloud

Sada nastroju na vytvoreni cloudu

### ABRT

Nastroj na spravu padu aplikaci - umi posbirat data o zhavarovane aplikaci a udelat s nimi prislusnou akci

### PAM

[Popis zakladu PAM na root.cz](https://www.root.cz/clanky/pam-sprava-autentizacnich-mechanismu/)

/lib/security/, /usr/lib64/security/ ... zde jsou moduly pro PAM  
/etc/security/ ... konfiguracni soubory  
/etc/pam.d/ ... konfigurace pro aplikace. Pokud soubor pro aplikaci chybi, pouzije se other  
##### Struktura:

auth|account|password|session required|requisite|sufficient|optional|include|[[] ](http://www.linux-pam.org/Linux-PAM-html/sag-configuration-file.html) modul|soubor  
priklad "OR" operatoru: [default=cislo - ekvivalent goto](https://unix.stackexchange.com/questions/353272/using-pam-succeed-if-so-to-allow-passwordless-su-for-a-given-group)
##### priklad:

auth sufficient pam_root_ok.so ... pro _autentifikaci_ _staci_ aby byl uzivatel root  
auth required pam_deny.so ... pro _autentifikaci_ se _vyzaduje_ nepovolit  
auth sufficient pam_permit.so ... pro _autentifikaci_ _staci_ aby byl uzivatel pusten  
auth requisite pam_unix.so ... pro _autentifikaci_ je _nutne a staci_ tradicni unix autentifikace (dalsi radky se ignoruji)  
auth requisite pam_succeed_if.so uid >= 500 quiet ... pro _autentifikaci_ je _nutne a staci_  aby UID bylo vetsi-rovno 500  
auth requisite pam_tally.so deny=3 unlock=300 ... kdyz se zada 3x spatne heslo, uzivatel se zablokuje (faillog)  
auth reqisite pam_nologin  
auth [user_unknow=ignore success=ok ignore=ignore auth_err=die default=bad] pam_securetty.so ... slozitejsi podminka: Nepusti nikoho krome roota, povoli mu pristup na specialni zarizeni  
passwd include common-password ... pro _zmenu hesla_ _precist instrukce z_ common-password  
##### napoveda

man -k pam_ ... prehled modulu a jejich popis  

##### moduly

[pam_listfile](https://linux.die.net/man/8/pam_listfile) ... seznam uzivatelu, skupin, ...  
[pam_sss](https://linux.die.net/man/8/pam_sss) ... pouziti sssd  
pam_cracklib ... kontrola sily hesla  
pam_deny ... selhani  
pam_krb5 ... kerberos  
pam_limits .. nastaveni systémových limitu (pamet, procesor, ..)  
pam_nologin ... kontrola existencie /etc/nologin. Kdyz soubor existuje, prihlasi se jen root  
pam_time .. pristup podle casu  
pam_unix ... Kontroluje užívateľov a heslá podľa /etc/passwd a /etc/shadow  
pam_warn – zaznamená do systémového logu pokus o prístup  

### NIS

server, klient - Network Information Server - sdili /etc/passwd, /etc/shadow, /etc/groups, /etc/gpasswd
##### NIS server

balicky: rpm -i ypserv ypbind yp-tools portmap  
SElinux bools: allow_ypbind  
konfiguracni soubory: /etc/sysconfig/network, /etc/ypserv.conf, /var/yp/*, etc/sysconfig/yppasswdd  
service portmap start ... postmaper  
service yppassedd start ... NIS password change demon  
service ypserv start ... NIS server  
domainname aaa ... nastavi NISDOMAIN (nastavuje se tez v /etc/sysconfig/network>  
(service ypxfrd start) ... NIS transfer diractory server pro prenos na sekundarni NIS servery  
/usr/lib/yp/ypinit -m ... vytvoreni NIS databaze ve /var/yp/DOMAIN/  
cd /var/yp/DOMAIN/;make ... prekompiluje daa do map  
/usr/lib/yp/ypxfr MAPfile ... prenese MAPu z primarniho serveru  

##### NIS klient

rpm -i ypbind  
/etc/yp.conf - nastaveni NIS serveru  
/etc/nsswitch.conf - nastaveni, jake NSS zdroje informaci budou akceptovany (local files, NIS, LDAP, atd)  
authconfig --enablenis --nisdomain=example.com --nisserver=instructor.example.com --update ... zapne NIS autentifikaci  
authconfig --disablenis --update ... vypne NIS autentifikaci  
service ypbind start ... start NIS klienta  
getent passwd USER1 ... dotaze se na passwd data o uzivateli USER1  
ypcat passwd.byname ... vylistuje ze serveru passwd by name  
ypwhich -m ... seznam map na NIS serveru  
yppasswd -l aaa ... zmeni shell uzivatele aaa  
yptest  

### LDAP - Lighweight Directory Access Protocol

/etc/nsswitch.conf nastaveni ldap autentifikace  

##### LDAP server

rpm -i openldap openldap-server  
iptables -L input -p tcp,udp -dport 636,389 -j enable ... povoleni portu ve firewallu  
/etc/openldap/slapd.conf, /var/lib/ldap/DB_CONFIG, /etc/openldap/schema/*, /etc/pki/tls/certs/*  
slapadd -v -l example.ldif ... inicializuje LDAP databazi, zapise je v /var/lib/ldap/  
chown ldap.ldap /var/lib/ldap/*
service ldap start ... spusti ldap server  
slapcat ... vypis hodnot v LDAP databazi  
ldapmodify -s -f modify.ldif ... pridava, ubira, modifikuje zaznamy v LDAP databazi, jednoducha autentifikace  
service ldap stop;slapindex;service ldap start ... preindexovani databaze  

##### LDAP klient

rpm -i nss_ldap openldap openldap-clients  
slapd  
/etc/ldap.conf ... specifikuje, adresu LDAP serveru, DN, TLS sifrovani  
/etc/openldap/ldap.conf ... specifikuje, adresu LDAP serveru, DN, TLS sifrovani pro manualni dotazy pomoci prikazu ldap klienta (ldapsearch -x -Z)  
authconfig %%--%%enableldap %%--%%ldapserver=instructor.example.com %%--%%ldapbasedn=dc=example,dc=com %%--%%ldaploadcacert=ftp://instructor/pub/cacert %%--%%update ... zapne LDAP informace o uzivatelich  
authconfig %%--%%enableldapauth %%--%%ldapserver=instructor.example.com %%--%%ldapbasedn=dc=example,dc=com %%--%%ldaploadcacert=ftp://instructor/pub/cacert %%--%%update ... zapne LDAP autentifikaci  
authconfig %%--%%disableldap %%--%%update ... vypne LDAP informace o uzivatelich  
authconfig %%--%%disableldapauth %%--%%update ... vypne LDAP autentifikaci  
slapcat ... vypis hodnot v LDAP databazi  
ldapsearch -b 'dc=example,dc=com' '(objectclass=*)' ... (balicek openldap-clients) dela  dotazy na ldap server  
ldapsearch -b dc=local -D admin@local -H ldap://localhost -w $pwd "(mail=aaa@local)" cn ... zobrazi polozku cn pro filtr mail=aaa@local  
ldapmodify -D 'cn=root,dc=example,dc=com' -W -f modify.ldif ... pridava, ubira, modifikuje zaznamy v LDAP databazi, pta se na heslo pro root  

### Kerberos

**server**  
rpm -i krb5-server krb5-workstation (ntp)
iptables -L input -p tcp,udp -dport 88,464,749,543,2105  -j enable ... povoleni portu ve firewallu fpr kerberos, kpasswd, kadmin a 2x klogi  
/etc/krb5.conf  
/usr/kerberos/sbin/kdb5_utl create -r REALM -s ... vytvori dazabazi REALM ve /var/kerberos/krb5kdc/*  
kadmin.local ... lokalni administrace kerberos  
kadmin ... vzdalena admonistrace kerberos  
service krb5kdc start ... spusteni kerberos  
service kadmin start ... spusteni kadmina  
**klient**  
rpm -i krb5-workstation  
/etc/krb5.conf ... konfiguracni soubor  
realm discover ifs.ori.local ...
/usr/kerberos/bin/telnet,ftp,rsh,rcp ... kerberos telnet,ftp,rsh,rcp  
kpasswd ... zmena kerberos hesla  
ksu ... kerberos su  
[kinit](https://web.mit.edu/kerberos/krb5-devel/doc/user/tkt_mgmt.html) ... vytvoreni ticketu s oberenim hesla na 10 hodin  
kinit -f -l 3h david@EXAMPLE.COM ... vytvoreni forwardovatelneho ticketu na jine pocitace s expiraci 3 hodiny  
kinit username@MYDOMAIN.COM -k -t /etc/krb5.keytab ... autentifikace pomoci klicenky  
klist -f ... seznam aktualnich Kerberos ticketu,  vcetne flagu  
kdestroy ... zruseni existujiciho ticketu  
ktutil ... spusti nastroj na administraci klicenky  
kvno XXX/YYY ... XXX/YYY je adresa z klist - vypise verzi klice Kerberos principal  

### AD authentifikace (Active Directory)

**samba**  
rpm -i pam_smb  
/etc/pam_smb.conf, /etc/pam.d/system-auth  
**[winbind](http://samba.org/samba/docs/man/Samba3-HOWTO/winbind.html)**  
rpm -i samba-common, adcli  
/etc/pam.d/system.auth  
smbd  -b | grep CONFIGFILE ... konfiguracni soubor Samby  
adcli info DOMAIN ... informace o domene  
adcli join -D DOMAIN -U tomas@DOMAIN -W --show-details -v ... pripojeni do domeny - musi existovat zaznam computer v AD a musi mit pravo na zapis od uzivatele tomas  

### FreeIPA

[FreeIPA](http://freeipa.org/) je reseni bezpecnostniho informacniho managementu kombinujici Linux (Fedora), 389 (Fedora Directory Server), MIT Kerberos, NTP, DNS. Sklada se z weboveho ovladacio prostredi a prikazu.

### SSSD - System Security Services Daemon

[SSSD](https://fedorahosted.org/sssd/) je systemovy demon, jehoz hlavni funkci je umoznit pristup k ID a autentifikace vzdalenych prostredku pomoci obecnehych nastroju. Poskytuje
caching a offline podporu na systemu, PAM a NSS moduly a bude obsahovat D-BUS interfejs, k rozsireni uzivatelskych informaci.
sudo sssd -d9 -i ... spusteni sssd mimo sluzbu pro detailni informace o chybe  
journalctl -u sssd ... log sluzby  
systemctl restart sssd .... restart sluzy  
/etc/sssd/sssd.conf ... konfigurace - v kazde sekci je treba specifikovat debug_level = 6 pro lepsi debug  
/var/log/sssd/ ... logy  
sss_cache --everything ... vysypani cache  
[troubleshooting1](https://docs.pagure.org/SSSD.sssd/users/sudo_troubleshooting.html) a
[troubleshooting2](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/troubleshooting-sudo)  
ldbsearch -H /var/lib/sss/db/cache_$domain.ldb -b cn=sysdb '$filter' ... prohlizeni cache  

### auditd

service auditd start/stop/status  
/etc/audit/*  
/var/log/audit/audit.log  
ausearch  
aureport  

### cron

service cron start/stop/status  
/etc/cron.allow  
/etc/cron.deny  
crontab -l ... seznam naplanovanych uloh  
crontab -e ... editace naplanovanych uloh  

### System crontab

/etc/crontab ... konfiguracni soubor  
/etc/cron.* ... adresare se spoustenymi skripty  

### SELinux

Security extended Linux - vetsi zabezpeceni prav pro soubory - cast jadra

/etc/sysconfig/selinux ... nastaveni SELinuxu  
ls -Z ... seznam prav pro soubory  
ps -Z ... seznam prav pro procesy  
chcon -t etc_t install.log ... zmeni prava na etc_t  
chcon --reference /etc/passwd /var/log/messg ... zmeni prava /var/log/messg podle /etc/passwd  
restorecon /root/* ... vrati prava souboru (a adresaru /root/*) na puvodni prava (definovana)  
getenforce ... ukaze miru zabezpeceni - Enforcing - brani vyuzivani nevhodnych souboru, Permissive - jen loguje  
setenforce 0 ... prepne rezim z Enforce na Permissive  
getsebool -a ... vylistuje prepinace booleans  
setsebool -P allow_ftpd_anon_write on ... pernamentne povoli anonymni upload  
semanage ... nastavuje a ukazuje nadefinovana pravidla  
semenage fcontext -l | cut -d: -f3 | sorn -u | grep "named.*_t" ... vylistuje typy souboru pro proces named  
service setroubleshootd start ... bere logy z audit.log a okomentovane vkladaa do messages  
sealert ... vypisuje okomentovane logy z messages  
man 0 selinux  
man httpd_selinux samba_selinux ftpd_delinux named_selinux nfs_selinux  

### Anaconda

### homed

systemctl status systemd-homed ... stav služby  
homectl ... seznam uživatelů  
homectl create UZIVATEL ... vytvoří uživatele  

### MRG

Massages, Realtime, Grid - [MRG](http://www.redhat.com/f/pdf/MRG_whitepaper_web.pdf) je sada nastroju, vcedte casti jadra, konfiguracnich nastroju, nastroju na monitorovani vykonu,
AMQP zprav, podpora virtualizace (posilani virtualnich stroju) a jinych, na vybudovani infrastruktury vyuzivajici lipe prostredku a zvyseni celkoveho vykonu

yum install condor  

### ostatni

[amanda](http://www.amanda.org) ... zalohovaci server  
[nagios](http://nagios.sourceforge.net/docs/) ... monitorovaci sluzba - monitoruje stroje, sluzby, FS a tvori alerty  
logwatch ... dela denni prehledy log souboru  
/etc/logwatch/conf/logwatch.conf  
logrotate ... rotuje log soubory  
/etc/logrotate.conf  
tmpwatch ... cisti stare soubory ve specifickych adresarich  
anacron ... spousti cron ulohy, ktere nebyly spustene behem doby, kdy byl pocitac vypnuty  
/etc/acacrontab  
service autofs start/stop/status ... automounter  
/etc/auto.master  
rpm -i xinetd
/etc/xinetd.conf
service xinetd start/stop/status/restart/reload

```
	chkconfig kudzu off        # Annoying RedHat new hardware detection
	chkconfig isdn off         # ISDN controller
	chkconfig nscd off         # Network authentication (not needed when standalone)
	chkconfig gpm off          # Some kind of mouse server
	chkconfig sendmail off     # Mail utility (not needed for non-server)
	chkconfig netfs off        # Automatically mount network file systems
	chkconfig ntpd off         # Network Time Protocol daemon (not needed when standalone)
	chkconfig autofs off       # Automounter
	chkconfig rawdevices off   # Creates raw devices for Oracle, etc.
	
	chkconfig cups off         # Printer daemon (not needed if you don't have a printer)
	chkconfig postfix off      # Postfix mail system (not needed for non-server)
	chkconfig smpppd off       # SuSE meta PPP daemon
	chkconfig fbset off        # Framebuffer devices ?
	chkconfig splash off
	chkconfig splash_early off
	chkconfig splash_late off
```
