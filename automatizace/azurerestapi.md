# azurerestapi

## API

[Microsoft REST API catalog](https://docs.microsoft.com/en-us/rest/api/) - Azure REST API, VSTS, atd.  

## Azure Instance Metadata service REST API

[https://docs.microsoft.com/en-us/azure/virtual-machines/windows/instance-metadata-service](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/instance-metadata-service)

## Azure REST API

[jak pouzivat Azure Rest API](https://blog.jongallant.com/2017/11/azure-rest-apis-postman/) pomoci Postman za 2 minuty  
[Mala ukazka REST API](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough) - metriky k virtualnim masinam  
[Seznam metrik](https://docs.microsoft.com/en-us/rest/api/monitor/metrics/list)  
[generovani uplne vlastnich custom metrik](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/metrics-custom-overview), vcetne popisu API  
[https://dev.loganalytics.io/documentation/Using-the-API/RequestFormat](https://dev.loganalytics.io/documentation/Using-the-API/RequestFormat) ... https://api.loganalytics.io/ - API k Log Analytics s novymi Kusto query prikazy  

## Storage API

[storage api by cUrl](https://stackoverflow.com/questions/51072445/azure-storage-table-api-rest-with-curl)

## REST API & PowerShell

Connect-AzAccount  
$context = Get-AzSubscription -SubscriptionName Predplatne | Set-AzContext  
$cache = $context.TokenCache  
$cacheItem = $cache.ReadItems()  
$token = ($cacheItem | where { $_.Resource -eq "https://management.core.windows.net/" }).accessToken  
$Headers = @{}  
$Headers.Add("Authorization","Bearer  $($token)")  
$ResourceGroupApiUri = "https://management.azure.com/subscriptions/$($context.Subscription)/resourcegroups?api-version=2017-05-10"  
$ResourceGroups = Invoke-RestMethod -Method Get -Uri $ResourceGroupApiUri -Headers $Headers  
Invoke-RestMethod -Method Put -ContentType "application/json" -Headers $Headers -Uri $URL -Body $json_ss

## REST API & Bash

az login  
TOKEN=$(az account get-access-token | jq .accessToken | sed -e 's/"//g') ... tady ziskame bareer kod  
curl --location -H "Content-Type: application/json" -H 'Authorization: Bearer $TOKEN'  -X GET 'https://management.azure.com/subscriptions/YYY/providers/Microsoft.Compute/skus?api-version=2019-04-01'  

====SavedSearches 2017-03-03 - update/create====

```
Invoke-RestMethod -Method Put -Uri 'https://management.azure.com/subscriptions/aaaa-bbbbb-ccccc/resourcegroups/XXXX/providers/Microsoft.OperationalInsights/workspaces/YYYYYY/savedSearches/bbb?api-version=2017-03-03-preview' -Headers $Headers -Body '{"etag":"*","properties":{"category":"Updates","displayName":"ccc","query":"Heartbeat | where Computer in~  (\"v4uatweadm0
1.ifs.ori.local\" ) | distinct Computer","functionAlias":""}}' -ContentType "application/json"
```

Pro create je mozno dat etag prazdne, pro update je potreba dat "*"  
[API 2015-03-10 popis](https://docs.microsoft.com/en-us/azure/azure-monitor/insights/solutions-resources-searches-alerts)  
[update notes pr API 2017-03-15-preview](https://docs.microsoft.com/en-us/azure/azure-monitor/insights/solutions-resources-searches-alerts) - nove Kusto query
