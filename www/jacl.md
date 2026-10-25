# WebSphere Application Server - JACL

Seznam aplikaci:

```
$AdminApp list
```

Status nodeagenta:

```
set nodeagent_status
[$AdminControl queryNames cell=myCell,node=myNode,server=nodeagent,*]

if {[llength $nodeagent_status] != 0}
{
puts "nodeagent is running"
}
else
puts "nodeagent is not running, all application status is not available" 
```

Status aplikacniho serveru:

```
set server_status
[$AdminControl queryNames cell=myCell,node=myNode, server=myServer,*]
if {[llength $server_status] != 0}
{
puts "server $server_status is running"
}
else
puts "server $server_status is not running, all application status is not available" 
```

Status aplikace (jede/nejede):

```
set myRunningApp [$AdminControl queryNames type,Application,name=myApp,*]
if {[llength $myRunningApp] != 0}
{
puts "App myApp is started"
}
else
puts "App myApp is not running"
```

Restart aplikace:

```
set appManager [$AdminControl querynames cell=myCell,node=myNode, type=ApplicationManager,process=myServer,*]

AdminControl invoke $appManager stopApplication myApp

AdminControl invoke $appManager startApplication myApp 
```

Stop vsech aplikaci:

```
foreach app $apps {set appName [$AdminControl getAttribute $app name];
 $AdminControl invoke $appManager stopApplication $appName}
```
