# IBM Cloud Manager

## Externi odkazy

[IBM Cloud Manager With OpenStack 4.2 Administrators Guide](https://www.ibm.com/developerworks/community/wikis/form/anonymous/api/wiki/e6a8193b-bd0a-4c69-b641-328d20a4f69c/page/349dbe65-7750-44cd-b283-4cbcc399da4b/attachment/cd4e0e7b-14d1-42c4-baa6-acbe004ae2bd/media/ICMO_Admin_guide%204_2%20031715.pdf)  
[IBM Knowledge Center - ICMwO 4.3](https://www.ibm.com/support/knowledgecenter/SST55W_4.3.0/liaca/liaca_kc_welcome.html)
[Instalace a odinstalace ICM 4.3](https://www.ibm.com/support/knowledgecenter/SST55W_4.3.0/liaca/liacainstallsmentry.html)  
[IBM Knowledge Center - ICM 4.3 - Deploying SCO cloud](https://www.ibm.com/support/knowledgecenter/SST55W_4.3.0/liaca/liaca_deploying_icop.html)  
[IBM Knowledge Center - ICM 4.3 - konfigurace](https://www.ibm.com/support/knowledgecenter/SST55W_4.3.0/liaca/liacaconfigentry.html)  
[Migrace z ICM 4.2 na ICM 4.3](https://www.ibm.com/support/knowledgecenter/SST55W_4.3.0/liaca/liaca_migrating_to_4_3.html)  
[Youtube - Introducing IBM Cloud Manager with OpenStack 4.3 and IBM Cloud Orchestrator 2.5](https://www.youtube.com/watch?v=qJ1jh10nszk)  

Produkt pro managovani cloudu - jednoduchy webovy portal.

## IBM Cloud Manager - Deployer

ICMD je webovy produkt na spravu privatniho cloudu. Vyzaduje mit
nainstalovany IBM Cloud Manager with OpenStack. Podporovane jsou
pouze x86 KVM, QEMU, VMware, Docker a PowerVC hostovaci systemy.

## Instalace

Instalacni balik se stahne z IBM Cloud Manager with OpenStack

tar -zxvf icm-4.2.beta-deployment-manager-ui.tar.gz  
     icm-4.2.beta/icm-4.2.beta_install -P root_password  

## Odinstalace

yum -y erase icm-deployer-client  
yum -y erase icm-deployer  

## Start/stop/status

service icm-deployer stop  
service icm-deployer start  
service icm-deployer status  
cat /opt/ibm/cmwo/version/product.version ... verze CMwO (Cloud Manager with OpenStack)  

## IBM Cloud Manager Services with OpenStack

Umoznuje privatni a hybridni cloud, obsahuje v sobe Chef, CLI,
cookbooks a OpenStack sluzby (Nova (VM), Neturon (sit), Glance
(images), Cider (storage), Ceilometr, Heat (orchestrace), Keystone
(ID), Horizon (UI))

## Start/stop/status

/etc/cmwo_services.sh status  
/etc/cmwo_services.sh start  
/etc/cmwo_services.sh stop  

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
