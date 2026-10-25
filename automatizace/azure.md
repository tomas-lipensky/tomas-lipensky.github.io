## Azure

### Externi odkazy

[docs.microsoft.com/en-us/learn/](https://docs.microsoft.com/en-us/learn/)  
[docs.microsoft.com/en-us/azure/](https://docs.microsoft.com/en-us/azure/)  
[docs.microsoft.com/en-us/azure/architecture/](https://docs.microsoft.com/en-us/azure/architecture/)  
[azure.microsoft.com/en-us/solutions/architecture/](https://azure.microsoft.com/en-us/solutions/architecture/)  
[azureinteractives.azurewebsites.net/Azure101Cards](http://azureinteractives.azurewebsites.net/Azure101Cards/default.html?wt.mc_id=AID625426_QSG_SCL_242981)  
[Migrace VM z ASM do ARM](https://blogs.technet.microsoft.com/diegoviso/2015/12/10/migrating-azure-virtual-machines-from-asm-to-arm/)  
[Vice info k priprave](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/migration-classic-resource-manager-overview)  
[azureinteractives.azurewebsites.net/CloudDesignPatterns/default.html](https://azureinteractives.azurewebsites.net/CloudDesignPatterns/default.html)  
[MS Channel 9](https://channel9.msdn.com/) ... portal videi or vyvojaru z Microsoftu  
[Microsoft Virtual Academy](https://mva.microsoft.com/)  
[Cenova kalkulacka mezi datacentry](https://azureprice.net/?region=southindia)  
[Omezeni a limitace](https://docs.microsoft.com/cs-cz/azure/azure-subscription-service-limits) predplatnych v ARM Azure  
[CCO Dashboard](https://github.com/Azure/ccodashboard) ... Power BI dashboard s prehledem zdroju v predplatnych  
[https://feedback.azure.com/](https://feedback.azure.com/) ... User voice - misto na zadavani novych napadu k Azure a k hlasovani o nich  
[https://play.google.com/store/apps/details?id=com.microsoft.azure](https://play.google.com/store/apps/details?id=com.microsoft.azure) ... Androidi aplikace na sledovani udalosti z Azure  
[https://status.azure.com/en-us/status/history/](https://status.azure.com/en-us/status/history/) ... historie stavu, problemu a vypadku Azure  
[https://www.azurenotes.tech/](https://www.azurenotes.tech/) ... Novinky v Azure  
[https://azurecharts.com/](https://azurecharts.com/) ... Azure Heat Map - analyza nejcasteji se menicich funkci Azure  

[https://github.com/Azure-Samples/aci-helloworld](https://github.com/Azure-Samples/aci-helloworld) ... php hello world aplikace do App Service, repozitar obsahuje mnoho demonstracnich kodu  
[https://github.com/MicrosoftLearning](https://github.com/MicrosoftLearning) ... Microsoft learning cviceni  
[https://github.com/godeploy/](https://github.com/godeploy/) ... Cviceni pro godeploy  
### Dodatecne nastroje

[azcopy](https://azure.microsoft.com/cs-cz/blog/azcopy-5-1-release/) ... nastroj na kopirovani do/z Azure Blob, File, Table  

### Interni odkazy

[AZCLI](AZCLI)  
[PowerShellAzure](PowerShellAzure)  
[AzureRestApi](AzureRestApi)  
[Azure dotazy na logy a diagnostiku](automatizace/azure-dotazy) .. Kusto Query Language  
[azure-runbook](azure-runbook)  
[azure-arm](azure-arm)  
#### Komponenty, agenti

[azure agenti](azure-agent)

### Webove nastroje

[portal.azure.com](https://portal.azure.com)  
[https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FGoDeploy%2FAZ300%2Fmaster%2Fxg-azure-master%2FmainTemplate.json](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FGoDeploy%2FAZ300%2Fmaster%2Fxg-azure-master%2FmainTemplate.json) ... spusteni ARM template (sablony) z portalu  
[resources.azure.com](https://resources.azure.com/)  
[ARM Vizualizer for Azure Templates](http://armviz.io/designer)  
http://169.254.169.254/metadata/instance?api-version=2019-08-01 ... URL aktivni z managovaneho VM na zjisteni metadat o sobe samem  
### Nastroje na lokalni pocitac

[SSMS](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) … SQL Server Management Studio - graficke prochazeni MSSQL a Azure database  
Microsoft Azure Storage Explorer … graficke prochazeni Account storage, tabulek, souboru atd
[Portal](https://preview.portal.azure.com/app/Download) ... lokalni aplikace s Azure Portalem  

### Funkcionalita

[PIM](https://docs.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-configure) - docasne prideleni vyssich prav uzivateli  
[Update management](https://docs.microsoft.com/cs-cz/azure/automation/pre-post-scripts) vcetne pre/post sckriptu na updatovani WIndows/Linux OS  
### PowerShell Az

[Install-Module Az](https://azure.microsoft.com/en-us/blog/azure-powershell-cross-platform-az-module-replacing-azurerm/) ... Instalace Az modulu (Win, Lin, ...) jede na vsech platformach  
Login-AzAccount ... pripojeni na Azure  
Get-AzSubscription ... seznam predplatnych  
Get-AzSubscription … seznam predplatnych  
Set-AzContext $(Get-AzSubscription -SubscriptionName AAA) … vyber predplatneho  
Enable-AzAlias [-Module <string>] [-Scope Process | CurrentUser | LocalMachine] ... nastaveni kompatibility Az a Az pomoci aliasu  
Disable-AzAlias [-Module <string[]>] [-Scope Process | CurrentUser | LocalMachine] ... vypnuti aliasu  
### PowerShell AzureRm

Login-AzureRmAccount ... pripojeni na Azure  
Add-AzureRmAccount  
Get-AzureRmSubscription ... seznam predplatnych  
Set-AzureRmContext $(Get-AzureRmSubscription -SubscriptionName AAA) ... vyber predplatneho  
Select-AzureRmSubscription -SubscriptionId "yoursubscriptionid" ... vyber subsciption  

### Resources a Resource groups (zdroje a skupiny/mnoziny zdroju)

Get-AzResourceGroup ... seznam vsech Resource group  
Get-AzResourceGroup | Export-AzResourceGroup -IncludeParameterDefaultValue ... ulozi Resource groupy jako JSON template  
Get-AzResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines ...  

### Virtualni stroje - Virtual Machine

Get-AzVm -ResourceGroupName RGtlipensky -name VMtlipensky ... informace o VM  
Get-AzVMDiagnosticsExtension -ResourceGroupName RGtlipensky -vmname VMtlipensky ... ukaze diagnosticke rozsireni ([skript na aktivaci rozsirenych metrik](https://github.com/Cloudyn/azure-enable-diagnostics))  
Get-AzPublicIpAddress -Name $publicIpName -ResourceGroupName $rgName … seznam verejnych adres  
[Invoke-AzVMRunCommand](https://docs.microsoft.com/en-us/powershell/module/az.compute/invoke-azvmruncommand?view=azps-1.4.0) -ResourceGroupName RG -VMName VM -CommandId 'RunPowerShellScript' -ScriptPath 'C:\a.ps1' ... spusti skript na serveru (z Azure agenta)  
Set-AzVMCustomScriptExtension -ResourceGroupName az104-08-rg01 -VMName az104-08-vm0 -Location EastUS -ExtensionName "IIS" -FileURI 'https://raw.githubusercontent.com/godeploy/AZ104/master/Module08/az104-08-install_IIS.ps1' -Run 'az104-08-install_IIS.ps1' ... prida custom script rozsireni a provede jim dany skrip  

### Audit - Activity log

Get-AzLog -StartTime 2018-10-10T10:30 | where-object { $_.HttpRequest.Method -eq "DELETE" } | select-object Caller,EventTimestamp,Authorization ... vypis DELETE akci  
Get-AzLog -StartTime (Get-Date).AddDays(-7) | Where-Object {$_.Authorization.Action -like 'Microsoft.sql/servers/*'} ... vypis za posledni tyden na MSSQL serverech  

### Databaze

Find-AzResource -ResourceType 'Microsoft.Sql/servers' ... seznam databazi  
(Find-AzResource).ResourceType | Sort-Object -Unique ... seznam vsech objektu v predplatnem  

### Automations

[Find-WhoAmI.ps1](https://github.com/azureautomation/runbooks/blob/master/Utility/ARM/Find-WhoAmI) ... zjisti jaky automatizacni account spustil Runbook a ktery runbook]]

Automatizace Azure prostredku, casovani. Vytvoreni noveho spojeni s jinym uctem popisuje [blog](https://blogs.endjin.com/2015/02/generating-and-using-a-certificate-to-authorise-azure-automation/).

Get-AzAutomationAccount ... seznam automatizacnich uctu  
[Get-AzureRmAutomationConnection](https://docs.microsoft.com/cs-cz/azure/automation/automation-connections) ...  seznam Automatizacnich spojeni (na jiny ucet v predplatnem)  
[Get-AzureRmAutomationCertificate](https://docs.microsoft.com/cs-cz/azure/automation/automation-certificates) ... seznam Automatizacnich certifikatu  
[Get-AzureAutomationCredential](https://docs.microsoft.com/cs-cz/azure/automation/automation-credentials)\\ ... Manazovane kredence automatizacniho uctu  
[Get-AzureRmAutomationVariable](https://docs.microsoft.com/cs-cz/azure/automation/automation-variables) ... seznam promennych automatizacniho uctu  
Get-AzAutomationRunbook RG AutomationAccount ... seznam runbooku  
Get-AzAutomationSchedule RG AutomationAccount ... seznam naplanovanych uloh  
Get-AzAutomationJob RG AutomationAccount -StartTime ( (Get-Date).AddHours(-1)) ... ukoly za posledni hodinu  
[New-AzureRmAutomationCertificate](https://docs.microsoft.com/en-us/azure/automation/automation-certificates) ... Vytvoreni noveho certifikatu  
Connect-AzAccount -ServicePrincipal -ApplicationId  "http://my-app" -Credential $pscredential -TenantId $tenantid ... pripoji se jako Service Principal  
[Register-AzAutomationScheduledRunbook](https://docs.microsoft.com/en-us/powershell/module/az.automation/register-azautomationscheduledrunbook?view=azps-1.2.0) -ResourceGroupName RG -AutomationAccountName AutomAccount -RunbookName cisteni_db   -ScheduleName kazdou_hodinu ... Nastaveni schedule (casovani) pro runbook v automatizacnim uctu  
Unregister-AzAutomationScheduledRunbook -ResourceGroupName RG -AutomationAccountName AutomAccount -JobScheduleId 123143 ... zruseni casovani pro runbook  
Get-AzAutomationScheduledRunbook -ResourceGroupName RG -AutomationAccountName AutomAccount ... seznam casovani runbooku ([Vice o schedulingu](https://docs.microsoft.com/en-us/azure/automation/automation-schedules))  
Get-AzAutomationJob ... seznam jobu (provedeni runbooku)  
### Certifikaty

##### Vygenerovani korenoveho certifikatu:

New-SelfSignedCertificate -Type Custom -KeySpec Signature -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
1.HashAlgorithm sha256 -KeyLength 2048 -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign

##### Vygenerovani klientskeho certifikatu:

New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
1.Subject "CN=P2SChildCert" -KeyExportPolicy Exportable -HashAlgorithm sha256 -KeyLength 2048 `
2.CertStoreLocation "Cert:\CurrentUser\My" -Signer $cert `
3.TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")

### Role

Get-AzRoleDefinition | FT Name, Description ... seznam [roli](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-assign-admin-roles)  
Get-AzRoleAssignment -ResourceGroupName pharma1 ... seznam prirazeni roli v resource grupe  pharma1  
Get-AzRoleAssignment -SignInName tomas@example.com ... seznam prirazenych roli pro cloveka  
Get-AzRoleAssignment | where {$_.RoleDefinitionName -eq "User Access Administrator" -and $_.Scope -eq "/"} ... vypis globalnich roli  
[New-AzRoleAssignment](https://docs.microsoft.com/en-us/azure/role-based-access-control/role-assignments-powershell) -SignInName tomas@a.b -RoleDefinitionName "Reader" -ResourceGroupName RG … priradi parvo Reader uzivateli na resource grupu RG  
Remove-AzRoleAssignment -SignInName tomas@aaa.bbb -RoleDefinitionName "User Access Administrator" -Scope "/" ... odebrani globalni role  

### Azure Active Directory

Get-AzADApplication ... seznam AAD aplikace  
Get-AzADServicePrincipal -SearchString "aad"... seznam AAD Service Principal s podretezcem aad ve jmene  
Get-AzureADServicePrincipal -All $true ... seznam vsech SP  
Get-AzADGroup -SearchString admins ... seznam skupin s podretezcem "admins"  
Get-AzADUser -SearchString Tomas ... seznam uzivatelu s podretezcem Tomas ve jmene nebo ID  
Get-AzADGroupMember -GroupObjectId 792dac6f-12bc-4f40-a9e0-ea58e795d0324 ... seznam clenu skupiny  
New-AzRoleAssignment -ObjectId 7777 -RoleDefinitionName "Reader" -Scope /subscriptions/00000 ... prida aplikaci ID 7777 nebo skupine ID 7777 roli Reader v subscription 0000  
New-AzRoleAssignment -SignInName tomas@example.com -RoleDefinitionName "Virtual Machine Contributor" -ResourceGroupName pharma1 -ResourceName TomasVM ... prida prava uzivateli  
Remove-AzRoleAssignment -SignInName tomas@example.com -RoleDefinitionName "Virtual Machine Contributor" -ResourceGroupName pharma1 ... odebere roli  

##### Nastaveni nove aplikace a uctu Service Principal

Add-Type -Assembly System.Web … Iniciuje modul na generovani hesla  
$password = [System.Web.Security.Membership]::GeneratePassword(16,3) ### vyganeruje heslo  
$securePassword = ConvertTo-SecureString -Force -AsPlainText -String $password … vytvori zakodovany retezec  
$ap = new-AzADApplication -DisplayName "AAD:perf-monitoring-stgasia" -IdentifierUris "http://localhost/AADperf-minitoring-stgasia" -Password $securePassword ### vytvori novou aplikaci  
$sp=[New-AzADServicePrincipal](https://docs.microsoft.com/en-us/powershell/azure/create-azure-service-principal-azureps?view=Azps-6.11.0) -ApplicationId $ap.ApplicationId -Password $securePassword ### vytvori noveho Service Principal (SP)  
New-AzRoleAssignment -ObjectId $sp.Id -RoleDefinitionName "Reader" -ResourceGroupName RG ### Priradi roli na resource grupu pro SP  
$s = Get-AzSubscription -SubscriptionId a-b-c-d ### ziska tenantID z predplatneho  
$mycreds = New-Object System.Management.Automation.PSCredential ($ap.ApplicationId, $securePassword) ### vytvori promennou s kredencemi  
Connect-AzAccount -ServicePrincipal -Credential $mycreds -TenantId $s.TenantI  ### pripoji se jako service principal  

##### Nastaveni nove role a prav

[Nastaveni nove role](https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles-powershell)
  $role = Get-AzRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
  Set-AzRoleDefinition -Role $role
$svcprincipal.AppRoles | FT ID, DisplayName ... ukaze aplikacni prava  
$svcprincipal.Oauth2Permissions | FT ID, UserConsentDisplayName ... ukaze delegovana prava  
$reqGraph = New-Object -TypeName "Microsoft.Open.AzureAD.Model.RequiredResourceAccess" ... Objekt reprezentujici pristup k Microsoft Graph  
[pekny clanek o nastaveni prav](http://blog.octavie.nl/index.php/2017/09/19/create-azure-ad-app-registration-with-powershell-part-2)
### Storage account

$storageAccount = Get-AzStorageAccount -ResourceGroupName RG -Name SA … najde storage account  
Install-Module [AzStorageTable](https://docs.microsoft.com/en-us/azure/storage/tables/table-storage-how-to-use-powershell) … Nainstaluje modul pro Storage table  
Install-Module [AzStorageTable.TravisEz13](https://www.powershellgallery.com/packages/AzStorageTable.TravisEz13/1.0.3) ... to same pro AZ. Ostatni moduly nejedou  
$storageTable = Get-AzureStorageTable –Name TABULKA –Context $storageAccount.Context … Vybere tabulku  
Get-AzureStorageTableRowAll -table $storageTable … vsechny zaznamy z tabulky  
Get-AzureStorageTableRowByColumnName -table $storageTable -columnName "jmeno" -value "Tomas" -operator Equal … zaznamy kde hodnota sloupce "jmeno" je "Tomas"  
Get-AzureStorageTableRowByCustomFilter -table $storageTable -customFilter "(roky eq 1)"… zaznamy kde hodnota sloupce "roky" je 1  
$ctx=New-AzureStorageContext -StorageAccountName STORAGEACCOUNT -StorageAccountKey 'KEY'  
Set-AzureStorageBlobContent -Container BLOBKONTEJNER -Context $ctx -Blob CESTA_V_BLOBU -File SOUBOR ... nahrani souboru na Blob  
### Metriky, statistiky VM, Logy a Alerty

Get-AzActionGroup ... seznam skupin akci  
Get-AzActivityLogAlert ... seznam log alert resources  
Get-AzAlertHistory ... historie alertu  
Get-AzAlertRule ... seznam alertovych pravidel  
Get-AzAutoscaleHistory ... historie automatickeho skalovani  
Get-AzAutoscaleSetting ... Nastaveni automatickeho skalovani  
Get-AzDiagnosticSetting ... ziska logovaci kategorie a casovani  
Get-AzLog ... zobrazeni logu  
Get-AzLogProfile ... logovaci profily  
Get-AzMetricDefinition –ResourceId (Get-Azvm RG VM).Id ... [seznam metrik](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) pro dany resource  
Get-AzMetric -ResourceId (Get-AzVM RG VM).Id -DetailedOutput -StartTime (get-date).AddMinutes(-5) -MetricName "Network In" | Select-Object -expand data ... Vypis metriky Network In za poslednich 5 minut  
Get-AzDiagnosticSetting … zobrazi nastaveni Diagnostiky (boot diagnostika, logy ...)  
Set-AzDiagnosticSetting -ResourceId x/y/z … zobrazi nastaveni Diagnostiky (boot diagnostika, ...) pro x/y/z VM  
$actionEmail = New-AzAlertRuleEmail -CustomEmail me@contoso.com … vytvoreni noveho emailu pro alertovaci pravidla  
Add-AzLogAlertRule -Name StartAlert -Location 'East Asia' -ResourceGroup myRG -OperationName Microsoft.Compute/virtualMachines/start/action -TargetResourceGroup myRG -Actions $actionEmail … nastaveni alertu pri startu VM  
Add-AzMetricAlertRule -Name "Cpu_pres_90" -Location westus -ResourceGroup RG
1.Description "CPU > 90" -SendToServiceOwners -RuleType Metric -Operator GreaterThan -Threshold 90
2.WindowSize 00:05:00 -ResourceId '/sub/a/resGr/RG/prov/aaa/VM' -MetricName '\Processor(_Total)\% Processor Time' -TimeAggregationOperator Average …  … vytvoreni alertu na CPU pres 90%  

#### =Tagy

Get-AzVm | Where-Object { $_.tags['tagkey'] -eq 'aaa' } ... filtrace VM podle tagu  
Get-AzTag ... seznam objekty s danym tag name  
$VM-AzVm -Name Server -ResourceGroupName RG  
$VM.Tags.Add("jmeno", "hodnota")  
$VM.Tags['jmeno'] = "jina hodnota"  
Set-AzResource -Tag $VM.Tags -ResourceId $VM.Id -Force .. ulozeni  

### Analytic Log Workspace

Get-AzOperationalInsightsSavedSearch ... Vylistovani/informace o ulozenych hledanich (log dotazech)  
Set-AzOperationalInsightsSavedSearch ... vytvoreni/uprava ulozenych dotazu - nepodporuje nove Kusto query. Podpora Kusto query je v API verzi 2017-03-10-preview  

### Webove sluzby - App service

[skripty of Octavie van Haaften](http://blog.octavie.nl/index.php/assets) pro manipulaci s Webovymi sluzbami  
azverify.subdomena.domena.naddomena ... DNS zaznam, ktery umozni vytvorit Custom Domain pro App Service bez outage  

### CDN sluzby

cdnverify.subdomena.domena.naddomena ... DNS zaznam, ktery umozni vytvorit Custom Domain pro CDN endpoint  

### Managed Identity

Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -Headers @{Metadata="true"} ... ziskani tokenu pro System assigned identity  
$content=Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02
1.01&client_id=aaaabbbb-cccc-dddd-eeee-111122223333&resource=https%3A%2F%2Fmanagement.azure.com%2F' -Headers @{Metadata="
true"} ... ziskani tokenu pro jinou identitu - user assigned identity  
$access_token = $content.access_token ... ziskani bareer kodu  
Invoke-WebRequest -Uri 'https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.Compute/virtualMachines/<VM-NAME>?api-version=2017-12-01' -Method GET -ContentType "application/json" -Headers @{ Authorization ="Bearer $access_token"} ... pouziti bareer kodu  

response=$(curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true -s)  
access_token=$(echo $response | python -c 'import sys, json; print (json.load(sys.stdin)["access_token"])') ... curl priklad  

### Vault

https://contoso-vault2.vault.azure.net/ ... URL pro Vault  
$secretvalue = ConvertTo-SecureString 'hVFkk965BuUv' -AsPlainText -Force  
$secret = Set-AzKeyVaultSecret -VaultName 'Contoso-Vault2' -Name 'ExamplePassword' -SecretValue $secretvalue  
(Get-AzKeyVaultSecret -vaultName "Contoso-Vault2" -name "ExamplePassword").SecretValueText  

### Role

$scope = (Get-AzRoleAssignment -RoleDefinitionName 'Support Request Contributor (Custom)').Scope .... najde role Supprot Request Contributor  
Remove-AzRoleAssignment -ObjectId '[object_ID]' -RoleDefinitionName 'Support Request Contributor (Custom)' -Scope $scope ... odstrani role  
Remove-AzRoleDefinition -Name 'Support Request Contributor (Custom)' -Force  

### Scaling Sets

[https://raw.githubusercontent.com/MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator/master/Allfiles/Labs/08/az104-08-configure_VMSS_disks.ps1](https://raw.githubusercontent.com/MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator/master/Allfiles/Labs/08/az104-08-configure_VMSS_disks.ps1) ... pridani VM rozsireni na pouziti datovych disku  

### Virtual Network

##### P2S spojeni

apt-get install -y strongswan libcharon-extra-plugins libcharon-standard-plugins libstrongswan-standard-plugins libstrongswan-extra-plugins  
https://docs.microsoft.com/en-us/azure/storage/files/storage-files-configure-p2s-vpn-linux
