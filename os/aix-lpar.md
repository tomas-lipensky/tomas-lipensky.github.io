# AIX - LPAR a virtualizace

Logicke oddily - LPARy se spravuji bud z HMC, nebo z IVM (Integrated Virtual Manager), jez ma stejnou IP jako VIO  

## Obsah:

[Externi odkazy](#link)  
[Klient - LPAR](#lpar)  
[HMC](#hmc)
[VIOS - Virtual I/O Server](#vios)  

## Externi odkazy

HMC web kilent ... https://IP adresa HMC (Drive byl potreba WebSM)
IVM (Integrated Virtualization Manager) ... IP adresa VIO serveru
[IBM Support Fix Central](http://www-933.ibm.com/support/fixcentral/) ... podpora a update
[IBM Systm p Support](http://www-947.ibm.com/systems/support/supportsite.wss/brandmain?brandind=5000025)
[SPT](http://www-947.ibm.com/systems/support/tools/systemplanningtool/) system planning tool  
[VIOS](http://www14.software.ibm.com/webapp/set2/sas/f/vios/home.html)
[Dokumentace k VIOS](http://www14.software.ibm.com/webapp/set2/sas/f/vios/documentation/home.html)
[http://www-03.ibm.com/systems/power/hardware/cod/index.html>CoD - Capacity on Demand](http://www-03.ibm.com/systems/power/hardware/cod/index.html>CoD - Capacity on Demand)
[Linux on POWER machines](http://www-03.ibm.com/systems/power/software/linux/index.html)
[IBM Power Systems PowerVM](http://www-03.ibm.com/systems/power/software/virtualization/index.html)
[IBM Power systems - facts and features](http://www-03.ibm.com/systems/power/hardware/reports/factsfeatures.html)
[IBM Servers - storage](http://www-03.ibm.com/systems/storage/)
[IBM Support Line Supported Products List](http://www-03.ibm.com/services/sl/products/java2.html)
[Virtual Networking on AIX 5L](http://www-03.ibm.com/servers/aix/whitepapers/aix_vn.pdf)  
[IBM and Linux](http://www-03.ibm.com/linux/)  
[Redbooks](http://www.redbooks.com): PowerVM Virtualization on IBM System p
[IBM Product Information Centers](http://www.ibm.com/support/publications/us/library/)
[Seznam prikazu](http://publib.boulder.ibm.com/infocenter/eserver/v1r3s/index.jsp?topic=/iphcx/hmckickoff.htm)  
[Power 5/6 info](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp)
[IBM System p and AIX Infocenter](http://publib.boulder.ibm.com/infocenter/systems/index.jsp)
[Santoschovy stranky o AIX a LPARech](http://santosh-aix.blogspot.com/)  
[HMC How to](http://www.unixwerk.eu/aix/hmc-howto.html) ... pekne HOWTO - prikazy HMC  
[VIO How to](http://www.unixwerk.eu/aix/ios-howto.html) ... pekne HOWTO - prikazy VIO  
[Seznam HMC prikazu](http://aix4admins.blogspot.cz/2011/08/hmc-command-line-commands-have-help.html) ... velmi prehlene  
[LPAR4RRD](http://www.lpar2rrd.com/install.htm?4.1#fragment-8) - webovy interface na ziskani info z HMC o managovanych masinach  

## LPAR Klient - Logical Partition

##### AIX

uname -L ... ukaze ID a nazev LPARu  
lparstat -i ... informace o lparu  
lsdev -Cc disk -s vscsi ... Ukaze vsechny virtualni disky (disky z VIOS)  
lscfg -vpl hdisk2 ... ukaze vitalni data virtualniho disku hdisk2, potrebne k indentifikaci hdisu na VIOS  
/usr/sbin/rsct/bin/rmcctrl -z ... stop RMC demona  
/usr/sbin/rsct/bin/rmcctrl -A ... start RMC demona  
/usr/sbin/rsct/bin/rmcctrl -p ... povoli RMC demona pro vzdalene spojeni z HMC  
lsrsrc IBM.ManagementServer ... ukaze HMC, ktere spravuje LPAR, pokud je nadefinovan (RMC)  
/usr/sbin/rsrc/install/bin/recfgct ... reinicializuje cely RMC system na LPARu  
<b>[RMC](http://publibn.boulder.ibm.com/doc_link/Ja_JP/a_doc_lib/aixbman/rsct/rscttfrm.htm) (Resource Monitoring and Control), soucast RSCT (Real scalar cluster technology):</b>  
IBM.DMSRM ... na HMC registruje HMC v NVRAM a zapistuje tam sifrovaci klice  
IBM.CSMAgentRM ... na LPARu cte IP adresu HMC a sifrovaci klic z NVRAM na spravovanem systemu  
IBM.DRM ... na LPARu automaticke pripojeni k HMC s daty od CSMAgenta  
IBM.ServiceAgent a IBM.Sfp jsou zaregistorvany na HMC  
LparCMDRm ... dotazuje LPAR klienta na status  

##### Linux

ls /sys/devices/vio/ ... na linuxu ukaze oznaceni zarizeni  
ls /proc/device-tree/vdevice/ ... na linuxu ukaze oznaceni zarizeni  
lsslot -c slot ... ukaze sloty z i virtualnich zarizeni  
/etc/init.d/vpdupdater restart ...update virtualnich zarizeni na Linuxu  
drslot_chrp_slot -c slot -s U7998.60X.100E7DA-V3-C5 -r ... odebrani slotu  
drslot_chrp_slot -c slot -s U7998.60X.100E7DA-V3-C5 -a ... pridani slotu  
modprobe hvcs ... modul pro virtualni konzolu z HMC  
modprobe ibmveth ... modul pro sitovou kartu z VIOS  
modprobe ibmcscsic ... modul virtualni SCSI adapter z VIOS  
modprobe 8021q ... modul pro VLANy  
vconfig ... nastavovani virtualnich sitovych karet z VIOS  

## HMC - Hardware Manage Console

[HMC Scanner](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/HMC%20Scanner) ... java aplikace na pripojeni k HMC/IVM a stazeni informaci o managovanych systemech  
default uzivatel/heslo: hscroot/abc123
Defaultni IP adresy spravovanych systemu P5-192.168.2.147,192.168.3.147, P6-169.254.2.147,169.254.2.147

#### Virtualni terminaly ( "~.", "~~." - ukonceni terminalu)

mkvterm -m MSYST1 -p sinalfa2 ... mytvori novy terminal a prepne do nej
rmvterm -m MSTST1 --id 1 ... zrusi otevreny terminal
vtmenu ... interaktivni prepinani do jednotlivych konzoli. Opusti se bud: "~~.", nebo "~.ENTER"

#### informace o HMC a sprava HMC (defaultni nastaveni uzivatele: hscroot/abc123>

asmmenu ... Advanced System Management
cpsysplan ... kopirovani sysplanu  
chhmc -c xntp -s enable ... povoli NTP sluzbu  
chhmc -c xntp -s add myserver.ntp.com ... nastavi ntp server  
chsyspwd -M MSYST1 -t access --passwd --newpasswd noveheslo ... zmeni pristupove heslo k MSYST1  
chsvcevent -o closeall ... zavre na HMC vsechny udalosti  
chsvcevent -p 85 -h MOPB4HMC-21 -o close ... zavre udalos 85  
deploysysplan -f SYSTEM.sysplan -M SYSTEM ... Nacte sysplan ze soyboru a prekonfiguruje P-System SYSTEM  
hmcshutdown -t 0 -r ... okamzity reboot HMC
lshmc -v ... ukaze verzi HMC
lshmc -r ... ukaze aknualni "remote settings"
lshmc -n ... Vypis sitoveho a vzdaleneho nastaveni HMC
lshmcusr ... Lists the property (name, role and description) of HMC user(s).
lslparutil
lsled -r sa -t phys -m MSYST1 ... ukaze stave vystrazneho svetla
lsrefcode ... Reference Code History
lscod ... Capacity on Demand
lsdump
lslic ... ukaze firmware - Licensed Internal Code
lslic -M MSYST1 -t disk ... ukaze nainstalovany firmware a firmware, ktery je na disku k dispozici v adresari /opt/ccfw/data  
lslic -m 9133-55A-SN65D29DG-ICISTMP -t sys -r ftp -h 192.134.197.57 -u USERID --passwd PASSWORD -d /DIRECTORY ... ukaze aktualni FW, a jaky FW je k dispozici pres FTP  
lssvcevents ... ukaze udalosti spravovanych systemu  
lssvcevents -m USBSV3_B47-9117-MMA-10148DA -t hardware ... ukaze HW udalosti na manazovanem systemu  
lssvcevents -t hardware -d 30 --filter "status=Open" ... ukaze vsechny otevrene udalosti za poslednich 30 dni  
lssysconn -r all ... ukaze system resources connections - pripojene POWER servery vcetne parametu
lssysplan ... seznam sysplanu  
rnvi ... restricted-nvi - omezeny vi editor
bkprofdata -m MSYST1 -f /mnt/floppy/MyBackup .. zaloha profilu  
rstprofdata -m MSYST1 -f /var/hsc/profiles/SN/prof1 -l 1 ... kompletni obnaoveni profilu ze zalohy (l=2 backup priority, l=3 managed syst. priority)  
ls /var/hsc/profiles/SN/ ... seznam provilo na MSYST1 se seriovym cislem SN  
chlparutil, lslparutil, rmlparutil ... statistiky vyuzivani HMC  
chhmcusr, lshmcusr, rmhmcusr ... user management  
lshmcusr ... seznam hmc uzivatelu  
mkhmcusr -u aaa -a hmcsuperadmin --passwd ahoj -M 180 ... vytvori uzitavele aaa se spravcovskymi pravy, heslem ahoj platnym 180 dni  
chhmcusr -u hmcuser1 -t assign -o a -r resourcerole -v lpar_role ... prida doli zvanou lpar_role uzivateli hmcuser1  
chhmcusr -u user -t passwd ... zmeni uzivatelovo heslo  
chsyspwd ... zmena hesla  
chsacfg, lssacfg ... meni Service Agent - upozornovani IBM o udalostech  
chsacfg -t email -o enable ... povoli odesilani mailu v pripade problemu
chsacfg -t email -o setsmtp -h 10.155.54.28 -p 25 ... nastavi smtp server a port
chsacfg -t email -o add -a czfrux@cz.ibm.com --events all ... nastavi emailovou adresu
lssacfg -t email ... ukaze nastaveni odesilani emailu
chsacfg -t email -o test -a all ... posle testovaci zpravu
chled -r sa -t phys -m MSYST1 -o off ... vypne vystrazne svetylko  
mkauthkeys --remove 'joe@somehost' ... smaze joe@somehost z authorized_keys2  
mksysplan -m SYSTEM -f SYSTEM.sysplan ... udela sysplan (soubor s nastavenim) P-Systemu SYSTEM  
OS_install -o define_resource -a type=AIX -a version=1.5.1.0 -a location=/export/resources/vios15 -a source=/dev/cdrom vios_res_15 ... zkopiruje instalacky VIO serveru z CD na lokalni disk  
rmsysplan ... mazani sysplanu  
updhmc -t s -h 10.20.30.40 -u root -p passwd -f /update/HMC_update.zip ... provede update HMC ze vzdaleneho serveru  
updlic ... spravuje a upgraduje firmware na spravovanych systemech  
updlic -m MSYST1 -o k ... zkusi citelnost firmware na MSYST1  
updlic -m MSYST1 -o o ... Firmware muze spravavat jen OS  
updlic -M MSYST1 -o h ... Firmware muze spravovat jen HMC konzola  
updlic -M MSYST1 -o c ... soucasne (Currect) Firmware se zkopiruje z Temporary do Parnament  
updlic -M MSYST1 -o j ... Reject Firmware - zkopiruje Pernament to Temporary  
updlic -o a -m 9133-55A-SN65D29DG-ICISTMP -t sys -r disk -l latest -q ... zjisti, zda posledni upgrde muze byt concurent, ci distuptivni  
updlic -o a -m 9133-55A-SN65D29DG-ICISTMP -t sys -r mountpoint -d /home/hscroot/patch -l latestconcurrent ... Install and Accept aplikuje posledni concurent FW patch, a udela kopii predchoziho T do P  

#### Operace a power management spravovanych systemu a LPARu

chsysstate -m MSYST1 -r sys -o onstandby ... Prepne z "Power off" stavu na standby  
chsysstate -m MSYST1 -r sys -o onsysprof -f profil1 ... Prepne z "Power off" stavu na standby/activated - nacte ulozeny profil profil  
chsysstate -m MSYST1 -r sys -o on ... Prepne z "Power off" stavu na standby/activated - spusti vsechny LPARy, jez maji nastaveny autostart  
chsysstate -m MSYST1 -r sys -o off (--immed)... Pred uzitim, nesmi jet LPARy. Po uziti se (rychle) prepne system do "Power off"  
chsysstate -m MSYST1 -r sysprof -n xyz -o on ... zapne systemovy profil xyz  
chsysstate -m MSYST1 -r lpar -o shutdown -n pzadm02 (--immed) ... (okamzite) vypnuti LPARU = shutdown -hF
chsysstate -m MSYST1 -r lpar -o on -n pzadm02 -f Normal ... zapnuti LPARu s profilem Normal
chsysstate -m MSYST1 -r lpar -o shutdown -n frmpqdw00srb2xm --restart (--immed) ... reboot = shutdown -r(F)
chsysstate -m MSYST1 -r lpar -o dumprestart { -n Name | --id PartitionID } ... udela dump a pote restart LPARu  
lshwres -m MSYST1 -r mem --level syst ... podrobne informace o pameti v systemu MSTST1  
lshwres -m MSYST1 -r proc --level syst ... podrobne informace o procesorech  
lshwres -m MSYST1 -r io --rsubtype slot ... podrobne informace o vstupnich/vystipnich zarizenich  
lshwres -m HJ4P550B2 -r io --rsubtype slot -F lpar_name,phys_loc,drc_index,description --header ... ukaze IO zarizeni, potrebne informace  
lshwres -m MSYST1 -r virtualio --rsubtype scsi ... vypis virtualnich IO zarizeni  
lshwres -m MSYST1 -r virtualio --rsubtype eth --level sys ... vypis virtualnich sitovych adapteru  
lshwres -m MSYST1 -r virtualio --rsubtype eth --level lpar ... vypis virtualnich sitovych adapteru pro jednotlive lpary  
lssyscfg -r sys -F name,state --header ... ukaze prehled spravovanych POWER systemu a jejich stav
lssyscfg -m MSYST1 -r lpar -F name,state --header ... ukaze prehled spravovanych lparu a jejich stav
lssyscfg -m MSYST1 -r sys -F active_lpar_share_idle_procs_capagle ... ukaze vsechny LPARy na MSYST1 a zda mohou poskytovat nevyuzity vyhraneny procesor  

#### informace o LPARech

lscod -m MSYST1 -t hist ... historie LPARu
lssyscfg -r sys -F name,type_model,ipaddr,state --header ... ukaze prehled spravovanych POWER systemu, IP, a jejich stav
lssyscfg -m MSYST1 -r lpar ... ukaze prehled LPARU ve spravovanem systemu MSYST1  
lssyscfg -m MSYST1 -r lpar -F lpar_name,state ... ukaze stav lparu na MSYST1  
lssyscfg -m MSYST1 -r prof --filter lpar_names=lpar2 ... ukaze prehled profilu oddilu ve spravovanem systemu MSYST1  
lssyscfg -m MSYST1 -r prof -F name,lpar_name,io_slots ... ukaze seznam profilu a prirazene karty  
lssyscfg -r sysprof ... ukaze prehled systemovych profilu  
lssyscfg -m MSYST1 -r proc --filter "lpar_name=LEF7LPAR2-SINITC3" ... ukaze prirazeni procesoru danemu lparu
lspartition -dlpar ... seznam LPARu, ktere podporuji DLPAR (dynamic lpar), ukaze status LPARu, ktere hlasi RMC (jestli je navazano spojeni)
lshwres -m MSYST1 -r proc -sys lpar ... nastaveni procesoru pro lpary  
lshwres -m MSYST1 -r proc --level lpar -F lpar_name,run_procs --header ... ukaze aktualni pocet virtualnich procesoru pro lpary  
lshwres -m MSYST1 -r proc --level lpar -F lpar_name,curr_proc_units ... ukaze aktualni pocet vyuzivanych procesoru pro lpary  
lshwres -m MSYST1 -r mem --level plar -F lpar_name,run_mem ... Aktualni pocet prirazene pameti  

#### Meneni, vytvareni a mazani LPARu

chhwres -m MSYST -r proc -id 1 -r prof -i "pend_sharing_mode=keep_idle_procs|share_idle_proc|share_idle_procs|share_idle_procs_always" ... nastavi sdileni procesoru  
chsyscfg ... meni lpary, profil lparu, ci systemove profily  
chsyscfg -r {lpar | prof | sys | sysprof | frame} {-m managed-system | -e managed-frame} {-f configuration-file | -i "configuration-data"} ... zmeni parametry "configuration-data" nebo configuration-file na managed-system, ci managed-frame u lparu, profilu, systemovem profilu, atd.  
chsyscfg -m MSYST1 -r sys -i "new_name=sys1,power_off_policy=1" ... Zmeni power-off politiku na zpravovanem systemu 9406-570*89320051  
chsyscfg -m MSTST1 -r prof -i "name=Normal,lpar_name=LEF6LPAR5,proc_mode=shared,min_proc_units=1.0,desired_proc_units=2.0,max_proc_units=4.0,min_procs=1,desired_procs=2,max_procs=4,sharing_mode=cap,uncap_weight=0"
chsyscfg -m MSTST1 -r prof -i "name=Normal,lpar_name=LEF6LPAR5,min_mem=4096,desired_mem=8192,max_mem=12288" ... zmeni profil normal u lparu LEF6LPAR5
chsyscfg -r prof -m HJ4P550B2 -i "name=normal,lpar_name=HJ4MESB201,io_slots+=2103000B/none/1" ... prida slot 2103000B do provilu  
mksyscfg ... vytvari nove lpary, profil lparu, ci systemove profily  
mksyscfg -m MSYST -r {lpar | prof | sysprof} -i "parametry" -f file ... vytvori lpar,profil,systemovy profil na serveru SERVER s paramery "paramery" nebo ze souboru file  
mksyscfg -m MSYST -r sysprof -i "name=sysprof1,"lpar_names=lpar1,lpar2","profile_names=prof1,prof1"" ... vytvori systemovy profil  
mksyscfg -m MSYST -r lpar -i profile_name=prof1,lpar_env=aixlinux,min_mem=1024,desired_mem=2048,max_mem=4096,name=part1 ... vytvori lpar  
mksyscfg -m MSYST -r lpar -i "profile_name=prof1,lpar_env=aixlinux,min_mem=1024,desired_mem=2048,max_mem=4096,name=part1,proc_mode=ded,min_procs=1,desired_procs=1,max_procs=2,sharing_mode=keep_idle_procs" ... vytvori lpar  
mksyscfg -m MSYST -r lpar -f [/tmp/profiles.txt](profiles.txt) ... vytvori lpar, data nacte ze souboru  
rmsyscfg ... maze lpary, profil lparu, ci systemove profily  
rmsyscfg -m MSYST -r {lpar | prof | sysprof} -n name ... smaze lpar,profil, systemovy profil na MSYST1 jmenem name  
rmsyscfg -m MSYST -r lpar --id 5 ... smaze lpar cislo 5  
rsthwres -r io -m HJ4P550B2 -p HJ4MESB201 ... znovu nacte informace or HW  

#### Informace o HW na spravovanych systemech a jejich dynamicka zmena zmena ([DLPAR](http://www.ibm.com/developerworks/systems/articles/DLPARchecklist.html))

chhwres -m MSYS1 -r mem -o a --id 1 -q 128 -w 10 ... Prida 128MB pameti LPARu 1, zkousi to 10 min  
chhwres -m MSYS1 -r mem -o r -p aix_p1 -q 512 -d 5 ... odebere 512 MB pameti z lparu aix_p1 a vystup bude v detailu 5  
chhwres -m MSYS1 -r proc -o a -p lpar1 -q 1 ... prida jeden procesor lparu lpar1  
chhwres -m MSYS1 -r proc -o m -p p1 -t p2 --procs 1 -w 0 ... presune 1 procesor z p1 do p2, zkousi to dokud neuspeje  
chhwres -m MSYS1 -r proc -o m --id 1 --tid 2 --procunits .5 ... prevede z lparu 1 na lpar 2 0.5 procesoru  
chhwres -m MSYS1 -r proc -o s -p lpar1  -a "sharing_mode=share_idle_procs_active" ... dynamicky zmeni sdileni procesoru  
chhwres -m MSYS1 -r io --rsubtype slot -o a -p LPAR1 -l 21030003 -w 0 ... prida lparu LPAR1 i/o zarizeni s DRCindexem 21030003  
chhwres -m MSYST1 -r hea -o a -p LPAR1 -l 23000020 -physport 0 -g2 --logport 4 ... prida logicky port 4 pro fyzicky port 0 patrici skupine 2  HEA adapteru ID 23000020 lparu LPAR  
chhwres -m MSYST1 -r procpool -o s--poolid1 -a "new_name=Production,max_pool_proc_units=3,reserved_pool_proc_units=0.5" ... vytvori Shared-Processor Pool - skupinu sdilenych procesoru  
chhwred -m MSYST1 -r procpool -o s -p LPAR1 -a "shared_proc_pool_name=Production" ... prirazeni (klidne i presuniti z jine) LPAR1 do procesorove skupiny Production  
chhwred -m MSYST1 -r procpool -o s -p LPAR1 -a "shared_proc_pool_name=DefaultPool" ... vyrazeni LPAR1 z procesorove skupiny, kde byl  
chhwred -m MSYST1 -r procpool -o s --poolid 1 -a "new_name=Production,max_pool_proc_units=0,reserved_pool_proc_units=0" .. zruseni procesorove skupiny  
lshwres -m MSYST1 -r io --rsubtype {unit | bus | slot | iopool | taggedio} ... ukaze fyzicky hardware na spravovanem systemu managed-system  
lshwres -m MSYST1 -r io --rsubtype slot -F description,unit_phys_loc,bus_id,phys_loc,drc_name,lpar_id,drc_index --header ... ukaze hardwarove resources - sloty
lshwres -m MSYST1 -r virtualio --rsubtype {eth | hsl | virtualopti | scsi | serial | slot} ... ukaze virtualni zarizeni na spravovanem systemu  
lshwres -m MSYST1 -r mem --level {lpar | sys} ... ukaze statistiku pameti na systemu, ci lparu  
lshwres -m MSYST1 -r proc --level {lpar | pool | sys} ... ukaze nastaveni procesoru  
lshwres -m MSYST1 -r hca --level {lpar | sys} ... ukaze HCA (Host Channel Adapter)  
lshwres -m MSYST1 -r sni ... ukaze SNI (Switch Network Interface)  
lshwres -m MSYST1 -r procpool ... informace o procesorovych skupinach  
rsthwres ... vrati hw resources po dinamickych zmenach do puvodniho stavu  
rsthwres -r {io | mem | proc} -m managed-system [{-p partition-name | --id partition-ID}]  
chedo -a | grep xpm_xvcpus ... zjisti, zda je zzapnuty VP (Virtual Processor) folding, 0 zapnuto, -1 vypnuto  
schedo -o vpm_xvcpus=-1 ... vypne VP folding  

DLPAR funguje, kdyz je spojeni HMC-Hypervisor, HMC-LPAR a komunikuje RMC)

#### Virtualni a fyzicke zarizeni pro LPARy

chsyscfg -m sys1 -r prof -i 'name=server_name,lpar_id=1,"virtual_eth_adapters=596/1/596*0/1,506/1/506*0/1,"' ... prida virtualni sitovy adapter
596/1/596//0/1, coz rika slot_number=596, vyhovuji ieee, port_vlan_id=1, nema prirazene zadne VLAN id, neni trunk adapter, je "required".  
Syntaxe pro Virtual ethernet adapter : slot_number/is_ieee/port_vlan_id/"additional_vlan_id,additional_vlan_id"/is_trunk(number=priority)/is_required  

chsyscfg -m sys1 -r prof -i 'name=server_name,lpar_id=1,"virtual_scsi_adapters=301/client/4/vio01_server/301/0,303/client/4/vio02/303/0"' ... vytvori 2 scsi sloty 301,303 typu klinet, nejsou required  

Syntaxe pro Virtual scsi adapter: virtual-slot-number/client-or-server/supports-HMC/remote-lpar-ID/remote-lpar-name/remote-slot-number/is-required  
lshwres -r virtualio --rsubtype scsi -m sys1 ... seznam scsi virtualnich zarizeni v sys1  

## VIO server - Virtual I/O server

[VIOS advisor](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/VIOS%20Advisor) ... VIOS Performance advisor (prikaz part)  

lsdev, mkdev, rmdev, entstat, atd. jsou pouzitelne z padmina stejne jako z roota na aixu, jsou vsak jinaci parametry (-l = -dev, -a = -attr, atd.). Na VIOS lze prepnout do roota jen pro instalaci "third-party SW", jinak lze ztratit support  

installios ... spusti instalaci VIOS z HMC, nelze z IVM manazovanych systemu  

oem_setup_env ... pod padmin prepne na root uzivatele
cfgassist ... konfiguracni agent jako smitty - nastavuje pod padminem cas, hesla, bezpecnost, TPC/IP, update  
chdev -dev en3 -attr netaddr=10.0.0.5 netmask=266.0.0.0 state=up ... nastavi dalsi sitovou kartu a adresu  
chdev -dev vscsi0 -attr vscsi_path_to=30 -perm ... nastavi parametry vscsi0
chtcpip ... meni tcpip nastaveni sitovych karet  
chpath -dev hdisk1 -pdev scsi0 -attr priority=2 ... zmeni prioritu pouzivani cesty k hdisk1  
ioslevel ... ukaze verzi VIO  
licence --accept ... prijme licenci  
lsnetsvc ssh ... informace, zda sshd demon je spusteny  
lstcpip ... jako netstat -in, vylistuje nastaveni sitovych karet  
mirrorios -f hdisk2 ... kdyz jsou ve VG 2 PV, pak mirroruje rootvg VIO serveru na hdisk2  
mktcpip -hostname VIO1 -inetaddr 1.2.3.4 -start -netmask 255.0.0.0 -gateway 1.2.3.1 ... nastavi sitovou konfiguraci  
help ... seznam vsech prikazu v padminovi  
startnetsvc ... spusti sitovou sluzbu, napr ssh, ldap, telnet  
stopnetsvc ... zastavi sitovou sluzbu, napr ssh, ldap, telnet  
viosecure ... meneni bezpecnosti VIO serveru  
viostat ... ukaze statistiky vytizeni CPU a I/O operaci na disky  
Pro spravu lze vyuzit WebSM menu (properties -> virtual IO Adapter ...)

#### Infoformace o zarizenich

lsdev -slots ... (padmin) seznam virtualnic slotu (konvence <20 pro sitove karty, >20 pro harddisky)
lsdev -virtual ... ukaze vsechny virtualni zarizeni - LPARu  
lsdev -vpd ... ukaze informace o platvorme - procesory, sbernice, disky - neco jako prtconf  
lsdev -dev vhost2 ... vylistuje konkretni zarizeni - sbernici vhost2  
lsdev -dev hdisk2 -vpd ... vylistuje konkretni zarizeni - hdisk2, vcetne informaci o adrese atd (vitalni informace)  
lsdev -type adapter|grep en ... seznam sitovych karet
lsdev -slots ... ukaze virtualni sloty LPARu (vhost)  
lsmap ... vypis zavislosti mapovani mezi virtualnimi a fyzickymi zarizenimi  
lsmap -vadapter vhost0 ... vypis virtualniho adapteru a vsech jeho zarizeni (vSCSI servru), znaceni: typ.model.S/N.cislo_lparu.slot
lsmap -all | grep vhost ... vypise virtualni masiny
lsmap -all | grep -p hdisk30 ... uukaze virtualni disk k disku hdisk30
lsmap -all -net ... ukaze definovane virtualni VLANy  
lsrep ... vypis repozitare "storage volume group"
lsvopt ... seznam virtualnich CD/DVD mechanik  
lsslot -c slot | grep -i hea ... ukaze vsechny integrovane HEA (IVE) sitove karty  
lshwres -m MSYST1 -r hea --rsubtype phys --level sys ... ukaze vyzicke HEA adaprety  
lshwres -m MSYST1 -r hea --rsubtype logical --level sys ... ukaze logicke HEA adaptery  
lshwres -m MSYST1 -r hea --rsubtype logical --level port --filter "lpar_name=LPAR" ... ukaze prirazene logicke HEA porty prirazene lparu LPAR  
lshwres -m MSYST1 -r io --rsubtype slot ... ukaze I/O sloty  
oem_setup_env; fget_config -Av ... ukaze ktery disk je z ktere storage (darX)

#### Upgrade vios pack

updateios -dev /mnt/lpp_source/vios14_fixpack92_lpp -install -accept
reboot
ioslevel ... Napise verzi VIO

#### VIOs backup/restore

backupios -file /mnt ... vytvori tar soubor obsahujici mksysb a jine
backupios -file /mnt/VIOS1_newP5_B2_220308.mksysb -mksysb ... vytvori jen mksysb soubor

#### Vytvoreni virtualnich zarizeni pro logicke oddily - SEA

mkvdev -sea ent0 -vadapter ent10 -default ent10 -defaultid 101 -attr ha_mode=auto ... vytvori z fyzicke sitove karty ent0 virtualni sitovou kartu ent10, PVID=101 (vlan).
mkvdev -sea ent0 -vadapter ent1 ent2 -default ent1 defaultid 2 ... vytvori SEA (Shared Ethernet Adapter) ze sitove karty ent0, virtualni karty ent1, ent2 (muze jich byt az 16)  
mkdev -lnagg ent0 ent1 ... vytvori EtherCannel - (link aggregation) ze sitovych adapteru ent0 a ent1  

#### Vytvoreni virtualnich zarizeni pro logicke oddily - VSCSI - CD/DVD

mksp -f STORAGEpool1 hdisk1 ... (make storage pool) vytvori "storage volume groupu" STORAGEpool1 z hdisk1  
mkrep -sp STORAGEpool1 -size=10G ... (make media repository) vytvori 10G oddil "storage logical volume"  
mkvopt -name aaa -size 4G ... (make virtual optical disk) vytvori 4G medium pro CD/DVD v repozitari  
mkvdev -fbo -vadapter vhost0 ... (make virtual device) vytvori fbo (file backed optical) CD/DVD pouzivajici virtualni adapter vhost0  
loadopt -disk clientData -vtd vopt1 ... nacte disk clientData od virtualni CD/DVD mechaniky vopt1, nachazi se v /var/opt/STORAGEpool1/  

#### Vytvoreni virtualnich zarizeni pro logicke oddily - VSCSI - disk z fyzickych disku

mkvdev vdev hdisk1 vadapter vhost1 ... vytvori virtualni (bootovatelny) disk pro vhost1 z hdisk1  
mkvdev vdev hdisk2 vadapter vhost0 dev client_disk1 ... vytvori virtualni disk s nazvem client_disk1  

#### Vytvoreni virtualnich zarizeni pro logicke oddily - VSCSI - disk z LV

mkvg -f -vg vioserver1VG hdisk1 hdisk5 ... vytvori VG vioserver1VG (konvence: VIOS_nameVG) z hdisk1 a hdisk5
extendvg vioservr1VG hdisk2 hdisk 6 ... rozsiri VG o hdisk2 a hdisk6
mklv -lv LPAR1hd1LV vioserver1VG 30G hdisk0 ... vytvori LV LPAR1hd1LV v VG vioserver1VG na hdisk0 (konvence:LPAR_nameHD_nameLV)
mkvdev -vdev LPAR1hd1LV vadapter vhost0 [-dev vtLPAR1hd1]... vytvori virtualni disk z LV LPAR1hd1LV [nazev zarizeni vtLPAR1hd1]  

#### Vytvoreni virtualnich zarizeni pro logicke oddily - VSCSI - disk ze souboru

mksp -f lparpool hdisk2 ... vytvori Storage pool "lparpool"  
mksp -fb fbpool -sp lparpool -size 6G ... vytvori fb (file-backing) souborovy storage pool  
mkbdsp -sp fbpool 2G -bd File2 -vhost4 [-tn vtscsi1]... Vytvori soubor File2 v souboruvem storage poolu fbpool pro adapter vhost4 [se jmenem zarizeni vtscsi1]  

#### Mazani virtualnich zarizeni

rmvdev -vtd vtscsi1 ... smaze virtualni scsi zarizeni vtscsi1 (musi se predtim oddelat se systemu pomoci rmdev)  
rmdev -dev vhost0 ... zrusi definici virtualniho SCSI adapteru host0  
rmdev -dev vhost0 -recursive ... smaze vhost0 vcetne vsech dcerinych zarizeni  

#### nastavovani parametru na klientovi (na LPARu)

chdev -dev fscsi0 -attr fc_err_recov=fast_fail dyntrk=yes -perm ... nastavi pernamentni zmenu (po vypnuti/zapnuti lparu) pro dynamic_tracking (paralelni zapisovani na disk) a fast_failover
chpath -l hdisk4 -p vscsi5 -a priority=2 ... na klientovi se nastavi priorita, s jakou se budou sdilet disky mezi vio servery
chdev -l hdisk5 -a hcheck_interval=20 -P ... nastavi interval zdravotnich kontrol
lasttr -El hdisk5 | grep hcheck_interval ... kontrola, zda je nastaven Health Check interval = 20
lasttr -El ent0 | grep media_speed ... kontrola, zda je nastavena rychlost na 1000_Full_Duplex
lsattr -El fscsi5|grep fc_err_recov ... kontrola, zda je nastaveno fast_fail
lsattr -El fscsi5|grep dyntrk ... kontrola, zda je nastaveno Dynamic Tracking FC Devices yes
lspath -AHE =l hdiskx -p vscsi5 ... Ukaze prioritu

#### Konvence

Nazev node (LPAR) nazevSERVERU_budova_serioveCISLO, napriklad Vio1_b2_db4ef
slot <20 ... eth karta
slot >20 ... hdisk, sudy na vio1, lichy na vio2, prvni hdisk, potom swap
vioServerVG ... nazev VG
[partitionName][hdX]LV ... nazev LV (saxsap15phd0LV)

#### VIO disky pro HACMP

Na VIO serverech:
chdev -dev hdisk1 -attr reserve_policy=no_reserve ... disk nebude v reserved modu (pouziti Enhanced Concurent Mode)
Na klientech:
chdev -l hidsk1 -a hcheck_interval=20 -a hcheck_mode=nonactive -P ... nastaveni parametru

#### Disky pri 2 VIOS, nebo pri 2 cestach

chdev -dev fscsi0 -attr fc_err_recov=fast_fail dytrynk=yes -perm
chdev -dev hdisk1 -attr reserver_policy=no_reserve

#### SEA a etherchannel cahnnel

mkdev -sea -ent0 -vadapter ent2 -defult ent2 -defaultid 1 -attr ha_mode=auto ctl_chan=ent3 netaddr=9.3.4.1 largesend=1 ... Nadefinuje SEA s failover, komunikacni kanal pres ent3  
chdev -dev ent4 -attr ha_mode=auto ctl_chan=ent3 ... nakonfiguruje jiz nakofigurovanou SEA na failover mod s kontrolnim kanalem pres ent3 pro virtualni kartu ent4  
chdev -dev ent4 -attr ha_mode=standby ... manualni failover  

#### [IVM](http://publib.boulder.ibm.com/infocenter/powersys/v3r1m5/topic/iphch/abstract_ivm.htm) ... Integrated Virtualization Manager

produkt - balik nastroju na ovladani Systemu umisteneho na Virtual I/O Serveru

mksysplan -f Server.sysplan -m Server-9117-MMA-SN123456 ... Vytvori [sysplan](http://publib.boulder.ibm.com/infocenter/powersys/v3r1m5/index.jsp?topic=/iphch/iphchkickoff.htm) - informace o Power spravovaneho systemu  

#### SEA s VLANy

mkvdev -sea ent0 -vadapter ent1 -default ent1 defaultid 199 ... vytvori dalsi virtualni sitovy adapter. Neoznacene pakety budou na VLANu 199  
mkvdev -vlan ent2 tagid 10 ... vytvori dalsi virtualni sitovy adapter na vlanu 10
