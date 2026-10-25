# zabbix

Nastaveni metriky pomoci Zabbix trapu (data prichazi z klientu jako webhook pomoci zabbix_sender)  
zabbix_sender -z <server IP address> -p 10051 -s "New host" -k trap -o "test value" ... posilani dat pro zabbix_trap metriku  

### Zabbix API

[Zabbix API](https://www.zabbix.com/documentation/3.0/manual/api)  
[Zabbix API priklad v Powershellu](https://gist.github.com/Sam-Martin/43c78a9efc4916f35971e21843ffd37b)

```
if(!$credential){
    $credential = Get-Credential
}
$baseurl = 'http://zabbix.server'
$params = @{
    body =  @{
        "jsonrpc"= "2.0"
        "method"= "user.login"
        "params"= @{
            "user"= $credential.UserName
            "password"= $credential.GetNetworkCredential().Password
        }
        "id"= 1
        "auth"= $null
    } | ConvertTo-Json
    uri = "$baseurl/api_jsonrpc.php"
    headers = @{"Content-Type" = "application/json"}
    method = "Post"
}

$result = Invoke-WebRequest @params

$auth = ($result.Content | ConvertFrom-Json).result

$params.body = @{
    "jsonrpc"= "2.0"
    "method"= "host.get"
    "params"= @{
        output = "extend"
		selectFunctions = "extend"
		selectLastEvent = "extend"
		selectGroups = "extend"
		selectHosts = "extend"
    }
    auth = $auth
    id = 2
} | ConvertTo-Json

$result = Invoke-WebRequest @params
$result = $result.Content | ConvertFrom-Json

$filtred_nodes = ($result.Content | ConvertFrom-Json).result | where { $_.name -like "SERVERPATTERN*"} | select hostid,name

foreach ($filtred_node in $filtred_nodes) {

    $params.body = @{
         "jsonrpc"= "2.0"
         "method"= "item.get"
         "params"= @{
             output = "extend"
     hostids = "$($filtred_node.hostid)"
         }
         auth = $auth
         id = 2
     } | ConvertTo-Json

     $result2 = Invoke-WebRequest @params

    $status = ($result2.Content | ConvertFrom-Json).result | Where-Object { $_.name -like "*ITEMPATTERN*"}

    Write-Output "$($filtred_node.name) $($status.status)"

    if ($status.status -eq 0) {

        $params.body = @{
                      "jsonrpc"= "2.0"
                      "method"= "item.update"
                      "params"= @{
                          itemid = "$($status.itemid)"
                  status = "1"
                      }
                      auth = $auth
                      id = 2
                  } | ConvertTo-Json
            
                  $result2 = Invoke-WebRequest @params
                  Write-Output "Item disabled"
    }
}
```
