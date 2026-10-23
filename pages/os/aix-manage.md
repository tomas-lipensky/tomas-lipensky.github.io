# AIX - Sprava systemu, balicky, uzivatele, ...

### Externi odkazy

[AIX 6.1](http://www.ibm.com/support/knowledgecenter/ssw_aix_61/com.ibm.aix.base/kc_welcome_61.htm) - oficialni stranka podpory  
[AIX komunita na DW](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/AIX)  
[Prikazy](http://l-gee.net/unix/table_aix.html)  
RPM balicky: [AIX Toolbox](ftp://public.dhe.ibm.com/aix/freeSoftware/aixtoolbox/RPMS/ppc/)  
RPM balicky: [AIX Toolbox for Linux Applications](http://www-03.ibm.com/systems/power/software/aix/linux/toolbox/rpmgroups.html)  
RPM balicky: [Perzl.org](http://www.perzl.org/aix/)  
RPM balicky: [oss4aix.org](http://www.oss4aix.org/download/everything/RPMS/)  

### Uzivatele

aixpert -f mysec.xml ... importuje bezpecnostni politiky ze souboru mysec.xml  
chdev -l sys0 -a enhanced_RBAC='true' ... po rebootu aktivace [RBAC](http://www.ibm.com/developerworks/aix/library/au-aix_rbac/index.html) (Role Based Authentication Control)  
chdev -l sys0 -a max_logname=10 ... povoli loginy o max delce 10 znaku  
chuser unsuccessful_login_count=0 UZIVATEL ... zastavi parametr pro uzivatele UZIVATEL  
lssec -f /etc/security/lastlog -s root -a unsuccessful_login_count ... ukaze pocet neuspesnych loginu roota  
lsuser UZIVATEL ... Vupise parametry uzivatele UZIVATEL  
lsuser -R LDAP -a id gecos ALL ... vypise vsechny ldap uzivatele  
lsgroup ALL ... vylistuje vzechnu skupiny a jejich parametry  
mkuser AAA ... vytvori uzivatele AAA  
mkgroup adms=john,mary DELIVERY ... vytvori skupinu delivery, kterou spravuji admini john a mary  
mkrole authorizations=aix.wpar.system newRole ... vytvori novou roli pro zapinani/vypinani wparu v RBAC. Musi se jeste aplikovat setkst  
passwd UZIVATEL ... proveze zmenu hesla pro uzivatele UZIVATEL  
pwdadm -c UZIVATEL ... nastavi, ze heslo pro uzivatele UZIVATEL nevyprsi  
rmuser UZIVATEL ... Smaze uzivatel UZIVATEL  
echo "user:n3w_p466w0rd" | /bin/chpasswd -c ... zmeni heslo z prikazoveho radku, nekryptovane heslo  
echo $UNAME:$NEWHASH | /usr/bin/chpasswd -e ... meneni hesla z prikazoveho radku, kryptovane heslo v argumentu  
chsec -f /etc/security/user -s default -a logintimes=:0800-1700 ... zmeni v /etc/security/user pro vsechny uzivatele hodnotu logintimes (mohou se pripojova mezi 8:00 az 17:00  
chsec -f /etc/security/lastlog -a unsuccessful_login_count=0 -s USER ... vynuluje neuzpesne pokusy o prihlaseni pro uzivatele  
setkst -t role chuser roles=newRole defailt_roles=newRole user1 ... priradi se uzivateli user1 role newRole a aplikuje se v kernel security tables  
usrck ... zkontroluje definice uzivatelu v /etc/passwd  
/etc/security/mkuser.default ... definice nove vytvorenych uzivatelu  
/etc/security/limits  
/etc/nologin ... pokud existuje tento soubor, uzivatele se nemohou pripojit  

### Balicky

/usr/sbin/emgr -P ... zobrazi zamknute balicky  
emgr -r -L DbgKernel ... Odebere vnitrni upravu jadra, ktera se jmenuje DbgKernel  
/var/adm/ras/emgr.log ... emgr logy  
epkg ... vytvareni EFIXu - interim Fixu ... zaplat, ktere jeste nejsou soucasti SP  
emgr -l ... souhrn nainstalovanych aparu  
inutoc . ... vytvori indexovy souvor .toc s popisy balicku a zavislostmi  
instfix -ic ... seznam vsech fixu, ktere jsou pokryty nainstalovanou verzi  
instfix -ik IZ05535 ... ukaze, zda fix byl nainstalovany  
instfix -icqv | grep ':-:' ... ukaze, ktere filesety chybyaktualni verzi AIXu nainstalovane na systemu  
installp ... instalace balicku  
installp -a -d. gskta.rte ... nainstaluje balicek gskta.rte  
installp -a -d . * ... nainstaluji vsechny balicky v tomto adresari  
installp -u ... odinstalace balicku  
geninstall -I "a -cgNQqwX -J"  -Z   -d . ... instalace balicku  
geninstall -I "a -cgNqwX -J"  -Z   -d . -f File ... instalace rte  
geninstall -d . robi.rte ... instalace balicku z aktualniho adresare  
lppchk -v ... zkontroluje konzistenci nainstalovanych balicku  
lppchk -l ... zkontroluje symbolicke linky balicku  
lslpp -l bos.rte.* ... vypise seznam vsech balicku, ktere zacinaji na bos.rte.  
lslpp -h ... vypuse datmy, kdy se nainstalovaly (patchovaly) jednotlive balicky  
lslpp -w /usr/bin/lssec ... ukaze, do ktereho balicku patri /usr/bin/lssec  
lslpp -f bos.rte.security ... seznam vsech souboru balicku bos.rte.security  
mkinstallp -d /tmp/pkg ... interaktivni vytvareni bff balicku  
[mklpp](http://ramses.smeyers.be/varia/aix/createlpp/) ... vytvareni lpp balicku  
smitty install_all  
smitty bffcreate ... vytvori bff balicky z instalacnich medii  
updateios -commit ... upgrade (VIO? serveru?)  
updateios -install -accept -dev 'FixPack11.1 path'  
ioslevel  
http://www-933.ibm.com/support/fixcentral/main/System+p/AIX ... Fixy a nove TL a ML  

#### Zarizeni

bindprocessor -q ... ukaze virtualni procesory
bootinfo &#8211;r ... vypis velikosti pameti  
bootinfo -K ... pocet bitu (32/64) architektury  
bootinfo -s hdisk0 ... velikost disku hdisk0  
chattr ... meni parametry ovladacu  
chdev -dev hdisk1 -attr reserve_policy=no_reserve ... nastavi zarizeni hdisk1, ze jde pouzit na vice jak jednom VIO  
cfgmgr (-v)... detekuje nove zarizeni (ukecany vypis)  
cfgmgr -v -l scsi0 -v ... detekuje a nastavi nove zarizeni scsi0 a jeho deti, ukecany vypis  
cfgmgr -vl ssar ... detekuje a nastavi SSA zarizeni  
sfgmgr -i lpp_source ... nainstaluje filesety s ovladaci k zarizenim, ktere nemaji ovladac  
drslot ... (Dynamicly reconfigure slot) spravuje a dynamicky meni sloty (napriklad hot-plug vkladani PCI karet do slotu)  
getconf ... informace o nastaveni systemu (kernel atd.)  
lparstat -i ... informace o lparu  
lsattr -El fscsi6 ... vypise nastaveni zarizeni fscsi6  
lsarrt &#8211;E &#8211;l sys0 &#8211;a realmem|systemid ... vypis velikosti pameti|S/N  
lsattr  -El  en0 ... parametry driveru  
lsattr  -El  ent0 ... parametry hardwaru  
lscfg ... Seznam nastavenych zarizeni a jejich fyzicka adresa v pocitaci (Unit.Model.S/N-lokace-slot)  
lscfg -vpl hdisk1|proc0|mem0 ... vypis informaci o disku hdsik1 (vyrobce, typ ..)  
lsdev -Cc (h)disk|adapter|if|tape ... seznam daneho druhu zarizeni vcetne fyzicke lokace a typu  
lsdev -Cs vscsi|scsi|pci ... (=lsparent -Ck scsi) seznam zarizeni tridy scsi  
lsdev -l hdisk2 -H ... vypise zarizeni hdisk2 a Hlavicky atributu  
lsdev -p fscsi6 ... vypise vsechny deti zarizeni fscsi6  
lsdev -Cl hdisk2 -F parent ... ukaze rodicovske zarizeni pro hdisk3  
lsdev -P -c tape -F "type subclass description" ... jake vsechny paskove mechaniky jsou podporovany  
lsdevfc ... vylistuje fibre channel zarizeni
lsdisp ... ukaze nainstalovane graficke adaptery  
lsparent -C-l hdisk9 ... ukaze rodicovske zarizeni pro hdisk9  
lsrsrc "IBM.ManagementServer" ... ukaze HMC server, pokud je  
lsslot -c pci ... informace o pci slotech (zarizeni, lokace)  
lsslot -c slot ... vypis zarizeni a jejich slotu  
lssyscfg -m Server-9117-570-SN65B2E80 -r lpar -F name ... Ukaze jmena virtualnich podstroju (LPARu)  
lsvpd ... Ukaze Vital Product Data (SN, typ, model atd) systemu  
lvlstmajor ... seznam major cisel k zarizenim  
mkdev ... vytvareni zarizeni v ODB  
mkdev -c disk -s scsi -t type -p scsi1 -w whereconnected -a pv=yes ... vytvori zarizeni scsi disk na radici scsi1 s parametrem PV  
mkdev -d -c disk -s scsi -t osdisk -p scsi0 -w x,0 ... Nastavi zarizeni "jiny systemovy SCSI disk" do "defined" stavu  
mkdiv -l hdisk2 ... Nastavi zarizeni podle preddefinovanych parametru v PdDev  
mkvdev -vdev <hdisk> -vadapter <vhost> -dev <vtd> ... vytvori virtualni zarizeni (hdisk na adapteru vhost bude mit jmeno vtd\\chdev -dev <hdisk> -attr pv=yes ... vytvori PVID pro hdisk  
oslevel -s ... ukaze verzi, ML, a TL AIXu  
oslevel -rl 5300-06 ... ukaze, ktere baliky chybi do TL 06  
prtconf ... souhrne informace o Systemu, Hw atd.  
rmdev -l en1 -d ... vymaze ovladac sitove karty  
rmdev -l ent1 -d ... vymaze informace o HW sitove karty  
rmdev -l pci2 -R ... rekurzivni odstraneni zarizeni  
rmss -c 512 ... emuluje 512 MB pameti  
rmss -r ... vypne emulaci pameti  
schedo -a ... vypise parametry procesoru  
schedo -o vpm-xvcpus=-1 ... vypne dynamicke meneni poctu virtualnich procesoru (VP Folding)  
schedo -o smt_snooze_delay ... Ukaze parametr SMT snoozing (lze zjistit i lsattr -El proc0)  
smtctl ... zobrazi/zmeni stav SMT (Simultaneous multi-threading). Pro parametru boot se musi udelat bosboot -a  
uname -a ... ID pocitace + OS  
/usr/lpp/EMC/CLARiiON/bin/inq.aix32_51 -clar_wwn ... informace o storage a lunech na Clarionu  

#### [Firmware a aovladace](http://www.ibm.com/developerworks/wikis/display/WikiPtype/p5+System+Firmware+Upgrade)

[Link](http://www-933.ibm.com/support/fixcentral/firmware/supportedCombinations) na podporovane firmware u jednotlivych stroju  
lsmcode -c ... ukaze Firmware  
lsmcode -rd ent0 ... ukaze firmware sitove karty  
lsmcode -A ... ukaze vsechny firmware  
/usr/lpp/diagnostics/bin/update_flash -v -f 01SF240_382_382 ... otestuje Firmware, zda je OK  
/usr/lpp/diagnostics/bin/update_flash -f 01SF240_382_382 ... aplikuje Firmware  
/usr/lpp/diagnostics/bin/update_flash -r ... Reject Frimware - Prehraje Temporary FW tim,co je v Pernament FW  
ldfware -file 01EA3xx_yyy_zzz ... update na vio  
invscout ... oscanuje vsechna zarizeni a vypise jejich firmware (vcetne systemoveho frimware Power masiny)  
[ftp://ftp.software.ibm.com/software/server/firmware/catalog.mic](ftp://ftp.software.ibm.com/software/server/firmware/catalog.mic) ... nejnovejsi databaze ovladacu pro invscout  
/var/adm/invscout/microcode/catalog.mic ... lokace katalogu ovladacu (firmware, microcode)  
[https://www-304.ibm.com/webapp/set2/mds/mds](https://www-304.ibm.com/webapp/set2/mds/mds ) ... misto na upload vystupu invscout (*.mup) - analyzuje vystup, doporuci upgrade, doda linky i postup  

### Jadro

/etc/tunables/nextboot ... nastaveni paramertu jadra pro dalsi reboot  
tuncheck -r -f nextboot ... zkontroluje parametry jadra v /etc/tunables/nextboot pro dalsi reboot  
smit load64bit ... zapne podporu 64-bitovych aplikaci na 32-bit. jadre  
/etc/tunables/lastboot ... parametry jadra po poslednim (soucasnem) startu OS  
ln -sf /usr/lib/boot/unix_64 /unix; ln -sf /usr/lib/boot/unix_64 /usr/lib/boot/unix; bosboot -ad ipldevice; shutdown -Fr ... zmena jadra na 64-bit  

### Procesy a vykon serveru

/usr/lpp/perfagent/daily.cf ... konfiguracni soubor pro xmwlm  
cat /proc/sys/fs/jfs2/memory_usage ... vyuziti bufferu (cache) file systemu - casti pameti pro cteni diskovych operaci dopredu  
dbx -a PID ... debuguje program (ukaze vlakna atd)  
dbx /usr/java/bin/java core ... debuguje core soubor  
[dbx](https://blogs.oracle.com/mandalika/entry/sun_studio_debugging_multi_threaded) ... prikazy: th-vypis vlaken, th info-info o vlaknech, detach-vyskoci a neukonci process, exit-vyskoci, ukonci process, registers-?, th 3 -info o vlaknu 3, thread current nb-?, cont - pokracuje ve vykonavani programu, what - vypise jake instrukce se zrovna vykonavaji  
ipcs -am ... ukazuje meziprocesovou komunikace (InterProcess CommunicationS)  
ipcrm -m ID ... zrusi meziprocesorovou komunikaci ID  
lvmstat -v rootvg -e ... povoli statistiky rootvg  
lvmstat -v rootvg 2 6 ukaze sest statistik po 2 sekundach  
lvmstat -l datalv -d ... zakaze statistiky datalv  
[perf53](ftp://service.boulder.ibm.com/aix/tools/perftools/perfpmr/perf53/) ... nastroj na posbirani dat o vykonosti AIX53  
procsig 111 ... ukaze signaly pro kill pro danny proces  
proctree PID ... strom rodicovskych procesu pro proces PID  
procwait ... pocka na konec procesu a ukaze status  
ps -fT 1111 ... ukaze stromovou strukturu procesu 1111 a podporocesu  
ps eww $PID ... ukaze promenne prostredi pro proces $PID  
ropasrec ... zaznamenava data topasu  
sa1 ... demon umoznujici chod sar  
sar -u report reporty do /var/adm/sa/sa07
svmon -Put 5 ... ukoze informace o 5 procesech nejvyce vyuzivajicich pamet  
svmon -U -t 10 -O summary=basic ... ukaze strucny vypis 10 uzivatelu, jez uzivaji nejvice pameti  
topas ... ukazuje momentalni vtizenost systemu  
topasout ... cte vystupu souboru zmwlm nebo topasrec  
tprof -skex sleep 4 ... provede analyzu behem trvani prikazu sleep - knihovny, spotreba CPU  
truss COMMAND ... tracuje prikaz COMMAND  
vmstat ... informace o pameti, cpu, paging space atd.  
[wlmcntrl](http://wiki.lodbrok.be/?n=WikiAIX.WikiAIXNote) ... AIX Workload manager  
wlmmon ... zpracovava zapisy xmwlm  
xmwlm ... zapisuje nektere vykonostni veliciny v prubehu casu, jako vyuziti pameti, cpu, disku, zapisuje do /etc/perf/daily. Soubory lze cist topasout  
/etc/.init.state ... ukaze aktualni run level  
**WLM** - WorkLoad Manageru - kontroluje vykon systemu, umi omezovat prostredky pro jednotlive aplikace. WSM je webova konfigurace WLM  
lswlmconf ... ukaze vsechny nadefinovane proofily WorkLoad Manageru  
lslwmconf -c ... ukase soucasnou konfiguraci  
confsetcntrl -C confset1 standard ... zkopirje konfiguraci standard na confsef1  
wlmcntrl -a ... Odstartuje [WLM](http://www.redbooks.ibm.com/abstracts/sg245977.html) v aktivnim modu  
wlmcntrl -p ... Odstartuje WLM v pasivnim modu  
wlmcntrl -o ... Zastavi WLM  
wlmstat 2 3 ... 3 vypisy statistiky WLM po 2 sekundach  
smitty wlmconfig ... nastaveni WLM  
smitty wlmclass_gal ... nastaveni trid WLM  
/etc/wlm/Config/limits, /etc/wlm/Config/shares ... konfiguracni soubory  
wlmcheck -d Config ... Ukaze tridy v profilu "Config"  
lsclass -C System ... Ukaze tridu System  
[lpar2rrd](http://www.lpar2rrd.com/) ... webovy tool na zubrazeni vykonnosti, pameti a konfigurace LPARu  

### informace o discich LVM, FS, PS, Dump

bootinfo -s hdisk0 ... velikost disku hdisk0  
lsdev -Cc adapter ... seznam radicu  
lsdev -Cc disk ... seznam disku  
lsdev -p hdisk0 ... ktery adapter ovlada disk hdisk0  
lsparent -Pl scsi0 ... ktere disky ovlada radic scsi0  
lscfg | grep disk ... nazvy disku  
lscfi -vl hdisk0 ... podrobne informace o disku hdisk0  
lsattr -El hdisk0 ... nastaveni driveru disku hdsik0  
lspath ... ktery radic ovlada ktery disk  
fget_config -vA ... informace o discich v diskovych polich  
datapath query adapter ... seznam radicu pro Fiber Chanel  
datapath query device ... seznam zarizeni fro FC  
datapath query essmap|grep hdisk1667 ... informace o disku v fiber chanel  
lsvp -a ... Vypis jednotlivych cesta a harddisku ve Fibre chanel  
lsvp -d ... seznam pozic v jednotlivych bay ve Fiberchanel  
lsvpcfg ... seznam nastaveni virtual path, prirazeni VG, atd.  
fcstat fscsi0 ... Stav a statistiky radice pro fiber chanel fscsi0  
lsdev -C -t hdisk -c disk -s ssar -H ... ukaze ssa disky  
ssaxlate -l hdisk5 ... info o ssa disku hdisk5  
lspv  
lsvg  
lsps  
lsfs  
bootlist -m normal -o ... ukaze poradi bootovani  
lsps -a ... ukaze paging space  
sysdumpdev -l ... ukaze aktivni sysdump disky  
sysdumpdev -e ... ukaze potrebne misto na system dump  
kdb ... analyza sysdumpu nebo karnelu  

### ODM

odmadd [parts.add](parts.cre.txt) ... prida polozky v parts.add do ODM (odm soubor parts je definovan v souboru)  
synclvodm ... synchronizuje LVM a ODM informace  
odmcreate [parts.cre](parts.cre.txt)  
odmchange -qpart_description=Wheel -oparts parts.change ... prepise zaznamy s popisem Wheel v ODM databazi parts informacema ze souboru  
odmdelete -qpart_description=Wheel -oparts ... mymaze polozku obsahujici Wheel z ODM databaze parts  
odmdrop -o parts ... zrusi celou ODM tabulku parts  
odmget -q "name=hdisk0 and attribute=pvid" CuAt ... Vypise z ODM databaze CuAt zaznamy, kde name=hdisk0 a attribute=pvid  
odmget -q name=hdisk3 CuDv | grep parent ... ukaze rodicovske zariceni pro hdisk3  
odmget -q parent=lhea0 CuDv | grep name ... ukaze vsechny detske zarizeni sitoveho hubu HEA (Host Ethernet adapter)  
odmget -q attribute=TCB_STATE PdAt ... zjisti, zda je zapnuty TCB (trusted computing base) (prikaz tcbck)  
odmshow CuAt ... ukaze datovou strukturu (definice promennych) ODM registru CuAt  
/etc/objrepos/CuAt ... CurrectAttributes  
$ODMDIR/CuDv ... CurrectDevices - zarizeni, LVM, atd.  
CuDep ... CurrectDependencies - Informace o LVM, atd.  
CuDvDr ... CurrectDevicesDrivers - minor/major cisla, atd.  
PdDv ... PredefinedDevices - preddefinovane parametry k zarizenim  
PdDvLn  

### Sluzby

lssrc -a ... seznam a stav vsech sluzeb  
lssrc -s tlmagent ... ukaze stav sluzby tlmagent  
lssrc -g tcpip ... stav vsech sludeb ve skupine tcpip  
refresh -s syslog ... Restartuje sluzbu syslog  
stopsrc -s inetd ... Zastavi sluzbu syslog  
startsrc -s inetd ... spusti sluzbu syslog  

### Chybove hlaseni, log soubory

alog -ot boot ... ?  
audit on ... zapne auditovani ([Popis auditu na ibm support](http://www-01.ibm.com/support/docview.wss?uid=isg3T1000212)  
audit off ... vypne auditovani  
audit query ... stav auditovani  
/etc/security/audit/ ... konfigurace  
cat /var/log/eprise/aaa | auditpr -v ... naformatuje Audit log na cteni (zobrazi audit)  
/var/adm/res/conslog ... log po rebootu - konzola  
chcore -c on -p on -n on -l /corefiles ... nastavi, aby dupm soubory se ukladaly do /corefiles, byly kompresovany a ve jmenu byl PID a cas padu aplikace  
lquerypv -h <core file> 64c ... ukaze, ktera aplikace dupm vyvolala  
errpt ... (error report) seznam vsech chybovych hlaseni  
errpt -aj XXXXX ... podrobny popis chyboveho hlaseni XXXXX  
/usr/lib/errdemon ... demon pro errpt  
/usr/lib/errdemon -l ... ukaze statistiky logu errpt  
file /core ... napise informaci o core souboru  
more /var/sna/sna.err ... chybove hlaseni  
errclear -d S 1 ... Smaze vsechny "S"oftwarove chyby starsi 1 dne  
errclear 0 ... smaze vsechny chyby z logu  
errlogger "To je test" ... vytvori chybove hlaseni s popisem "To je test"  
/usr/lib/errdemon -l ... informace o stavu hlasice chybovych hlaseni  
diag -a ... update nastaveni systemu  
diag -d sysplanar0 -c -L complete ... zapise Repair Acrion do errpt  
snap -r  
snap -a  
snap -gbc  
snap -D ... ziska /unix a dump soubor  
snapcore /home/root/core ... ziska data z core souboru a zabali je do PAX souboru vhodneho pro analyzovani SW chyby. Vysledek v /tmp/snapcore  
svmon ... analyzovani (nebo ziskani) obrazu virtualni pameti  
svmon -G ... ukaze statistiku virualni a normalni pameti  
/usr/lpp/diagnostics/bin/diagrpt -a ... diagnosticka zprava o kazdem zarizeni  
http://www.ahinc.com/aix/led.htm ... LED kody zobrazujici se na displeji chyb na bedne pocitace  

lsitab -a ... ukaze procesy, co se spousteji pri startu systemu  
chitab ... meni inittab  
rmitab ... bere veci z inittabu  
mkitab ... pridava do inittabu  
acctcom ... Ukaze historii procesu (cerpa z /var/adm/pacct)  
fwtmp < /var/adm/wtmp > /tmp/wtmp.txt ... manipulace se souborem wtmp - konverze a z wtmp formatu do textu  
/usr/sbin/acct/fwtmp -ic < /tmp/fwtmp.txt > /var/adm/wtmp ... konverze z txt do wtmp formatu  
tcrpt/trcstop/trace ... sleduje jadro a dela zapisy do log souboru  

#### accounting

/usr/lib/acct/turnacct on/off ... zapne/vypne accounting  
/usr/sbin/acct/ckpacct 10000 ... vypne accounting, necha jen pacct omezene velikosti a zbytek presune do pacct1, pote spusti accounting  
/usr/sbin/acct/acctcom pacct1 ... ukaze zaznamy (procesy) v pacct1  

### Ostatni

banner ... velike napisy  
swcons ... presmeruje vystup konzoly jinam  
pg ... jako more  
uux ... spusti na jinem unixu  
wall ... message for other logged users  
timex ... shows system activity during a command  
odmget -q attribute=TCB_STATE PdAt ... zjisti, zda je zapnuty TCM - Trusted Computer Base bezpecnostni system  
telinit m = shutdown -m ... Prepne OS do Single-user=Maintenance modu  
telinit q ... nastartuje nove veci v inittabu v aktualnim RC  

### terminal

tty ... vypise zarizeni aktualniho terminalu  
echo "ahoj" > `tty` vypise ahoj na aktualni terminal  
stty -a ... ukaze nastaveni klaves terminalu  
stty -echo ... nastavi aktualni terminal, ze nejsou videt znaky, ktere jdou z klavesnice
