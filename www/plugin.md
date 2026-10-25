# IBM WebSphere plugin

## Externi odkazy

[trial verze WebSpehre Plugin for WAS](http://www14.software.ibm.com/webapp/download/search.jsp?go=y&rs=wspwas)  

## Cesty

PLUGIN=/opt/IBM/HTTPServer/Plugin

## Generovani pluginu

$PROFIL/bin/GenPluginCfg.sh ... generovani xml konfiguracniho souboru pro plugin pro vsechny Webservery v profilu  
$WAS/bin/GenPluginCfg.sh -propagate yes -node.name NODE -server.name AS -webserver.name W1 ... generovani a propagace xml konfiguracniho souboru pro plugin pro zadany server
