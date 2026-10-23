# Azure Runbook

====Automatizacni spojeni====

```
        $serviceName = 'MyCloudService'
        $cert = Get-AutomationCertificate -Name 'MyCertificate'
        $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
        –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
        Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert
```
