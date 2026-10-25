# Powershell

### Externi odkazy

[http://commandwindows.com](http://commandwindows.com/)  
[]()  

### Programy managovatelne PS

Exchange 2007+  
SQL 2008+  
System Center Data Protection  
System Center Operations Manager  
System Center Virtual Machine Manger  
atd.  

### Prikazy

&amp; spustitelny_soubor parametrt ... spusti spustitelny soubor s parametry, ktere se neinterpretuji jako PS parametry  

CALL D:\BATCH\SendSuccessMail.vbs ... spusti VBS  

### Nahrady z shellu

prikaz | grep ... prikaz | out-string -stream | select-string  
1.ErrorAction SilentlyContinue ... 2> /dev/null ... prepinac na potlaceni chyb  
Get-ChildItem -Path . -recurse | where { ($_.Mode -notlike 'd') -and ($_.LastWriteTime -gt (Get-Date).AddDays(-1)) } ... find . -mtime -1  
foreach ($i in $(ls *)) {"{0:N0} MB $i".replace('\','/') -f ( ( Get-ChildItem "$i" -Recurse | Measure-Object -Property Length -Sum -ErrorAction Stop).Sum / 1MB)} … du - smx * (velikost vsech podadresaru)  
gci -r| sort -descending -property length | select -first 10 name, length … 10 nejvetsich souboru  
### Promenne

Promenne jsou objekty, mohou obsahovat 1-dimenzionalni promenne, ale i sady promennych

help variables  
get-variable ... seznam promennych  
$PSVersionTable ... objekt obsahujici hodnotu verze  
$profile ... profilovy powershell  
$a=%%"%%$profile je profil%%"%% ... vlozeni promenne do promenne  
$a=%%"%%$profile je retezec%%"%% ... nezameni $profile za jeji hodnotu  
$text=%%"%%Ahoj, moje cislo je {0:N0} je to {1:P2} procent%%"%% -f 50.5432 0.15555 ... formatovani textu  
$d=Get-Date; %%"%%Dnes je {0: d. M. YYYY H:mm:ss}%%"%% -f $d ... formatovani datumu  
$a=%%"%%1%%"%%; [int]$a ... prevede retezec na cele cislo  
$? ... true posledni prikaz bez chyby. False- posledni prikaz selhal  
[xml]$pes='<dogs><dog name=%%"%%alik%%"%%/><dog name="cvalik"/></dogs>'  
$pes.dogs.dog[0] ... ukaze vlastnost dogs, prvni prvek z pole  
$p[5..-1] ... vsechny prvky od 5teho do posledniho  
$soubor | Get-Content C:\aaa.txt ... nacte vsechny radky do promenne typu pole  
${C:\aaa.txt}=$soubor ... ulozi obsah promenne do souboru  
$pole=1,2,3,4,5 ... definice pole  
$asocpole=@{ "Ferda" = "mravenec"; "Pytlik"="brouk"} ... definice asociiativniho pole  
$asocpole.keys, $asocpole.values, $assocpole["Ferda"], $assocpole[0] ... seznam klicu, seznam hodnot, hodnota pro klic  
$asocpole.add( "Bob", "kralik" ), $asspole.remove("Bob") ... pridani, odebrani prvku  
$null ... prazdny objekt  
$error ... pole chyb od startu powershellu  
$multiline=@"text na  
vice radku"@  
$LASTEXITCODE, $? ... posledni return code, True/False jestli posledni prikaz skoncil dobre (bez chyb/vyjimek)  
### Konfigurace

$profile ... profily - skripty co se vykonaji pri startu PS  
C:\Windows\System32\WindowsPowerShell\v1.0\*ps1xml ... vychozi vzhled zobrazeni prikazu jako get-process atd. Nemenit, prestane fungovat. Je treba vytvorit vlastni a podepsat  

### Operatory

help operators
#, <# #> ... komentare  
> >> 2> 2&>> ... presmerovani vystupu jako v shellu  
1.and -or -not -xor ... logicke operatory  
2.gt -lt -le ge -eq -like -clike ... binarni operatory (kdyz zacina na c - case sensitive, i - case insensitive)  
+ - * / %  ... aritmeticke operatory  
() ... operatorove zavorky  
$p -is "array" ... napise, zda je promenna pole  
"ahoj pane" -replace "pane","kluku" ... substituce  
(1..10) -join ";" ... spoji prvky pole pomoci oddelovace, vrati jako text  
"1,2,3" -split "," ... vrati pole, kde rozdeli text podle oddelovacu  

### Funkce

Funkce ulozene v souboru psm1 (modul), mohou byt naimportovany

Function Pozdrav ($jmeno) { write-host "ahoj $jmeno"} ... (moznost zadat typ [string]$jmeno) definice funkce s parametrem  
pozdrav "Honzo" ... (pozdrav -jmeno Honzo) vyvolani definovane funkce  
function secti ([int]$cislo1=0, [int]$cislo2= $(throw "nezadan parametr cislo2")) {} ... vychozi hodnoty, druha vychozi hodnota je "vykonej chybovou hlasku"  
Import-Module C:\labs\mod.psm1  
Get-module -listavailable ... seznam registrovanych modulu  
import-module SQLPS ... nacte modul pro praci MS SQL server  
get-command -module SQLPS ... ukaze prikazy modulu SQLPS  

### rizeni toku

foreach-object ($i in $array) { Write-Host $i; $_ } ... (foreach, %) pro kazdy prvek $i v poli $array, vypis ho a vrat ho jako objekt  
if ($promenna -eq $null) { "neni definovano" } elseif { "OK" } elseif { "nemuze nastat" } ... if else podminky  
get-service | foreach ... jina moznost for foreach  
for ( $i=1 ; $i -lt 5 ; $i++ ) {} ... for smycka  
while ( $i -ne 2 ) {} ... while smycka  
break ... prerusi cyklus  
continue ... preskoci zbytek bloku a skoci zase na dalsi beh bloku  

### Chyby, debugging

1.ErrorAction SilentlyContinue ... potlaceni chybovych hlaseni - akce jako $errorview, ale jen pro tento beh  
2.errorVariable x ... chyba se ulozi do promenne $x pro tento beh prikazu i do $error  
throw "chyba" ... vyvolani chyby  
$error ... seznam vsech chyb od startu powershellu  
$errorview ... prepinani runych vzhledu chyb  
$erroractionPreference=SilentlyContinue ... akce co ma PS delat kdyz narazi na chybu - pokracuje, nezobrazuje chybu  
try { dir \asd } catch { write-host Error happen: $_.Exception.Message } ... try a catch blok pro akce v pripade chyby v try bloku  
Set-PSDebug -Trace 1 ... zapne debug mod urovne 1  
Set-PSDebug -Step ... pta se me, kdyz chci skocim do interaktivniho modu prohlizet promenne, vratim se exit-em  
Set-PSDebug -off ... vypnu debug mode  
Set-StrictMode -version "1.0" ... hlasi chyby, kdyz promenna neexistuje  
Set-StrictMode -version "2.0" ... hlasi chyby, i kdyz promenna neexistuje i kdyz metodna, vlastnost neexistuje  
Set-StrictMode -off ... Vypne strict mode  
$host.EnterNestedprompt() ... skoci v tomto radku do debug modu ve skriptu a po exit zase pokracuje  
Set-PSBreakPoint -Command Stop-Process ... definice break pointu pro prikazu Stop-Process (jine uziti: pri zmene promenne, na radku x), h help v interaktivnim modu  
Get-PSBerakPoint ... vylistovani break pointu  

### MSSQL

Import-Module SQLPS  
cd SQLSERVER:/  
cd SQL\ROCKET\DEFAULT\DATABASES\DATABASE\TABLES\Schema.Table\Columns  
Invoke-SqlCmd "CREATE TABLE Lide (id int, jmeno nvarchar(50), prijmeni nvarchar(50))"  
import-csv C:\labs\lide.csv | foreach { Infoke-sqlcmd ("INSERT INTO dbo.lide (id, jmeno, prijmen) VALUES (" + $_.id + ", '" + $_.jmeno "', '" + $_.prijmeni + "')") }  
Invoke-SqlCmd "SELECT TOP 10 * FROM lide"  

### promenne

$env:temp ... promenna prostrendi (Get-help about_Environment_Variable)  
$args ... argumenty (parametry) ktere doplnuji prikaz, skript  
'banan' ... retezec  
('banan').GetType() ... typ promenne  

### Comlet-y

add-content ... to same jako >>, podporuje parametr -encoding  
add-windowsfeatire / install-windowsfeature  
compare-Obejct $objekt1 $objekt2 ... (compare) porovna 2 objekty, ukaze rozdilnosti  
convertTo-html  
convertTo-csv  
export-clixml C:\a.xml ... vystup objektu do xml  
export-clixml C:\a.xml ... vystup objektu do csv  
format-disk  
format table ... zobrazi vystup jako tabulku (vychozi vystup)  
format table id,processname -autosize ... zobrazi vystup jako tabulku, jen vybrane sloupce  
format-list * ... (fl) naformatuje vystup jako seznam "promenna : hodnota", * zobrazi vsechny hodnoty objektu (zobrazi to v jine forme)  
get-alias ... vypise nadefinovane aliasy  
get-acl C:/windows ... ukaze ACL zkracene info o souboru/adresari  
get-acl C:/windows | **fl * ** ... naformatuje vystup ze ukaze vsechny pole objektu  
get-command ... seznam vsech prikazu (aliasu, comandletu atd.)  
get-childitem -recurse... (dir) rekurzivni seznam souboru  
get-childitem | where { $_.Lenght -ge 10MB } ... ukaze soubory vetsi nez 10 MB  
get-childitem HKCU:\,HKLM:\ -recurse -include *PoerShell* ... rekurzivni hledani  
get-childitem Cert:\ -CodeSigningCert -recurse ... hledani certifikaty  
Get-content soubor.txt ... vypise obsah souboru  
Get-content soubor.txt -tail 20 ... vypise poslednich 20 radek ze souboru  
Get-Content server.log -wait ... zobrazi a zobrazuje vsechny nove radku  
get-executionpolicy (-list)... zobrazi nastaveni pro spousteni ps skriptu  
**get-help *alias** ... seznam vsech prikazu obsahujici alias v nazvu  
get-help help -full ... kompletni info o prikazu help  
get-help add-comupter -examples ... priklady  
get-help -? ... help  
get-history ... ukaze historii prikazu  
get-itemProperty HKCU:\Software\Microsoft\Windows\CurrentVersion\Run "(Default)" ... ziska hodnotu registru  
get-member ... ziska vlastnosti objektu (metody, vlastnosti, atd.)  
get-process | where { $_.handles -gt 80 }  
get-psdrives ... vylistuje vsechny "ps disky" - aliasy pro ruzne objekty - disky, adresare, registry, promenne atd.</br>
Get-Service | Where-Object {$_.displayName.StartsWith("NATION-")} | Select name ... seznam vsech sluzeb  
get-wmiObject Win32_LogicalDisk|select DeviceID,@{Label='Free Space'; Expression={$_.FreeSpace/1GB}} ... vylistuje logicke disky  
get-wmiObject Win32_OperatingSystem | fl $_.caption ... vytiskne verzi operacniho systemu  
group-Object Status ... (group) seskupi polozky z objeku pomdle sloupce Status  
Invoke-History 85 ... vyvola prikaz z historie  
invoke-command -computername aaa .... ... spusti prikaz na vzdalenem pocitaci  
import-clixml ... vypise objekty z xml zachycene pomoci export-clixml  
import-csv ... importuje z csv souboru  
join-path ([Environment]::GetFolderPath("Desktop)) "text.txt" ... spoji cesty  
(Measure-Command {dir -include *.ps1 -recursive}).totalSeconds ... meri kolik sekund trva prikaz  
measure-object -property sum -minimum -maximum sum ... (measure) kdyz se presmeruji objekty do measure, umi je zmerit - pocet objekty, min,max,avg,sum jednotlivych vlastnosti  
new-item -path . -name new_dir -type directory ... vytvori novy adresar  
new-item -path . -name new_file -type file -value "text  ... vytvori novy soubor  
new-itemProperty  
out-gridview ... zobrazi vystup v grafickem okne, filtr a trideni k dispozici  
out-null ... /dev/null  
out-printer ...  
out-host ... standartni vystup  
out-file ... vystup do souboru, nativni prikaz pro >  
out-string -strea ... vypise objekty jako retezec  
Push-Location ... ulozi si aktualni adresar do pameti (stack)  
Push-Location -stack job1 ... pojmenovani stacku, mozno mit vice ulozenych  
Pop-Location ... vrati aktualni adresar  
read-host ... vstup z std. vstupu  
remove-Variable aaa ... dealokuje promennou  
remove-windowsfeature  
resolve-path ... konvertuje relativni cestu na absolutni  
restart-computer  
send-mailMessage ... posle mail  
set-acl  
set-content ... to same jako >  
set-executionpolicy remoteSigned ... povoli spousteni PowerShell skriptu z lokalni masiny  
select -property Name,VM -first 10 ... ukaze jen vlastnosti Name a VM, jen 10 prvnich radku  
select-string "aaa" ... jako grep  
sort -property CPU -descending ... setridi vystup podle vlastnosti  
start-process ... (start) spusti soubor vychozi aplikaci  
tee-object ... ulozi objekt do souboru ale i na std. vystup  
where-object { $_.name -eq "notepad" } ... (where) vybere jen specifikovane objekty, podobne jak v sql  
write-host $profile -foregroundcoler red ... vypise na obrazovku promennou $profile cervene  
write-host "`n`n`thello`n" ... vypise : novy radek, novy radek, tabulator, hello, novy radek  

### Podepisovani klicem

cd Cert:  
$cert=dir -recursive -CodeSigningCert | where { $_.thumbprint -eq "dsafasdfasdfsadf" }  
set-authenticodesignature -filepath  .\a.ps1 -certificate $cert  

### vzdalene spousteni

$Host.ui.PromptForCredential("Matrix OS", "Enter the credentials","Administrator","") ... nepovinne, zmeni texty v get-credential  
$cred=get-credential    nebo   $password=convertto_securestring -asPlainText -Force "Heslo"; $cred=New-Object System.Management.Automation.PSCredential("User", $password)  
Invoke-Command -scriptblock { cls } -credential $cred -computername ROCKET  

### Active Directory

Import-Module ActiveDirectory  
cd AD:\  
cd "DC=turbomax,dc=local"  
cd "CN=Users  
dir | where {$_.name -eq tomas} | select *,@{Label='Path';Expression={$_.PSPath}} | del ... vymaze uzivatele  
remove-ADUser tomas  
$secure=ConvertTo-SecureString "Password1" -asplaintext -force
new-ADUser franta -AccountPassword $sercure -Enabled $true  
Invoke-SqlCmd -hostname . -Database AdventureWorks2012 -query "SELECT TOP 10 * from person.person" | foreach { New-ADUser -name ("user" + $_.id) -AccountPassword $password -Enabled $true -Given name $_.FirstName -Surname $_.LastName } ... vytvoreni uzivatelu z SQL tabulky  

### COM integrace - COM objekty

$object=New-Object -comObject WScript.Shell  
$object|Get-Member -memberType *Method  
$path=[system.environment]::getFolderPath('Desktop')  
$link=$wshell.CreateShortcut("$path\PowerShell.lnk")  
$link | get-member  
$link.TargetPath='powershell.exe'  
$link.Description='PS'  
$link.WorkingDirectory=$profile  
$link.IconLocation='powershell.exe'  
$link.save() ... ulozeni linku z objektu, pokud nenadefinujeme povinne parametry, tak bude chyba  

$IE=New-Object -ComObject 'InternetExplorer.Application'  
Eie.navigate("http://www.google.com")  
$ie.visible=$true  
$ie.quit  

$o=New-Object -ComObject Shell.Application  
$o.ToggleDesktop() ... minimalizace vsech oken  

[threading.thread]::CurrentThread.CurrentCulture='en.US'  
$Excel=New-Object -Com Excel.Application  
$excel.visible=$true  
$excel.workbook.add()  

### WMI

Informace poskytuje WMI sluzba (Windows Management Instrumentation)

Get-WmiObject -list  
Get-WmiObject Win32_OperatingSystem | fl *  
Get-WmiObject Win32_Process | fl * ... seznam procesu vcetne plneho prikazu  
Get-WmiObject Win32_Process -Filter "name = 'notepad.exe'" | select CommandLine ... filter na notepad.exe a vypis plneho prikazu  
Get-WmiObject Win32_NetworkAdapter | fl *  
Get-CimInstance CIM-Processor  
Get-CimInstance CIM-Processor -ComputerName .  
Get-WmiObject -class Win32_LogicalDisk  
Get-WmiObject -Query "Select * from Win32_LogicalDisk WHERE DeviceID='C:'"  

### Remoting

Get-WinEvent -logName Security -ComputerName DC1 -credental startrek\administrator ... jedna cesta jak spoustet prikazy  

WinRM sluzba, jede na HTTP/HTTPS a SOAP, potrebuje PSv2, .NET2 a vyssi, ..., jede na portu 5985

WinRM quickconfig ... Win prikaz - nastavi listener, dovoli administratorum pristup  
Set-WSManQuickConfig ... to same, ale z PS  
Enable-PSRemoting ... spusti Set-WSManQuickConfig a ruzna pravidla na povoleni  
new-pssession ... vytvori noe pripojeni, ale nepripoji se  
enter-pssession ... vytvori a pripoji se  
$s=new-session|enter-session ... pripoji se k existujicimu spojeni  
get-pssession ... seznam PS spojeni  
exit-pssession ... vyskoci ze spojeni  
remove-pssession ... ukonci spojeni  

### Jobs

Start-Job -name NewJob -Scriptblock {Get-Service} ... spusti ulohu na pozadi, napr. na jinem pocitaci  
Get-Job ... informace of ulohach  
Receive-Job -name newJob ... obdrzi vysledky - objekty z bufferu, muze to byt job ze scheudleru, vysledky se ulozi na pocitaci v xml  
Receive-Job -name newJob -keep ... vysledky se nechaji na pocitaci, neprepisi se
Remove-Job -name newJob ... smaze vysledky  
Get-SchedulerJob  
Set-SchedulerJob  
Set-ScheduledTask  
get-SchedulerTask  

### Logovani, auditovani

[Start-Transcript](https://technet.microsoft.com/en-us/library/hh849687.aspx)  

### Regularni vyrazy

"cislo 00420 111 222 333" - match "\d{1-4}[ -]\n{1-3}[ ]?\n{1-3}[ ]?\n{1-3}" ... zjisti pritomnost regularniho prikazu  
$matches ... vysledek hledani  
$text -replace "(?m)^",| " ... substituce na vice radcich, na zacatek kazdeho radky vlozi | "  

### prace s xml

[xml]$xml="&lt;a&gt;&lt;b&gt;&lt;c&gt;text&lt;/c&gt;&lt;d&gt;3&lt;/d&gt;&lt;/b&gt;&lt;/a&gt;" ... import xml lze provest i zadanim retezce  
$xml.a.b.text="5"  
$xml.save("C:\employees.xml")  

### Eventlog

Get-Eventlog -list ... stara metoda, pomale, ne vsechny eventy, funguje vsude  
Get-EventLog Aplication | where { $_.EventType -eq "Error" }  
Get-WinEvent -ListLog *operational*  
[xml]$filter=Get-Content("xmlfilter.xml")  
Get-WinEvent -filterXml $filter  

### Bitlocker

Suspend-BitLocker ... docasne vypne protekci disku  
Enable-BitLocker ... zakryptuje disk  
Disable-BitLocker ... zrusi enkrypci disku  
Resume-BitLocker ... obnovi enkrypci  

### Interaktivni priazy

Get-Counter -listSet * | where { $_.CounterSetName -like "*processor*" }  
get-Counter -Counter "\Processor(0)\% User Time" -Continuous | where { $_.CounterSamples.CookedValue -gt 10 } | foreach { "{0};{1}" -f (Get-date),($_.CounterSamples.CookedValue) }  

### Sanpin-y

Stare moduly v PS v.1. V novych verzich je nahradily moduly, ale snapiny jsou furt podporovane

### Moduly

### .NET integrace

PowerShell is .NET aplikace (.NET alternativa Javy na Win platformach)

$p=new-object System.Net.NetworkInformation.Ping ... iniciace noveho objektu dane tridy  
$p.send ... help k metode  
$a=$p.send('google.com') ... vyvolani metody, navratovy objekt se priradi promenne $a  
$a.Address.IPAddressToString ... vypise vlastnost objektu - ipadresu  
$message=New-Object System.Net.Mail.MailMessage(From,To)  
$message.Subject="Subject"  
$message.Body="Body"  
$attachment=New-Object System.Net.Mail.Attachment("c:\test.txt")  
$message.Attachments.Add($attachment)  
$client=New-Object System.Net.Mail.SmtpClient($SMTPServer)  
$client.Send($message)  
[system.math]::PI ... pouziti staticke tridy (nelze vytvorit objekt) na ziskani konstanty pi  
[Math] | get-member - static -membertype ... ziskani vlastnosti a metod staticke tridy  
[Environment]::GetFolderPath("Desktop") ... vrati cestu na Desktop  
[System.IO.Path]::Combine([Environment]::GetFolderPath("Desktop"),"test.txt")  
[System.O.Path] | gm -static ... seznam statickych metod a vlastnosti  
System.IO ... prace se vstupy/vystupy  
System.Text ... prace s texty  
System.Data ... prace z databazemi  
System.Threading  
System.Collections ... prace s poli, asoc. poli atd  
System.Xml ... prace s xml  
System.Net ... prace se siti  
System.Security ... prace s bezpecnosti - enkrypce, dekrypce, certifikaty  
System.Globalization ... lokalizace  
$a=New-Object System.Globalization.Cultureinfo("cs-CZ")  
$b=13.45; $b.toString("c") ... preformatuje to na menu  
$b.toString("c",$a) ... preformatuje to na cz menu  
$a.NumberFormat.CurrencySymbol="HUF" ... zmeni menu pro lokalizaci  

### Priklady

Get-Mailbox | Sort Size | Selevt -first 100 | | Move-Mailbox Server2
