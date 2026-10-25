# iis

### Start/stop/status

iisreset /start ... start IIS
iisreset /restart ... restart IIS
iisreset /stop ... stop IIS
net stop WAS ... Stop Windows Process Activation Service (WAS) a W3SVC
net start W3SVC ... start IIS - WAS + W3SVC

### Konfigurace

[https://docs.microsoft.com/en-us/iis/configuration/](https://docs.microsoft.com/en-us/iis/configuration/) ... dokumentace ke konfigurace (web.config)  

### Logy

C:\Windows\System32\LogFiles\HTTPERR\httperr28.log  
C:\Windows\system32\inetsrv\appcmd.exe list config | select-string "logFile.*directory"  
Get-EventLog Application | where Source -like "w3*"  
Get-EventLog Application | where Source -like ".NET*"  
Get-WinEvent -LogName Microsoft-IIS-Configuration/Administrative | select -first 10  
Get-WinEvent -LogName Microsoft-IIS-Configuration/Operational | select -first 10  
### Prikazy

dir IIS:\AppPools\MyAppPool\WorkerProcesses\ | % { Stop-Process -id $_.processId } ... zabije vsechny workery  
cd c:\windows\system32\inetsrv; .\appcmd list wp ... sezam workeru  
cd c:\windows\system32\inetsrv; .\appcmd.exe list site ... seznam asociovanych URL  
cd c:\windows\system32\inetsrv; .\appcmd.exe list app ... seznam asociovanych aplikaci\
cd c:\windows\system32\inetsrv; .\appcmd.exe list apppool ... seznam asociovanych aplikacnich poolu  
cd c:\windows\system32\inetsrv; .\appcmd.exe list module ... seznam iis modulu  
cd c:\windows\system32\inetsrv; .\appcmd.exe list vdir ... seznam asociovanych Virtualnich adresaru  
cd c:\windows\system32\inetsrv; .\appcmd list requests ... seznam HTTP requestu  
cd c:\windows\system32\inetsrv; .\appcmd list requests /elapsed:5000 ... seznam HTTP requestu delsich nez 5 sekund  
gwmi -NS 'root\WebAdministration' -class 'WorkerProcess' | select AppPoolName,ProcessId ... seznam workeru  
.\appcmd.exe list config  -section:webFarms ... vypis vsech load balancer prvku  
.\appcmd.exe list config -section:system.webServer/rewrite/globalRules  
.\appcmd.exe list config | select-string "^<" ... sezam vsech zakladnich sekci konfigu  
.\appcmd.exe set config  -section:webFarms /+"[name='$($farm.name)']" /commit:apphost ... vyrvoreni web farmy  
.\appcmd.exe set config "sonarqube" -section:httpRuntime /-maxRequestLength ... odebere atribut maxRequestLength ze sekce httpRunTime  
.\appcmd.exe set config -section:httpRuntime /maxRequestLength:102400 ... prida/zmeni atribut maxRequestLength s hodnotou 102400  
.\appcmd.exe set config -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:"104857600" ... zmeni/prida klic a atribut  

### PowerShell

Get-LocalIISSite ... informace o Site  
Get-WebConfigurationProperty -Filter "//defaultDocument/files/add" -PSPath "IIS:\Sites\D
efault Web Site" -Name "value"  
(get-WebConfiguration -Filter "/webFarms").Collection ... Ukaze web farmy  
get-WebConfigurationProperty -PSPath 'MACHINE/WEBROOT/APPHOST' -Filter "webFarms/webFarm
[@name='AsiaAdmin']/applicationRequestRouting" -name 'healthCheck' ... ukaze vlastnosti healtchecku  
Get-WebAppPoolState ... stav aplikacnich poolu  
Get-WebBinding ... ukaze porty navazane na IIS  
Get-WebCentralCertProvider ... certifikacni poskytovatel  
Get-WebConfigFile ... konfiguracni soubor  
Get-WebGlobalModule ... sezanm modulu a odpovidajicich knihoven DLL  
Get-WebHandler  
Get-WebManagedModule  
Get-Website ... seznam webovych site  
Get-WebBinding -Port 80 -HostHeader ping -Name default | Remove-WebBinding ... odstrani binding
