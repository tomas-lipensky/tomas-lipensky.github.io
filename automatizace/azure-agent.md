# azure-agent

## Hybrid Worker

[Hybrid Runbook Worker](https://docs.microsoft.com/cs-cz/azure/automation/automation-hybrid-runbook-worker) ... agent nainstalovany v datacentru, ktery umi spoustet runbooky mimo Azure

[Azure VM agent](https://docs.microsoft.com/en-us/azure/virtual-machines/extensions/agent-windows)  
C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\*\HybridAgent  
C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\*\HybridRegistration  
[Logy](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics-troubleshooting), binarky atd. diagnostickych agentu  
get-process -ProcessName Orchestrator.Sandbox  ... aktualne spustene runbooky v Hybrid workeru  
Get-WmiObject Win32_Process -Filter "processid = 1976" ... informace o rubbooku (ziskaneho z get-process) - informace o docasnem adresari s logama  
(Get-WinEvent 'Microsoft-Automation/Operational' )[0].Properties ... informace o poslednim ukoncenem runbooku v Event logu  
C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes ... logy Runbooku  

`Get-childItem 'HKLM:\SOFTWARE\Microsoft\HybridRunbookWorker'` ... kdyz existuje, hybrid worker je pripojeny k autoamtion accountu  
`Get-EventLog "Operations Manager" | select -First 10` ... Eventlogy k Hubrid workeru (Healthservice)  
`Get-EventLog "Operations Manager" | where EntryType -eq Error | select -First 1 | fl *` ... vypis chyby  

Oprava spatnych prav k adresari s certifikatama:
  $acl=get-acl C:\ProgramData\Microsoft\Crypto\RSA\MachineKeys\
  $acl | fl *
  $permission = "Everyone","Modify", 'ContainerInherit,ObjectInherit', 'None', 'Allow'
  $accessRule = New-Object System.Security.AccessControl.FileSystemAccessRule $permission
  $permission = "BUILTIN\Administrators","Modify", 'ContainerInherit,ObjectInherit', 'None', 'Allow'
  $accessRule = New-Object System.Security.AccessControl.FileSystemAccessRule $permission
  $permission = "NT AUTHORITY\NETWORK SERVICE","Modify", 'ContainerInherit,ObjectInherit', 'None', 'Allow'
  $accessRule = New-Object System.Security.AccessControl.FileSystemAccessRule $permission
  $acl.SetAccessRule($accessRule)
  $acl |Set-Acl

`Import-Module 'C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\*\HybridRegistration\HybridRegistration.psd1'` ... import modulu na registraci/odregistraci modulu
`Add-HybridRunbookWorker -GroupName TestGroup -EndPoint '$URL' -Token '$KEY' -Verbose` ... registrace Hybrid workera do group  
`Remove-HybridRunbookWorker -EndPoint '$URL' -Token '$KEY' -Verbose` ... odregistrace hybrid workera z grupy  

## Diagnostics extension agent (WAD)

Rozsireny monitoring - data z OS

C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics #... instalacni adresar  
C:\WindowsAzure\logs\plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics #... logy  
.\DiagnosticsPluginLauncher.exe -disable #... zastaveni agenta  
.\DiagnosticsPluginLauncher.exe -uninstall #... odinstalace agenta  
.\DiagnosticsPluginLauncher.exe -install #... instalace agenta  
DiagnosticsPluginLauncher.exe -update  
DiagnosticsPluginLauncher.exe -resetState  
DiagnosticsPluginLauncher.exe … restart agenta  

## Dependency Agent

Monitorovani procesu a zavislosti

## Log Analytics agent (drive Microsoft Monitoring Agent, MMA)

[MMA](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-agent-windows) se stara o poskytovani Hybrid Worker a Log Analytics funkci. Data posila do OMS (Operations Management  Suit) Workspace.

### Windows

dpkg -l omi omsagent omsconfig ... seznam balicku, verze agenta  
C:\Program Files\Microsoft Monitoring Agent\Agent\AgentControlPanel.exe ... nastaveni MMA  
Logy v Eventlogu  
C:\WindowsAzure\logs\WaAppAgent.log  
update_azureoperationalinsight_agent_heartbeat ... task ve windows scheduleru  
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log ... heartbeat log file  
C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent ... log soubory  
(New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List ... status MMA  
C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs ... setup log soubor  

Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName ... deployment status videny ze strany Azure  
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table  

`& 'C:\Program Files\Microsoft Monitoring Agent\Agent\TestCloudConnection.exe'` ... test pripojeni k workspace  

Pridani dalsiho workspace:
  $AgentCfg = New-Object -ComObject AgentConfigManager.MgmtSvcCfg
  $Workspaces = $AgentCfg.GetCloudWorkspaces()
  $WorkspaceID = 'ID'
  $WorkspaceKey = 'KEY'
  $Workspaces = $AgentCfg.GetCloudWorkspaces()
  $AgentCfg.AddCloudWorkspace($WorkspaceID,$WorkspaceKey)
  $AgentCfg.ReloadConfiguration()

Logy z MMA v Azure:
  search *   | where Type == "Heartbeat"
| where Category == "Direct Agent"
| where TimeGenerated > ago(30m)

### Linux

/opt/microsoft/omsagent/bin/omsadmin.sh -l  ... Seznam asociovanych workspacu  
/etc/opt/omi/conf/omiserver.conf  
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh --purge ... odinstalace  
sudo /opt/microsoft/omsagent/bin/service_control restart ... restart sluzby  
systemctl status omsagent-LAD.service ... status sluzby  
/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log  
/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log  
/var/opt/microsoft/omsagent/log/omsagent.log  
/opt/microsoft/omsagent/bin/stdout  
/var/lib/waagent/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux-*/omsagent.py -uninstall ... odinstalace agenta  
omsagent.py -uninstall ... zakazani agenta  
sudo -u omsagent /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py ... check  
## Network Watcher Agent

[NWA](https://docs.microsoft.com/en-us/azure/virtual-machines/extensions/network-watcher-windows) umi merit statistiky site.

Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent ... status z pohledu z Azure  
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\  

## PowerShell DSC Extension

[DSC Extension](https://docs.microsoft.com/en-us/azure/virtual-machines/extensions/dsc-windows) nahrava a spousti DSC soubory.

Deploy:

```bash
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name Microsoft.Powershell.DSC \
  --publisher Microsoft.Powershell \
  --version 2.73 --protected-settings '{}' \
  --settings '{}'
```

az vm extension list --resource-group myResourceGroup --vm-name myVM -o table ... status  
Set-AzureVMExtension -ExtensionName $extensionName -VM $vm -Publisher $publisher  -Version $version -PrivateConfiguration $privateConfig  -PublicConfiguration $publicConfig | Update-AzureVM  

## Virtual Machine Access Extension

[VMAccess Extension](https://docs.microsoft.com/en-us/azure/virtual-machines/extensions/vmaccess) umoznuje pripojeni k VM z portalu.

az vm user update --resource-group myResourceGroup --name myVM --username azureuser   --ssh-key-value ~/.ssh/id_rsa.pub ... reset SSH klice  
az vm user update --resource-group myResourceGroup --name myVM --username azureuser --password myNewPassword ... reset hesla  

az vm user reset-ssh --resource-group myResourceGroup  --name myVM ... restart Ssh demona  

az vm user delete
1.-resource-group myResourceGroup
2.-name myVM
3.-username myNewUser ... smazani uzivate  

az vm extension list --resource-group myResourceGroup --vm-name myVM -o table  

## Windows Azure Linux Agent

WAA - Windows Azure Linux Agent - zajistuje trvalost hostname (jinak se meni po kazdem rebootu) a jine  
/etc/waagent.conf  
/var/lib/waagent/ovf-env.xml  
waaagent -version  
/var/log/waagent.log ... log soubor  

[sudo apt-get install walinuxagent](http://blog.admindiary.com/persist-azure-linux-virtual-machines-hostname/) ... balicek  
/etc/waagent.conf ... nastaveni  
systemctl restart walinuxagent.service  

## InfluxData Telegraf Agent

[Influx Telegraf](https://www.influxdata.com/time-series-platform/telegraf/) agent pro Linux na reportovani rozsirenych metrik
