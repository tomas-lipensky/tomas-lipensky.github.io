# BPM

## REST API

[POST /bpm/repo/projects](https://www.ibm.com/support/knowledgecenter/SSTLXK_8.5.0/com.ibm.wbpm.ref.doc/rest/repository/bpm_repo_projects.htm) ... Import resoure  
[GET /bpm/repo/projects/{projectId}/export](https://www.ibm.com/support/knowledgecenter/SSTLXK_8.5.0/com.ibm.wbpm.ref.doc/rest/repository/bpm_repo_projects_projectid_export.htm) ... export resource  

## Prikazy

wsadmin -h SERVER -user UZIVATEL -password HESLO -lang jython ... spusti wsadmina na ICO a BPM prikazy  
[deployer](https://www.ibm.com/support/knowledgecenter/SS4KMC_2.4.0/com.ibm.sco.doc_2.4/enablement/commandlineinterface.html#commandlineinterface__BusinessProcessManagerCommandLineIn) -h SERVER -u UZIVATEL -p HESLO -f SKRIPT -s SOUBOR ... provede skript a vstup ze souboru  

## wsadmin

[AdminTask.BPMImport('[-inputFile FILE]')](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/enablement/commandlineinterface.html)  
[AdminTask.BPMExport('[-containerAcronym BILLDISP -containerSnapshotAcronym SS2.0.1 -containerTrackAcronym Main -outputFile C:\processApps\BILLDISP201.twx]')](https://www.ibm.com/support/knowledgecenter/SSFPJS_8.5.0/com.ibm.wbpm.ref.doc/topics/rref_bpmexport.html)  
[AdminTask.BPMShowProcessApplication()](https://www.ibm.com/support/knowledgecenter/SSFPJS_8.5.0/com.ibm.wbpm.ref.doc/topics/rref_showprocessapplication.html)  
[AdminTask.BPMListProcessApplications()](https://www.ibm.com/support/knowledgecenter/SSFPJS_8.5.0/com.ibm.wbpm.ref.doc/topics/rref_bpmlistpa.html)  

## deploy skripty

deployer.virtualimages.create('http://server.xyz.com/path/to/foo.ova') ... naimportuje virtualni obraz  
deployer.applications.create ... naimportuje novy virtualni obraz do Workload Deployer komponenty  

## Skipty

/opt/ibm/ico/pcg ... Ukazky skriptu v ICO2.5
