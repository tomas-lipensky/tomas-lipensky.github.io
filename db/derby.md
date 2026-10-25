# Apache Derby

## Odkazy

[Starting ij](https://db.apache.org/derby/docs/10.7/tools/ttoolsij11815.html)  
[Download derby](http://db.apache.org/derby/derby_downloads.html)  

## Derby Network Server

$DERBY_HOME/setNetworkServerCP ... nastavi CLASSPATH  
$DERBY_HOME/startNetworkServer.bat ... spusti network server  
java -jar derbyrun.jar server start ... alternatijva k predchozim 2 prikazum  
java -jar %DERBY_INSTALL%\lib\derbyrun.jar server shutdown ... zastavi Derby Network Server  

## Derby Client==

java -jar ~/derby/db-derby-10.12.1.1-bin/lib/derbyrun.jar org.apache.derby.tools.ij ... spusti interaktivni mod Derby klienta  
java -jar ~/derby/db-derby-10.12.1.1-bin/lib/derbyrun.jar org.apache.derby.tools.ij abc.sql ... spusti SQL davku v Derby klientovi  
java org.apache.derby.tools.ij -Dderby.system.home=/home/bill/databases ... spusti interaktivni mod, nastavi lokaci do adresare s databazema  

#### IJ prikazy:

connect 'jdbc:derby:/full/path/to/the/database/folder'; ... pripojeni k souborovemy kontejneru  
connect 'jdbc:derby://localhost:1527/sample'; ... pripojeni k listeneru  
show connections; ... ukaze pripojeni  
show indexes; ... ukaze indexy  
show schemas; ... ukaze schemata  
show tables; ... ukaze tabulky  
describe TVC4.ACTIVITY; ... popise tabulku  
run 'abc.sql'; ... provede SQL z abc.sql souboru
