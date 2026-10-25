### Query Language

Log Analytics query language (dotazovaci jazyk Log Analytiky) pouziva Kusto query - read-only SQL podobne dotazy na analyzudat.

[Skoleni na KQL](https://www.pluralsight.com/courses/kusto-query-language-kql-from-scratch)  
[MS Demo na KQL v Log Analytics](http://aka.ms/LADemo)  
[MS Demo an AI Analytics](aka.ms/AIAnalyticsDemo)  
[MS Demo na KQL v Windows Defender Advanced Thread Protection](aka.ms/WinDefATP)  
### Logy

[Log analytics query language](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-queries)

Event | where EventLevelName == "Error" | summarize count() by Source, Computer  

search in (Updates) "error" .. hleda v tabulce Updates zaznamy, kde je retezec "error"  
#####

Event logy ====

```
AzureActivity
| where ResourceProvider == "Microsoft.Automation"
// Oql: Type=AzureActivity ResourceProvider == "Microsoft.Automation" // Settings: {NAV: True} // WorkspaceId: {00000000-0000-0000-0000-000000000000} // Version: 0.1.91
| where OperationName == "Create or Update an Azure Automation schedule asset"
| where Resource  contains "STG"  
```

====Application Insight====

```
requests |
where resultCode startswith "40" |
where timestamp >= datetime(2018-12-06T00:00Z) |
where cloud_RoleInstance contains "webasia1" |
where name contains "GET aplikace/Index" |
summarize count(itemCount) by name |
order by count_itemCount  
```

```
requests
| extend diagnosticsParsedUrl = parseurl(url)
| where name contains "OPTIONS" 
| where resultCode == "500" 
| where timestamp > ago(6d)
| where diagnosticsParsedUrl['Path'] == "/system/ajax/"
| extend d=parse_json(customDimensions)
| extend agent=tostring(d["ClientApplication"]) 
| distinct agent, name, timestamp | summarize count() by agent 
```

tostring() je potreba pouzit pri expandovani objektu, jinak hlaska `Please use an explicit cast as grouping by a 'dynamic' type is not supported.`
