---
title: Cognos BIRT
---

## Interni odkazy

## Externi odkazy

[Cognos BI training](www.ibm.com/cognos/training)  
[IBM Support page](https://www-947.ibm.com/support/entry/myportal/support)  
[Fixlist for Cognos BI 10.2](http://www-01.ibm.com/support/docview.wss?uid=swg27027081)
[DW - IBM Cognos Proven Practices: Securing the IBM Cognos 10 BI Environment](http://www.ibm.com/developerworks/data/library/cognos/security/cognos_bi_platform/page602.html)  
[DW - IBM Business Analytics Proven Practices: IBM Cognos BI Dispatcher Routing Explained](http://www.ibm.com/developerworks/data/library/cognos/infrastructure/cognos_specific/page510.html)  
[IBM Cognos Planning and BI Backup and Recovery Guide (Updated)](http://www.ibm.com/developerworks/data/library/cognos/page324.html)  
[IBM Cognos Proven Practices: IBM Cognos 10 Dynamic Query Analyzer User Guide](http://www.ibm.com/developerworks/data/library/cognos/infrastructure/cognos_specific/page578.html)  
[Logging Console and Monitoring](http://www.ibm.com/developerworks/data/library/cognos/page80.html)  

## BIRT - Business Intelligence Reporting Tool

### Odkazy

[Online napoveda](http://help.eclipse.org/kepler/index.jsp?topic=%2Forg.eclipse.birt.doc%2Fbirt%2FScriptingReference.24.3.html)  

### Komponenty

[BIRT Designer](http://download.eclipse.org/birt/downloads/) - komponenta na vytvareni a reportovych vzoru a generovani reportu  
[BIRT Runtime](http://download.eclipse.org/birt/downloads/) - komponenta na generovani reportu ze vzoru  

### Prikazy

genReport.sh  

### Operatory

if-else operatory, na zaklade podminky se priradi cislo sloupci:

```
if (row["START_TIME_"] == null) { 1 }
else if (row["END_TIME_"] == null) { 2 }
else if (row["END_TIME_"] != null) { 3 }
else {0};
```

row["sloupec"].replace(/\^/g," "); ... nahrazeni znaku regularnimi vyrazy  

### Import z JSON souboru

[Use JSON as a Scripted Data Set](https://blogs.opentext.com/use-json-as-a-scripted-data-set/)
