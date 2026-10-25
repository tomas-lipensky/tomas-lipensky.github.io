# IBM HTTP Server

$IHS ... cesta k IHS, vetsinou /opt/IBM/HTTPServer

## Externi odkazy

[trial IHS 7 download](http://www14.software.ibm.com/webapp/download/product.jsp?s=p&id=RBAR-5LER2T)  
[Download of lastest IHS](http://www-03.ibm.com/software/products/us/en/http-servers)  

## start/stop

$IHS/bin/apachectl start  
$IHS/bin/apachectl stop  
/usr/sbin/apachectl configtest

## Konfigurace

htpasswd "$IHS/conf/admin.passwd" ihsadmin ... zmena hesla uzivatele ihsadmin
