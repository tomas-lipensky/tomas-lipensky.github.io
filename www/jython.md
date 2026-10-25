# [WebSphere Application Server](was.html) - jython

### Obsah

<dl>
<dt>[Externi odkazy](#odkazy)</dt>
<dt>[Interni odkazy](#interni)</dt>
<dt>[wsadmin](#wasadmin)</dt>
<dt>Moduly:</dt>
<dd>[AdminControl](#AdminControl)</dd>
<dd>[AdminConfig](#AdminConfig)</dd>
<dd>[AdminApp](#AdminApp)</dd>
<dd>[AdminTask](#AdminTask)</dd>
<dd>[Help](#Help)</dd>
<dt>[wsadmin: priklady administrace](#priklady)</dt>
</dl>

### Externi odkazy

$WAS/web/mbeanDocs/index.html ... Popisy vsech MBean typu  

[WebSphere Application Server Administration Using Jython](http://my.safaribooksonline.com/book/web-development/websphere/9780137043699) - kniha na Safari Books Online  

### Interni odkazy

[WAS](was.html)  
[Python](../dev/pzthon.html)  
[JACL](jacl.html)  

### wsadmin

wsadmin pouziva k administraci 5 zakladnich commandu: AdminControl, AdminConfig, AdminApp, AdminTask a Help  

##### AdminControl:

AdminControl.compleeObjectName('type=DeploymentManager,node=NODE1') ... vypise prvni obejkt, ktery odpovida zadani  
AdminControl.getCell() ... vrati jmeno cely  
AdminControl.getNode() ... jmeno node  
AdminControl.queryNames('*') ... vypise vsechny objektove jmena MBeanu jedoucich v MBean serveru  
AdminControl.queryNames('WebSphere:type=Server,node=NODE1,*') ... provede filtraci. "WebSphere:" je nepovinny udaj  
AdminControl.queryNames('type=ApplicationManager,cell='+AdminControl.getCell()+',*') ... dalsi priklad filtrace  
print AdminControl.invoke(MBean,'getVersionsForAllProducts') ... provede operaci (akci) getVersionsForAllProducts a vypise vystup  
AdminControl.invoke(AdminControl.queryName('type=ApplicationManager,node=NODE,*'), 'stopApplication', APPNAME) ... zastavi aplikaci APPNAME  
AdminControl.invoke(AdminControl.completeObjectName('type=NodeSync,node=SICNODE01,*'),'sync') ... synchronizace nodu  
AdminControl.getAttribute(AdminControl.completeObjectName('type=Server,node=NODE1,*'),'pid') ... precte hodnotu atributu pid v MBeanu, ktery jsme vyhledali completeObjectName  
Graficky tool: [MBeanInspector](http://www.alphaworks.ibm.com/tech/mbeaninspector)(MBI) se doporucuje pouzivat z Admin konzoly na vsechny JMX Mbeany. Nedodava se k WAS6, funguje ten z WAS5  
AdminControl.setAttribute() ... nastavovani atributu  
AdminControl.stopServer(SERVER_NAME, NODE_NAME) ... zastavi server na node  

##### AdminConfig:

print AdminConfig.types() ... seznam vsech TYPu objektu (konfiguracnich typu)  
print AdminConfig.attributes('ApplicationServer') ... seznam a popis atributu u jednotlivych polozek (z AdminConfig.types)  
print AdminConfig.parents('ApplicationServer') ... Vypise otcovsky konfiguracni typ pro konfiguracni typ ApplicationServer  
AdminConfig.getid('/Node:AS03TDMGR01/Server:dmgr/') ... vrati ID (Konfiguracni jmeno) pro objekt, (format: "viditelne jmeno(konfiguracni soubor a polozka)"). Lomitka / oddeluji jednotlive konfiguracni typy od druhych, = oddeluje typ od hodnoty  
AdminConfig.getid('/JDBCProvider:AAA/') ... vrati ID vsech nalezenych objektu (jako AdminConfig.list, ale s vyhledavanim podle klice)  
AdminConfig.list(TYP) ... seznam objektu daneho typu (seznam vsech TYPu: AdminConfig.types)  
print AdminConfig.list('ApplicationServer') ... vrati seznam ID objektu konfiguracniho typu ApplicationServer - seznam Aplikacnich serveru  
print AdminConfig.list('JDBCProvider') ... seznam JDBC poskytovatelu - jejich ID  
print AdminConfig.list('Cell') ... Ukaze ID cely  
print AdminConfig.list('ClusterServer') ... Ukaze ID cely  
print AdminConfig.list('Node') ... Ukaze ID nodu  
print AdminConfig.list('VirtualHost') ... seznam virtual hostu  
print AdminConfig.list('WebModuleDeployment') ... seznam web modulu  
print AdminConfig.defaults('ApplicationServer') ... Vypise vychozi hodnoty pro danny konfiguracni typ  
print AdminConfig.show('ODGEMB/nodes/AS03TDMGR01/servedmgr(cells/PREPRrs/dmgr|server.xml#Server_1)') ... Ukaze nastaveni (atributu) parametru daneho objektu (lze jej ziskat pomovi AdminConfig.getid)  
print AdminConfig.showall('dmgr(cells/PREPRODGEMB/nodes/AS03TDMGR01/servers/dmgr|server.xml#Server_1)') ... Ukaze nastaveni (atributu) parametru daneho objektu (ID) (lze jej ziskat pomovi AdminConfig.getid, nebo AdminConfig.list)  
print AdminConfig.showAttribute(AdminConfig.getid('/Node:AS03TDMGR01/Server:dmgr/')), 'name') ... Ukaze pouze parametr (atribut) name daneho objektu  
print AdminConfig.showAttribute(ID, 'name') ... Ukaze parametr name u ID  
AdminConfig.modify() ... modifikace prarametru ( [ ['promenna1', 'hodnota1], ['promenna2', 'hodnota2']]  
AdminConfig.modify(gAdminConfig.getid('/JDBCProvider:AAA/'), ['description', "Popis"]('description', "Popis")) ... priklad zmeny popisu, prepinace u objektu jako 'description' muzeve videt pomoci AdminConfig.show  
AdminConfig.create('VirtualHost',CELL_OBJECT,['name','vhost_name']('name','vhost_name'))) ... vytvoreni parametru  
AdminConfig.remove('SERVER_CONFIG_ID') ... odstraneni aplikacnihop serveru  
AdminConfig.save() ... ukozi zmeny udelane ve wsadminu  
AdminConfig.reset() ... zrusi zmeny udelane ve wsadminu  

##### AdminApp:

print AdminApp.help() ... seznam funkci AdminApp  
AdminApp.isAppReady("JMENO_APLIKACE") ... true, kdyz aplikace je ready (je ji mozne spustit)  
print AdminApp.list() ... vylistuje nainstalovane aplikace  
print AdminApp.listModules() ... vylistuje nainstalovane moduly aplikaci  
print AdminApp.listModules('TradeApplication') ... Vylistuje moduly jedne aplikace  
print AdminApp.options('WS_BIEN') ... ukaze prepinace aplikace WS_BIEN  
AdminApp.installInteractive('C:/PROGRA~1/IBM/WebSphere/AppServer/installableApps/ivtApp.ear') ... instalace aplikace  
AdminApp.install('c:/tmp/appl.ear', ["server", "serv2"], ["-appname", "IVT app"]("server", "serv2"], ["-appname", "IVT app") ') ... instalace aplikace, pote AdminConfig.sava  
AdminApp.install('c:/tmp/appl.ear', ['server', 'serv2', '-node', 'NODE', '-cluster', 'CLUSTER', '-appname', 'IVT app') ... instalace aplikace  
AdminApp.install('/opt/delivery/BLMONITOR/blm1.1-rc6.ear', '[ -nopreCompileJSPs -distributeApp -nouseMetaDataFromBinary -nodeployejb -appname BLMONITOR_1.1-rc6 -createMBeansForResources -noreloadEnabled -nodeployws -validateinstall warn -noprocessEmbeddedConfig -filepermission .*\.dll=755#.*\.so=755#.*\.a=755#.*\.sl=755 -noallowDispatchRemoteInclude -noallowServiceRemoteInclude -MapResRefToEJB [ "BLM Web Application" "" blmwapp.war,WEB-INF/web.xml jdbc/netdb javax.sql.DataSource jdbc/netdb10 "" "" ]( "BLM Web Application" "" blmwapp.war,WEB-INF/web.xml jdbc/netdb javax.sql.DataSource jdbc/netdb10 "" "" ) -MapModulesToServers [ "BLM Web Application" blmwapp.war,WEB-INF/web.xml WebSphere:cell=SICCELL,node=SICNODE01,server=as_blmonitor+WebSphere:cell=SICCELL,node=SICNODE01,server=ihs_sic ]( "BLM Web Application" blmwapp.war,WEB-INF/web.xml WebSphere/cell=SICCELL,node=SICNODE01,server=as_blmonitor+WebSphere/cell=SICCELL,node=SICNODE01,server=ihs_sic ) -MapWebModToVH [ "BLM Web Application" blmwapp.war,WEB-INF/web.xml blmonitor_vh ]( "BLM Web Application" blmwapp.war,WEB-INF/web.xml blmonitor_vh )]' )  
AdminApp.install('c:/tmp/appl.ear', [ -nopreCompileJSPs -distributeApp -nodeployejb -appname ' + newAppName + ' -createMBeansForResources -noreloadEnabled -nodeployws -validateinstall off -noprocessEmbeddedConfig -MapWebModToVH [.* .*.war,.* ' + VirtualHostName + ' ](.* .*.war,.* ' + VirtualHostName + ' ) -MapModulesToServers [.* .*.war,.* ' + SERVERS_MAPPING + ' ](.* .*.war,.* ' + SERVERS_MAPPING + ' ) -MapResRefToEJB [.* "" .*.war,.* ' + JDBC_Resource_Ref + ' javax.sql.DataSource ' + JDBC_JNDI_Name + ' ](.* "" .*.war,.* ' + JDBC_Resource_Ref + ' javax.sql.DataSource ' + JDBC_JNDI_Name + ' )] )  
print AdminApp.options('LOKACE_EAR') ... ukaze prepinace aplikace v lokaci  
AdminApp.uninstallinstall('IVT App') ... odinstalace aplikace  
AdminApp.enitInteractive('IVM app') ... interaktivni editace aplikace  
AdminApp.enit("IVT App", ["MapModulesToServers", ["IVT Application", "ivt_appr.war,WEB-INF/web.xml", "WebSphere:cell=CEL,node=NODE,server=SERVER,cluster=CLUSTER]("IVT Application", "ivt_appr.war,WEB-INF/web.xml", "WebSphere/cell=CEL,node=NODE,server=SERVER,cluster=CLUSTER)] ) ... editace app resveru, pote AdminConfig.save  

##### AdminTask

print AdminTask.help('-commandGroups') ... Seznam vsech skupin administracnich ukolu  
print AdminTaks.help('ClusterConfigCommands') ... Informace o skupine administracnich ukolu ClusterConfigCommands  
print AdminTask.help('createCluster') ... informace o administrativnim ukolu print createCluster  
print AdminTask.help('-commands') ... seznam vsech prikazu a jejich strucny popis  
AdminTask.createCluster('-interactive') ... Interaktivni vyplnovani parametru v ukolu createCluster  
AdminTask.createApplicationServer('-interactive') ... Interaktivni vytvoreni aplikacniho serveru  
AdminTask.deleteServer('-interactive') ... Interaktivni smazani aplikacniho serveru  
AdminTask.listNodes() ... seznam Nodu  
AdminTask.listServerTypes() ... seznam typu serveru  
AdminTask.showServerInfo(ID_applikacniho_serveru) ... ukaze informace o appl. serveru  

##### Help

print Help.AdminControl() ... vypise prikazy v baliku AdminControl  
print Help.AdminControl('compleeObjectName') .... popise prikaz AdminControl.completeObjectName  
print Help.attributes(AdminControl.completeObjectName('type=Server,node=NODE1,*')) ... vypise atributy daneho MBeanu  

### shell: uzitecne priklady

ps -ef | grep -v grep | grep WebS | awk '{ print $(NF-2),$(NF-1),$(NF) }' | sort | uniq  
ps -ef | grep httpd | grep -v grep | awk '{ print $9,$10,$11,$12,$13,$14 }' | sort | uniq  
LANG=en_US

### wsadmin: priklady administrace

Seznam aplikaci, jiny zpusob:

```
print AdminControl.queryNames('type=Application,*')
```


Seznam aplikaci a modulu:\\

```
for ap in AdminApp.list().split():
        for mo in AdminApp.listModules(ap).split():
                print ap + " : " + mo
```


Seznam aplikaci a jejich prirazeni:\\

```
for ap in AdminApp.list().split():
        for aaa in AdminApp.view(ap,['-MapWebModToVH','-MapModulesToServers']).split('\n'):
                if aaa.rfind('Serveur:') > -1:
                        print ap + " - " + aaa[10:-1]
```


Seznam aplikaci a prirazeni k serverum:\\

```
for ap in AdminApp.list().split():
        for mo in AdminApp.listModules(ap).split():
                for aaa in AdminApp.view(mo,['-MapWebModToVH','-MapModulesToServers']).split('\n'):
                        if aaa.rfind('Serveur:') > -1:
                                print mo + " - " + aaa[10:-1]
```


Zastaveni Deployment Manazera:\\

```
AdminControl.stopServer('dmgr','NODE')
```

nebo\\

```
AdminControl.invoke(AdminControl.completeObjectName('type=Server,processType=DeploymentManager,*'),'stop')
```


Zastaveni Node agenta:\\

```
AdminControl.stopServer('nodeagent','NODE')
```

nebo\\

```
AdminControl.invoke(AdminControl.completeObjectName('type=Server,node=NODE,name=nodeagent,*'),'stop')
```


Start Aplikacniho serveru:\\

```
AdminControl.startServer('server2','NODE')
```

nebo\\

```
AdminControl.invoke(AdminControl.completeObjectName('type=Server,node=NODE,name=NODE,*'),'launchProcess', 'server2')
```

nebo\\

```
AdminControl.invoke(AdminControl.queryNames('*:*,node=NODE',launchProcess', 'server2')
```


Zastaveni Aplikacniho serveru:\\

```
AdminControl.stopServer('server2','NODE')
```

zastaveni vsech Ap. serveru na jednm node: [stopApsOnNode.py](stopApsOnNode.py)  

Reset DMGR k replikaci manualnich zmen v XML na vsechny nody:\\

```
wsadmin DMGR> set config [$AdminControl queryNames *:*,type=ConfigRepository,process=dmgr]
wsadmin DMGR> $AdminControl invoke $config refreshRepositoryEpoch
```


Reset NODE k prepsani manualnich zmen v XML na NODE konfiguraci z DMGRy:\\

```
wsadmin NODE> set config [$AdminControl queryNames *:*,type=ConfigRepository,process=nodeagent]
wsadmin NODE> $AdminControl invoke $config refreshRepositoryEpoch
```

wsadmin -f [timeout.py](timeout.py) ... nastaveni timeout v Administrativni konzoli  
wsadmin -f [showMBeans.py](showMBeans.py) ... vypise bezici MBeans  

Seznam aplikaci, ktere bezi:\\

```
AdminControl.queryNames('type=Application, node=NODE,*')
```


Status vsech aplikaci: [StatusOfApps.py](StatusOfApps.py)  

Start zastavenych aplikaci:

```
AdminControl.invoke(AdminControl.queryNames('type=AplicationManager,node=NODE,process=server1,*'),'startApplication','APLIKACE')
```


Stop aplikace:

```
AdminApp.list() ... najdi aplikaci
print AdminControl.queryNames('type=Application,name=APLIKACE,*') ... najdi aplikacni server
AdminControl.invoke(AdminControl.queryNames('type=ApplicationManager,process=SERVER,*),'stopApplication','APLIKACE')
```


Start clusteru:\\

```
print AdminControl.queryNames('type=Cluster,*')
AdminControl.invoke(AdminControl.completeObjectName('type=Cluster,name=CLUSTER1,*'),'start')
```


Zastaveni clusteru:\\

```
print AdminControl.queryNames('type=Cluster,*')
AdminControl.invoke(AdminControl.completeObjectName('type=Cluster,name=CLUSTER1,*'),'stop')
```


Vygenerovani konfigurace Web-pluginu:\\

```
pluginGen = AdminControl.completeObjectName('type=PluginCfgGenerator,*')
AdminControl.invoke(pluginGen,'generate',"C:/PROGRA~1/IBM/WebSphere/AppServer/profiles/Dmgr01/config CELL CELLMANAGER dmgr plugin-cfg.xml")
```


Zapnuti logovani WebSphere komponent:\\

```
print AdminControl.queryNames('type=TraceService,*')
ts=AdminControl.completeObjectName('type=TraceService,process=serve1,*')
AdminControl.setAttribute(ts,'traceSpecification','com.ibm.ejs.*=all')
```


Vypnuti zapinani aplikace pri startu aplikacniho serveru: [DisableAppl.py](DisableAppl.py)  

listovani Virtual Hostu:\\

```
wsadmin>print AdminConfig.list('VirtualHost')
admin_host(cells/TestCell|virtualhosts.xml#VirtualHost_2)
default_host(cells/TestCell|virtualhosts.xml#VirtualHost_1)
wsadmin>print AdminConfig.show('admin_host(cells/TestCell|virtualhosts.xml#VirtualHost_2)')
wsadmin>print AdminConfig.show('admin_host(cells/TestCell|virtualhosts.xml#VirtualHost_2)')
[aliases [(cells/TestCell|virtualhosts.xml#HostAlias_4) (cells/TestCell|virtualhosts.xml#HostAlias_5)]]
[mimeTypes [(cells/TestCell|virtualhosts.xml#MimeEntry_101) (cells/TestCell|virtualhosts.xml#MimeEntry_102) (cells/TestCell|virtualhosts.xml#MimeEntry_103) (cells/TestCell|virtualhosts.xml#MimeEntry_104) (cells/TestCell|virtualhosts.xml#MimeEntry_105) (cells/TestCell|virtualhosts.xml#MimeEntry_106) (cells/TestCell|virtualhosts.xml#MimeEntry_107) (cells/TestCell|virtualhosts.xml#MimeEntry_108) ....
wsadmin>print AdminConfig.show('admin_host(cells/TestCell|virtualhosts.xml#HostAlias_4)')
[hostname *]
[port 9060]
wsadmin>print AdminConfig.show('admin_host(cells/TestCell|virtualhosts.xml#HostAlias_5)')
[hostname *]
[port 9043]
```


pocet spojeni do DB, vycisteni fronty spojeni:\\

```
ds=AdminControl.queryNames('*:type=DataSource,process=as_espacejobs_1,name=calbdsnp033_refonte,*')
print AdminControl.invoke(ds, 'showPoolContents')
print AdminControl.invoke(ds, "showAllPoolContents")&#8203;
AdminControl.invoke(ds, "purg&#8203;ePoolContents", "immediate")&#8203;
```


Start vsech Listeneru na messaging\\

```
for lPort in AdminControl.queryNames('type=ListenerPort,*').split():
  state = AdminControl.getAttribute(lPort, 'started')
  print(lPort, "    ", state)
  if state == 'false':
    AdminControl.invoke(lPort, 'start')
```


programek od Pavla k listovani url k aplikacim: [list_app_mod_vh_alias.jy](list_app_mod_vh_alias.jy)
