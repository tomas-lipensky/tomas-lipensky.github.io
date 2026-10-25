# IBM Cloud Private

## Externi odkazy

[IBM Cloud Private Community Edition](https://github.com/IBM/deploy-ibm-cloud-private) - Gitlab repozitar  
[Hands-on time with IBM Cloud Private](https://www.ibm.com/blogs/bluemix/2018/03/demo-try-private-cloud-install-an-app/)  
[Deploy a cloud-native microservices application on IBM Cloud Private](https://www.ibm.com/cloud/garage/tutorials/cloudnative-microservices-cloud-private?task=3) - Tutorial  
[Slack kanal o ICP](https://ibm-cloud-tech.slack.com/messages/C2HQFDAET/)  

Produkt pro managovani cloudu - jednoduchy webovy portal.

## Instalace

Instalacni balik se stahne z IBM Cloud Manager with OpenStack

## Odinstalace

## Start/stop/status

service icm-deployer stop  
     service icm-deployer start  
     service icm-deployer status  
     cat /opt/ibm/cmwo/version/product.version ... verze CMwO (Cloud Manager with OpenStack)  

## Komponenty

[prometheus](../sw/prometheus.html) ... pro monitoring  

## Cesty, soubory

/opt/ibm/cmwo/chef-repo ... repozitach Shefa  
/opt/ibm/cmwo/cli/config/ ... yml soubory - Heat templaty  
/opt/ibm/cmwo/properties/cmwo_4.3.lic ... licencni klic  

## Prikazy, management

knife os manage deploy cloud your-icos-hybrid-cloud.yml ... Deploy cloudu  
knife node list ... seznam region serveru  
knife node show FQDN ... informace o region serveru  

## Operace

[Zmena flavor](https://www.ibm.com/support/knowledgecenter/SST55W_4.3.0/liaca/liacaresizeopenstack.html) - CPU/MEM  

## Problemy, trouble shooting

[Kolekce logu a nastaveni](http://www-01.ibm.com/support/docview.wss?uid=nas8N1020598), napriklad pro IBM support  
[qmgcollect.sh](ftp://public.dhe.ibm.com/services/us/igsc/cloud/) ... [kolekce logu](http://www-01.ibm.com/support/docview.wss?uid=nas8N1020618) o ICM pro poslani na IBM support
