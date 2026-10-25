# Oracle Data Integrator

## Externi odkazy

http://technet.oracle.com  
http://metalink.oracle.com  
[ODI na wiki](http://en.wikipedia.org/wiki/Oracle_Data_Integrator)  

## Popis

ODI je z produktove rady Oracle Fussion Middleware, ktera slouzi na vytvareni datovych sklau a ETL transformaci pro integraci dat a BI.
Pro svuj beh patrebuje repozitar instance, ktery se vytvari pomoci [RCU](../sw/rcu.html).
Jedna moznost je instalovat standalone agent a stand alone klienta na editaci datoveho skladu a ETL procesu.
Dalsi moznost je nainstalovat J2EE verzi ODI a zaintegrovat do WLC nebo do WAS, vsechna konfigurace se pak provadi browserem.  

## Prikazy Standalone ODI

reposinst.sh ... prikaz na vytvoreni repozitare OWB na OracleDB.  
.agent.sh -PORT-7010 -NAME-EduAgentss

### Prikazy J2EE ODI

startManagedWeblogic.sh odiserver1  

### URL J2EE agenta
http://IP:PORT/odiconsole/
