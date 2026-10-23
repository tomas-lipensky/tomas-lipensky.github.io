## Windows

### Externi odkazy

[Codeplex](https://www.codeplex.com/) - opensource projekty na Microsoft produkty  

### Interni odkazy

[CMD a .bat soubory](bat)  
[Powershell](powershell)  
[registry](win-registry), WER dumpy, ..  
[Defender](win-defender), inTune, ..  
[Powershell](ps)  
[Debugging](win-debug) aneb hledani chyb  

### Verze

Verze se stenym jadrem

XP a 2003  
7 a 2008  
8 a 1012  
10 a 2016 (2016 ma negrafickou variantu instalace - [Server Core](https://docs.microsoft.com/en-us/windows-server/administration/server-core/what-is-server-core))  

### Administracni nastroje

RSAT - Remote Server Administration Tools ... Sada nastroju na vzdalenou konfiguraci MS sluzem (AD, ...)  
Invoke-Expression (New-Object Net.WebClient).DownloadString(‘http://bit.ly/Win10RSATinstall2’) ... nainstaluje RSAT  
Windows Admin Center ... Web UI na spravu vzdalenych Windows systemu (konzole, vzdalena plocha, nastaveni)  
[WSL](https://www.linux.com/blog/learn/2018/2/how-get-started-using-wsl-windows-10) - Windows Subsytem for Linux ... virtualni Linux prostredi ve Windows  
[Sysinternals](https://docs.microsoft.com/en-us/sysinternals/downloads/) - doplnujici nastroje na administraci Windows, i CLI utility  
[Dependency walker](http://www.dependencywalker.com/) - ukase zavislosti knihoven  
### Konfiguracni soubory

C:\WINDOWS\system32\drivers\etc\hosts ... nastaveni lokalniho prekladu jmen (jako DNS)

### Promenne

echo %username% ... jmeno uzivatele  
### Debugging nastroje

[Image File Execution Options](https://gooroo.io/GoorooTHINK/Article/17352/Image-File-Execution-Options-Good-Evil-Fun/28441#.W-wCDfZFyUl) ... volba registru pro spousteni debuggeru pri spousteni konkretniho spustitelneho souboru, detaily viz [stranka Windows registru](win-registry)  

#### Spravce balicku

WinGet ... pouze pro pracovni stanice  
chocolatey list --local ... seznam nainstalovanych  
choco install azure-pipelines-agent ... instalace  
choco upgrade azure-pipelines-agent ... upgrade  
choco uninstall azure-pipelines-agent ... odinstalace  

### Pripojeni, sezeni (session), vzdalene spousteni

mstsc ... remote desktop - vzdalena plocha  
mstsc /v:10.1.0.4 ... pripojeni ke vzdalenemu pocitaci 10.1.0.4  
quser ... ukaze aktualne pripojene uzivatele  
logoff ... odpojeni aktualniho sezeni (vypne spustene programy)  
net session ... ukaze jaci uzivatele jsou pripojeni  
qwinsta ... (Query WINdows STAtion) ukaze vsechna soucasna pripojeni  
rwinsta ... (Reset WINdows STAtion) prerusi aktualni ci cizi spojeni  

##### Pripojeni k prikazove radce z Linuxu

[winexe](http://rpm.pbone.net/index.php3/stat/4/idpl/21768497/dir/redhat_el_6/com/winexe-1.00-2.2.x86_64.rpm.html) -U DOMAIN/USERNAME%PASSWORD //MACHINEIP "cmd.exe"  
echo -ne '\n' | winexe -U DOMAIN/USERNAME%PASSWORD //MACHINEIP "powershell echo ahoj"  
Lze pouzit i pro [kopirovani](http://blog.jazzpod.co.uk/winexe-the-linux-psexec/)  

### Prikazy - binarky (ne cmd, ps) v \windows\System32

[rádkové príkazy Windows](http://www.samuraj-cz.com/clanek/radkove-prikazy-windows/)  
attrib *.* -s -h /s /d ... zrusi prepinac souboru system (-s) a hidden (-h) pro vsechny soubory a adresare (/d) v adresari a podadresarich (/s)  
certutil -p HESLO -importPFX certifikat.pfx ... import PFX certifikatu do klicenky LocalMachine\My  
cscript ... interaktivni textove managovani windows  
[diskshadow -s aaa.cmd](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/diskshadow) … vytvori novy disk z existujiciho adresare  
fsutil hardlink create new-file existing-file … vytvori hard link  
[handle](https://docs.microsoft.com/en-us/sysinternals/downloads/handle) … ukaze ktere procesy maji otevrene (zamcene) ktere soubory  
manage-bde.exe -protectors  -add c: -TPMAndPIN 123456 … prida dodatecny PIN pro BitLocker enkrypci disku  
manage-bde -status … status enkrypce, detaily  
manage-bde -changepin c: … zmena pinu  
manage-bde -protectors -add c: -TPM … zapne pouze TPM  
mklink c:\path\to\symlink c:\target\file … vytvori symbolicky link na soubor  
mklink /d c:\path\to\symlink c:\target\file  … vytvori symbolicky link na adresar  
msconfig ... konfigurace programu, ktere se spouzti pri startu windows  
msinfo32 ... info o windows  
net helpmsg 2 ... informace o exit kodu 2 ($LASTEXITCODE)  
net time \\dc.domain.local /set /y … synchronizace casu s NTP serverem  
net session ... ukaze jaci uzivatele jsou pripojeni  
net statistics workstation ... informace o behu systemu (uptime, pocet session, sitovych dat..)  
net stop scheduler ... spusti sluzby scheduler  
net user Guest ... ukaze informace o uzivateli (kdy se naposledy pripojil, informace o heslu atd)  
NET USER JMENO HESLO /ADD ... pridani uzivatele  
NET USER JMENO ... vypise info  o uzivateli  
NET USER JMENO HESLO ... zmeni heslo uzivatele  
netsh interface ip show config ... ukaze IP konfiguraci  
netsh interface ip set address "Local Area  Connection" static 192.168.0.10 255.255.255.0 192.168.0.254 ... nastaveni IP adresy  
netsh interface ip set address "Local Area Connection" dhcp ... nastavi automaticke DHCP  
netsh interface ip set dns name="Wireless Network Connection" source=static addr=192.168.1.200 register=PRIMARY ... nastaveni primarni DNS  
netsh interface ip add dns name="Wireless Network Connection" addr=192.168.1.5 index=2 ... nastaveni sekundarni DNS  
netsh interface dump > mycfg.dat ... provexe extrakt sitove konfigurace do souboru  
netsh interface dump > mycfg.cmd ... dump - prikazy  
netsh exec mycfg.dat ... obnovi sitovou konfiguraci ze zalohy dump  
netsh firewall set portopening tcp 445 smb enable ... povoli prot 445 na firewallu  
netsh advfirewall firewall delete name rule name=all protocol=tcp localport=21 ... smaze pravidlo  
netsh firewall set opmode disable ... vypne firewall  
netsh firewall set opmode enable ... zapne firewall  
netsh wlan show settings ... ukaze konfiguraci wifi  
netsh wlan connect ssid=”mySSID” name=”WLAN-Profil1” ... pripoji se k wifi  
netsh interface portproxy add v4tov4 listenport=8102 listenaddress=9.228.18.55 connectport=8102 connectaddress=15.1.22.143 ... port forwarding lokalniho portu 9.228.18.55:8102 na 15.1.22.143:8102  
netsh advfirewall firewall dump ... ukaze nastaveni rozsireneho firewallu  
openfiles ... ukaze otevrene soubory  
gpresult /v ... seznam politik (policies GPO)  
sc queryex type= service state= all ... seznam vsech sluzeb (z CMD ne PWSHELL)  
sc qc "IBMWAS70Service - X3_01_I" ... vypise podrobnosti o sluzbe  
SC CONFIG "IBMWAS70Service - X3_03_I" binPath= "D:\WebSphere\AppServer\bin\wasservice.exe X3_03_I" ... zmeni prikaz pro praci se sluzbou  
sc config "IBM Cognos:9301" start= disable ... vypne autostart (disable, auto, demand)  
sc stop schedule ... vypne task scheduler (stop, start)
[schtasks](http://www.howtogeek.com/51236/how-to-create-modify-and-delete-scheduled-tasks-from-the-command-line/) /query ... scheduler - ukaze naschedulovane ukoly  
schtasks /create /ru "System" /tn MujTask /tr "powershell -noninteractive Get-Date > C:\cas.txt" /sc once /ST 23:59 /F /V1 /Z … naplanuje job na pulnoc  
& schtasks /run /tn MujTask … spusti naplanovany job okamzite  
secpol.msc ... security policy  
services.msc ... Sprava sluzeb  
start a.html ... spusti soubor vychozi aplikaci  
systeminfo ... informace o hardware, OS a jak dlouho jede (uptime)  
taskill /F /PID 1234 ... ukonci nasilne process s PID 1234  
tasklist /v | find "SERVICE" ... detailni vypis procesu, vybere jen radky obsahujici slovo SERVICE  
taskmgr ... seznam procesu, ptere bezi, mozno vyvolat shift-ctrl-esc  
typeperf "\\Server1\Processor(_Total)\% Processor Time" … ukase vyuziti procesory v textovem rezimu  
WMIC /OUTPUT:C:\ProcessList.txt path win32_process get Caption,Processid,Commandline ... seznam procesu vcetne vsech argumentu presmerovany do souboru  
wmic bios get serialnumber ... seriove cislo pocitace (WMI Console)  
wmic cpu list  
wmic class win32_Processor get  
wmic product get name ... seznam nainstalovanych programu  
wmic product where name="sad das" call uninstall ... odinstalace programu  
wmic logicaldisk get caption,description,drivetype,providername,volumename ... seznam logickych disku  
wmic diskdrive list brief /format:list ... seznam fyzickych disku  
wmic os get lastbootuptime ... uptime  
wmic process where "name like '%chrome%'" get processid,parentprocessid,commandline ... vypis celeho prikazu u spusteneho procesu chrome, PID a rodicovskeho ID  
winrm qc ... (qc nebo quickconfig) - povoleni Windows Remoting  
[Winrm get winrm/config](https://blogs.technet.microsoft.com/askperf/2010/09/24/an-introduction-to-winrm-basics/) ... Ukaze konfiguraci Windows Remote Management  
Winrm enumerate winrm/config/listener ... ukaze pocet listeneru na WinRM  
[winrs -r:http://vzdaleny_server "cmd"](https://blog.thesysadmins.co.uk/winrm-winrs-and-forwarded-event-logs.html) ... remote shell - vzdalene spusteni shellu ([WinRM traces - logy](https://blogs.msdn.microsoft.com/wmi/2010/03/16/collecting-winrm-traces/))  
xcopy /h *.* C:\temp ... presune vsechny soubory vcetne skrytych (/h) do C:\temp  

### Vykon, performance

perfmon ... performance monitor - jako nmon na Unixu - umi ukladat statistiky vykonu  
[perfview](https://github.com/microsoft/perfview) ... ziskani informaci o pameti, pameti a procesech, prohlizeni trid a vykonostni analyza ([tutorial](https://channel9.msdn.com/Series/PerfView-Tutorial)  

### ostatni prikazy

DEVCON FIND =NET ... najde sitove adaptery  
DEVCON disable @ROOT\NET\0000 ... zakaze prvni sitovy adapter  
DEVCON enable @ROOT\NET\0000 ... povoli prvni sitovy adapter  
fixmbr ... opravi boot sektor (nahraje bootovaci manazer windows) - lze z opravneho media  
winmsd /report c:\temp\collect-winmsd.txt ... info o windows  

### Graficke programy - soucasti Windows

mmc.exe ... Microsoft Management Console - manazovani certifikatu, firewall, sluzby a jinych administratorskych ukolu na tento i okolni pocitace  

### Utility pro praci s WMI, registry atd.

WMI - Windows Management Instrumentation - infrastruktura na managoivani Windows.

[WMI Explorer](https://wmie.codeplex.com/) - pruzkumnik WMI objektu  
[Scriptomatic](https://technet.microsoft.com/en-us/scriptcenter/dd939957.aspx) - nastron na generovani WMI skriptu  

### Deployment Image Service and Management Tool (DISM)

Nastroj na provadeni servisnich operaci na Windows, nebo offline obrazu v WIM formatu  

Dism /online /Get-Drivers ... seznam ovladacu v bezicim systemu  
Dism /online /Get-DriverInfo /driver:oem9.inf ... info o ovladaci  
Dism /online /Get-Packages ... seznam balicku  
Dism /online /Get-Features ... seznam Features  
Dism /online /Get-Intl ... seznam nainstalovanych jazyku  

### Cisteni Windows

Dism.exe /Online /Cleanup-Image /AnalyzeComponentStore ... analyza obsahu C:\Windows\WinSxS adresare  
schtasks.exe /Run /TN "\Microsoft\Windows\Servicing\StartComponentCleanup" ... spusteni ukolu na cisteni C:\Windows\WinSxS adresare - smazani predchozich verzi komponent po 30 dnech  
Dism.exe /online /Cleanup-Image /StartComponentCleanup ... smazani predchozich verzi komponent (bez cekani 30 dnu)  
Dism.exe /online /Cleanup-Image /StartComponentCleanup /ResetBase ... smazani vsech predchozich verzi vsech komponent - nelze vratit komponenty do predchozich verzi  
Dism.exe /online /Cleanup-Image /SPSuperseded ... smazani zaloh pred aplikaci service packu  
[https://www.ghacks.net/2017/11/16/how-to-delete-downloaded-windows-update-files/](https://www.ghacks.net/2017/11/16/how-to-delete-downloaded-windows-update-files/) ... Cisteni C:\Windows\SoftwareDistribution adresare  

### Utility pro práci se soubory a disky

[Servant Salamander](http://www.altap.cz) -
Souborový manažér ve stylu NC, VC, Windows Comander...  
[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) - SSH klient (šifrovaný telnet)  
[Pagent](http://www.chiark.greenend.org.uk/~sgtatham/putty/) - nacteni klicu pro automatickou autentifikaci klicem  
[FTP Commander](http://www.internet-soft.com/ftpcomm.htm) - Ftp klient ve stylu Norton Commandera  
[WinSCP](http://winscp.sourceforge.net/eng/) - Další Ftp program ve stylu Nortona, avšak tentokrát komunikuje pres SSH  
[7-zip](http://www.7-zip.org/) - komprimační manažér, umí pracovat s archívy 7z, bz2, gz, Tar, Zip, Arj, Cab, Rar, Tar, Rpm, Deb...  
[AlZip](http://www.altools.net/) - komprimační manažér - kromě spousty formátů podporuje Drag &amp; Drop  
[Deepburner](http://www.deepburner.com/) - program pro vypalování CD/DVD. Vypaluje data, hudbu a obrazy (image) jiných CD a DVD. Uživatelsky přátelský.  
[Truecrypt](http://www.truecrypt.org/) - zakryptovane datove kontejnery/disky  
[FreeOTFE](http://www.freeotfe.org/) - zakryptovane datove kontejnery/disky  
guacamole - freeware web server na vzdalenou plochu  
notepad++ ... vylepseny notepad  
Visual Studio Code ... Textovy editor (IDE) ve stylu Sublime, Linux verze k dispozici  
http://www.engelteddy.com/image-synchronizer/ ... synchronizace adresare s ftp serverem  

### Programy pro práci s multimédii a internetem

[Firefox](http://www.czilla.cz/) - rychlý a propracovaný internetový prohlížeč s možností rozšíření  
[Thunderbird](http://www.czilla.cz/) - vynikající poštovní klient s možností rozšíření  
[XnView](http://perso.wanadoo.fr/pierre.g/) - prohlížeč a konvertor obrázků. Podporuje spoustu formátů, nestandartně rychlý, velice přispůsobivý, podpora slideshow.  
[WINAmp](http://www.winamp.com/) - přehrávač zvukových médií, který nabízí podporu mnoho zvukových soborů, skinovatelný  
[GIMP](http://www.gimp.org/) - Výborný graficky program ve stylu Photoshop...  
[TightVNC](http://tightvnc.com/download.php) - sdileni obrazovky po siti  
xming ... program umoznujici zobrazovani X11 paketu z ssh (putty)  
[RawCap](http://www.netresec.com/?page=RawCap) ... sniffer, umi i 127.0.0.1  

### Konfigurace

Logon/Logoff scripts - definovane v policies - Grpup Policy Mangement > User Conf > Policies  Windows Setting > scripts  
[Nastaveni kultury - nova kultura](https://stackoverflow.com/questions/28281161/installing-more-cultures-on-windows-server-2012)  
### Prohlížení dokumentů:

PS - [Ghost View](http://www.cs.wisc.edu/~ghost/) , prohlíží i PDF  
PDF - [Adobe Acrobat Reader](http://www.adobe.com)  
DVI - DVIWIN  

### Skriptovaci a automatizacni nastroje

[Autoit](https://www.autoitscript.com/site/autoit/) ... automatizace klikani, basic like syntaxe  

### Windows prikazy

system32\slmgr.vbs -skms server:port ... nastaveni KMS klienta - centralni management Windows licneci  
system32\slmgr.vbs" /ato ... automaticke spusteni sluzby?  
netdom join $SERVER_NAME /domain:$DOMAIN /UserD:$USER /PasswordD:PASSWORD ... prida do domeny  
[[https://docs.microsoft.com/en-us/powershell/scripting/core-powershell/console/powershell.exe-command-line-help?view=powershell-5.1|
	PowerShell]] -Command "Get-EventLog -LogName security" ... spusti powershell a v nem uvedeny prikaz v soucasnem okne  

====Windows vestavene programy====

```
Accessibility Controls     access.cpl  
Add Hardware Wizard   hdwwiz.cpl
Add/Remove Programs   appwiz.cpl
Administrative Tools  control admintools
Automatic Updates   wuaucpl.cpl
Bluetooth Transfer Wizard   fsquirt
Calculator  calc
Certificate Manager   certmgr.msc
Character Map   charmap
Check Disk Utility  chkdsk
Clipboard Viewer  clipbrd
Command Prompt  cmd
Component Services  dcomcnfg
Computer Management   compmgmt.msc
Date and Time Properties  timedate.cpl
DDE Shares  ddeshare
Device Manager  devmgmt.msc
Direct X Control Panel (If Installed)*  directx.cpl
Direct X Troubleshooter   dxdiag
Disk Cleanup Utility  cleanmgr
Disk Defragment   dfrg.msc
Disk Management   diskmgmt.msc
Disk Partition Manager  diskpart
Display Properties  control desktop
Display Properties  desk.cpl
Display Properties (w/Appearance Tab Preselected)   control color
Dr. Watson System Troubleshooting Utility   drwtsn32
Driver Verifier Utility   verifier
Event Viewer  eventvwr.msc
File Signature Verification Tool  sigverif
Findfast  findfast.cpl
Folders Properties  control folders
Fonts   control fonts
Fonts Folder  fonts
Free Cell Card Game   freecell
Game Controllers  joy.cpl
Group Policy Editor (XP Prof)   gpedit.msc
Group Policy Resoult gpresult.exe
Hearts Card Game  mshearts
Iexpress Wizard   iexpress
Indexing Service  ciadv.msc
Internet Properties   inetcpl.cpl
IP Configuration (Display Connection Configuration)   ipconfig /all
IP Configuration (Display DNS Cache Contents)   ipconfig /displaydns
IP Configuration (Delete DNS Cache Contents)  ipconfig /flushdns
IP Configuration (Release All Connections)  ipconfig /release
IP Configuration (Renew All Connections)  ipconfig /renew
IP Configuration (Refreshes DHCP & Re-Registers DNS)  ipconfig /registerdns
IP Configuration (Display DHCP Class ID)  ipconfig /showclassid
IP Configuration (Modifies DHCP Class ID)   ipconfig /setclassid
Java Control Panel (If Installed)   jpicpl32.cpl
Java Control Panel (If Installed)   javaws
Keyboard Properties   control keyboard
Local Security Settings   secpol.msc
Local Users and Groups  lusrmgr.msc
Microsoft Chat  winchat
Minesweeper Game  winmine
Mouse Properties  control mouse
Mouse Properties  main.cpl
Network Connections   control netconnections
Network Connections   ncpa.cpl
Network Setup Wizard  netsetup.cpl
Notepad   notepad
Nview Desktop Manager(If Installed)   nvtuicpl.cpl
Object Packager   packager
ODBC Data Source Administrator  odbccp32.cpl
On Screen Keyboard  osk
Opens AC3 Filter (If Installed)   ac3filter.cpl
Password Properties   password.cpl
Performance Monitor   perfmon.msc
Performance Monitor   perfmon
Phone and Modem Options   telephon.cpl
Power Configuration   powercfg.cpl
Printers and Faxes  control printers
Printers Folder   printers
Private Character Editor  eudcedit
Quicktime (If Installed)  QuickTime.cpl
Regional Settings   intl.cpl
Registry Editor   regedit
Registry Editor   regedit32
Removable Storage   ntmsmgr.msc
Removable Storage Operator Requests   ntmsoprq.msc
Resultant Set of Policy (XP Prof)   rsop.msc
Scanners and Cameras  sticpl.cpl
Scheduled Tasks   control schedtasks
Security Center   wscui.cpl
Services  services.msc
Shared Folders  fsmgmt.msc
Shuts Down Windows  shutdown
Sounds and Audio  mmsys.cpl
Spider Solitare Card Game   spider
SQL Client Configuration  cliconfg
System Configuration Editor   sysedit
System Configuration Utility  msconfig
System File Checker Utility (Scan Immediately)  sfc /scannow
System File Checker Utility (Scan Once At Next Boot)  sfc /scanonce
System File Checker Utility (Scan On Every Boot)  sfc /scanboot
System File Checker Utility (Return to Default Setting)   sfc /revert
System File Checker Utility (Purge File Cache)  sfc /purgecache
System File Checker Utility (Set Cache Size to size x)  sfc /cachesize=x
System Properties   sysdm.cpl
Task Manager  taskmgr
Telnet Client   telnet
User Account Management   nusrmgr.cpl
Utility Manager   utilman
Windows Firewall  firewall.cpl
Windows Magnifier   magnify
Windows Management Infrastructure   wmimgmt.msc
Windows System Security Tool  syskey
Windows Update Launches   wupdmgr
Wordpad   write
```


### Scenare

==Spusteni jako administrator==

```
#spustit prikazovy radek s admin pravama
PsExec.exe -s -i c:\Windows\System32\WindowsPowerShell\v1.0\powershell_ise.exe 
```


### Active Directory

[Microsoft Active Directory Topology Diagrammer](https://www.microsoft.com/en-us/download/confirmation.aspx?id=13380) ... vizualizace nastaveni Active Directory  
nslookup -type=srv _kerberos._tcp.YOUR-DOMAIN ... získání Kerberos serveru na síti
