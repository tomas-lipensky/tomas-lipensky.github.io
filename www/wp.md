---
title: WebSphere Portal
---

## Externi Odkazy:

[IBM Support Assistant Lite](https://www-304.ibm.com/support/docview.wss?rs=688&uid=swg24008662) w WebSphere Portal  

## wpscript

wp_root/bin/wpscript.sh -port 8882 ... interaktivni mod  
wp_root/bin/wpscript.sh -port 8882 -conntype SOAP ... interaktivni mod, typ spojeni SOAP (RMI, NONE)  
wp_root/bin/wpscript.sh -port 8882 -f script.jacl portaladmin adminpwd ... spusteni JACL scriptu pod uzivatelem portaladmin  
wp_root/bin/wpscript.sh -port 8882 -profile loginprofile.jacl -f script.jacl ... spusteni JACL scriptu pod uzivatelskym profilem  
wp_root/bin/xmlaccess.sh -in control.xml -user user -pwd pwd -url Myhost:9081/wps/config -out result.xml ... vyslani XML prikazu v control.xml  
wp_root/bin/xmlaccess.sh -in wp_root/config/work/setup_Portal.xml -user user -pwd pwd -url PortalConfigURL -out result.xml ... obnova Portalu  

Interaktivni mod:  
wp_root/bin/wpscript.sh -port 8882  
wsadmin&gt; $Portal login wpsadmin pwsadmin  
wsadmin&gt; $Content find page uniquename "wps.My Portal.Welcome" select  
wsadmin&gt; $Content create page "My New Page" html

prikazy:  
$Portal help  
$Portal login USER PASSWD  
$Portal logout  
$Content help  
$Content select the root ... ukaze ID root dokumentu  
$Content select [$Content create label AAA] ... ukaze ID vytvoreneho labelu AAA  
$Content create page BBB ... Vytvori stranku BBB  
$Layout help  
$Layout help select  
$Portlet - MBeam Portlet  
$Look - MBeam Look  
$Access  
$Paclist  

## xmlaccess

Export celeho portalu:  
&lt;?xml version="1.0" encoding="UTF-8"?&gt;  
&lt;request type="update" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="PortalConfig_1.3.xsd" **type="export"** export-users="false"&gt;  
&lt;portal action="export"/&gt;  
&lt;/request&gt;

Ziskani seznamu vsech zdroju stejneho typu:  
&lt;?xml version="1.0" encoding="UTF-8"?&gt;  
&lt;request type="update" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="PortalConfig_1.3.xsd" **type="export"** create-oids="false"&gt;  
&lt;portal action="locate"&gt;  
&lt;content-node action="export" objectid="*"/&gt;  
&lt;/portal&gt;  
&lt;/request&gt;

Ziskani konkretni stranky z portalu pomoci nikatniho jmena:  
&lt;?xml version="1.0" encoding="UTF-8"?&gt;  
&lt;request type="update" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="PortalConfig_1.3.xsd" **type="export"**&gt;  
&lt;portal action="locate"&gt;  
&lt;content-node action="export" uniquename="wps.MyPortal.Welcome.My Page"/&gt;  
&lt;/portal&gt;  
&lt;/request&gt;

Ziskani stranky se vsema potomkovyma objektama:  
&lt;?xml version="1.0" encoding="UTF-8"?&gt;  
&lt;request type="update" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="PortalConfig_1.3.xsd" **type="export"** create-oids="true"&gt;  
&lt;portal action="locate"&gt;  
&lt;content-node action="export" objectid="wps.My Portal" export-descendents="true"/&gt;  
&lt;/portal&gt;  
&lt;/request&gt;

Modifikace Unikatniho jmena:  
&lt;?xml version="1.0" encoding="UTF-8"?&gt;  
&lt;request type="update" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="PortalConfig_1.3.xsd" **type="update"** create-oids="false"&gt;  
&lt;portal action="locate"&gt;  
&lt;content-node action="update" objectid="_6_003II98OB041FAI_255" uniquename="my.portal.news"/&gt;  
&lt;/portal&gt;  
&lt;/request&gt;
