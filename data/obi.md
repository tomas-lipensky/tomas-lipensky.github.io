# Oracle Business Inteligence

### Externi odkazy

http://technet.oracle.com  
http://metalink.oracle.com  
[OBI popis na oracle.com](http://www.oracle.com/technetwork/middleware/bi-enterprise-edition/overview/index.html)

### Interni odkazy

### Popis

OBI je z rodiny Oracle Fussion a je to Business Inteligence produkt.  

#### Start/stop/status/info

Start:  
$WLC_HOME/server/bin/startNodeManager.sh  
$WLC_HOME/user_projects/domains/bifoundation_domain/bin/startWebLogic.sh  
$WLC_HOME/instances/instance1/bin/opmnctl startall  

Stop:  
$WLC_HOME/instances/instance1/bin/opmnctl stopall  
$WLC_HOME/user_projects/domains/bifoundation_domain/bin/stopWebLogic.sh  
ps -ef | grep NodeManager | grep -v grep | awk '{ print $2 }' | xargs kill  

Status:  
$WLC_HOME/instances/instance1/bin/opmnctl status  

#### Konfigurace

./Oracle_BI1/bin/config.sh .. konfigurace produktu, pokud neprobehla pri instalaci  

#### Logy

$WLC_HOME/common/nodemanager/nodemanager.log  

### Prikazy

ORACLE_HOME/jlib/cloningclient.jar ... klonovani BI  
OPatch ... patchovani Oracle produktu, i BI  

#### URL
http://IP:7001/console ... administracni konsole WebLogicu  
http://IP:7001/em - enterprise konzole ... Enterprise manager na spravu Oracle produktu  
http://IP:7001/analytics ... Analytics tool  
http://IP:7001/xmlpserver ... BI Publisher
