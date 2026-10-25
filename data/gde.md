# Infosphere Guardium Data Encryption - GDE

### Externi odkazy

[System Requirements](http://www-01.ibm.com/support/docview.wss?uid=swg27027174)  
[Firewall pravidla pro GDE](http://www-01.ibm.com/support/docview.wss?uid=swg21569674)  
[Must gather skript ktery posbira dulezite informace o sluzbe](http://www-01.ibm.com/support/docview.wss?uid=swg21579891)  

## DSE

DSM - Data Security Manager - server, kde se spravuji (nastavuji) klice, agenti, politiky

Web management jede na portu 8445.

### Instalace DSE

[Popis instalace a registrace GDE](http://www-01.ibm.com/support/docview.wss?uid=swg21694412)  
[Problemy s instalaci](http://www-01.ibm.com/support/docview.wss?uid=swg21960032)  

#### Start/stop/info

service cgss restart  
/opt/vormetric/DataSecurityExpert/agent/vmd/bin/check_host  
ssh <host> -l cliadmin;  system; restart  
vmsec status | grep -i vmd_URL

### konfigurace

/opt/vormetric/DataSecurityExpert/agent/vmd/bin/register_host

### logy

/var/log/vormetric/vorvmd_root.log  
C:\ProgramData\Vormetric\DataSecurityExpert\agent\log\vorvmd.log  

### Ovladani prikazovou radkou

[vmssc](http://www.ibm.com/developerworks/cloud/library/cl-installguardium/)  -s $DSM_HOST_IP -u $DSM_LOGIN_NAME -p $DSM_LOGIN_PASSWD -d $DSM_DOMAIN server ... pripojeni na server  
./vmssc server show -h vormetric.dsm  
./vmssc host add -G $AGENT_HOST ... pridani hosta  
./vmssc key add -a -h 239-key  
./vmssc key show AgentKey-256 ... seznam klicu  
./vmssc policy add ... pridani politiky  
./vmssc policy show -f policy.xml default_wide_open_policy  
./vmssc host addgp -p default_wide_open_policy -d /tmp/VMSSC/encrypt $AGENT_HOST  

## FS Agent

Jiny nazev pro agenty je VTE - Vormetric Transparent Encryption, starsi nazev VEE - Vormetryc Encryption Expert

#### start/stop/info

service secfs start  
systemctl stop secfs-init  
systemctl stop secfs-fs  

vmd -v ... verze agenta  
/var/log/vormetric/vordb2_usr.log  
vmd/bin/agentinfo ... vytvori souhrn informaci o Agentovi napriklad pro IBM support  
vmd/bin/check_host -a -d ... hostname a IP adresa agenta  
vmd/bin/agent_cert_mgr vmd view certificate agentsrvr ... seznam certifikatu  
vmd/bin/agent_cert_mgr vmd view certificate agent ... seznam certifikatu  
vmd/bin/vmsec status ... status agenta  
vmd/bin/vmsec checkinstall ... otestuje zda jsou moduly jadra funkcni  
vmd/bin/dataxform --version  
secfsd -status guard ... sezanm aktivnich zabezpecenych Filesystemu  
secfsd -status auth  
secfsd -status lockstat  
secfsd -status policy ... seznam aktivnich politik  

#### install

./vee-fs-xxxxxx.bin ... interaktivni mod  
sh vee-fs-xxxxxx.bin -e ... rozbali jen balicek  

### Registrace agenta

vmd/bin/register_host
[Problemy s registraci agenta](http://www-01.ibm.com/support/docview.wss?uid=swg21694500)  
[Problemy se zastavenim agenta](http://www-01.ibm.com/support/docview.wss?uid=swg21689892)

```
cat 'SERVER_HOSTNAME=server
AGENT_HOST_NAME=agent
#AGENT_HOST_PORT=1212
#STRONG_ENTROPY=1 # pro pouziti /dev/random
#PKCS11_PASSWKORD=heslo - kdyz uz je agent registrovat
#ONEWAY_COMMS=0' &gt; vee-fs.txt
```

./vee-fs-xxxxxx.bin -s vee-fs.txt ... automaticky mod  
./vee-fs-xxxxxx.bin -e ... rozbali pouze pkg/bff/rpm balicek  
pkgadd -d ./vee-fs/*.pkg ... instalace na solarisu, pro bff, rpm se pouzije nativni prikaz pro instalaci balicku  
installp -aX -d ./vee-fs-*.bff vee.fs  
/opt/vormetric/DataSecutipyExpert/agent/vmd/bin/uninstall

### logy

/var/log/vormetric/secfsd.log  

## DB2 agent

db2 backup database testdb compress comprlib /opt/IBM/DB2TOOLS/LUWEncryptionExpert/agent/db2/lib/libeetdb2.so
