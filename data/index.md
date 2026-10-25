# index

### Architektura

Obecne kazda aplikace pro nakladani s daty (ETL - extract transform load, business inteligenci, master data management, ...) se sklada z mnoha komponenet, pricemz jedna z komponent je:

[aplikacni server](../web/) a aplikace v nem, ktera zajistuje webovy management

a dalsi komponenty, ktere provadi primo manipulaci s daty.

### Odkazy

[Big Data and Analytics University](http://learning2.atlanta.ibm.com/qpg/university.nsf/analytics/BDA-Lobby) na learning2.atlanta.ibm.com  
[IBM BigData & Analytics Hub](http://www.ibmbigdatahub.com/)  

### ETL nastroje (Extract Transform Load

[Infosphere Datastage](datastage.html) (Infosphere Information Server)
[Oracle Warehouse Builder](owp.html)
[Oracle Data Integrator](odi.html)
Informatica PowerCenter Express - https://community.informatica.com/solutions/pcexpress
[Informatica PowerCenter](informatica.html) - http:*etl-tools.info/informatica/components.html http:*etl-tools.info/informatica/tutorial.html
[TalenD ETL](https://www.talend.com/products/talend-open-studio/) - OpenSource ETL

### Kontinualni prisun dat - zpracovani

[IBM Steams](steams.html)  

### Business Inteligence, <a fref="http://www.ibm.com/analytics/us/en/index.html|business analytics]] - reporting


[IBM Cognos BI](cognos.html) - [Business Intelligence](http://en.wikipedia.org/wiki/Business_intelligence)  - Reporty, analyzy dashboardy a skorovani z dat
[IBM Cognos TM1](tm1.html)
[IBM Cognos Insight](http://www.ibm.com/software/products/us/en/cogninsi) - Analyzy a vizualizace a sdileni dat
[IBM Cognos Express](http://www-01.ibm.com/software/analytics/cognos/express/)
IBM SPSS
[IBM SPPS Modeler](http://www-01.ibm.com/software/analytics/spss/products/modeler/) - prediktivni analyza
[IBM SPPS Data Collection](http://www-01.ibm.com/software/analytics/spss/products/data-collection/) - 
[IBM SPSS Statistics](http://www-01.ibm.com/software/analytics/spss/products/statistics/) - Statistiky na porozumeni dat a trendu
[IBM SPSS Collaboration and Deployment Services](http://www.ibm.com/software/products/us/en/spss-collaboration) - automatizace analytickeho procesu a bezpecne sdileni
[IBM Predictive Maintenance and Quality](http://www.ibm.com/software/products/us/en/predictive-maintenance-quality)
[IBM Algorithmics software](http://www-01.ibm.com/software/uk/analytics/algorithmics/) - financial analytics tool for decisions based on risk management
[IBM OpenPages](http://www-01.ibm.com/software/uk/analytics/openpages/) - tool for risk and compliance management
[DB2 Query Management Facility](http://www-03.ibm.com/software/products/en/qmf)
Microstrategy
[Pentaho](pentaho.html)
[Oracle BI](obi.html)
[Oracle Business Intelligence Discoverer](obid.html) (Oracle Discoverer)
[Oracle Hyperion](hyperion.html) ... [Business Intelligence ](http://en.wikipedia.org/wiki/Business_intelligence)- rozhodavaci software a mereni vykonu podniku


### Master data management


[InfoSphere MDM CS](mdm.html) - Master Data Management Colaboration Server (Colaboration Edition), Drive [WebSphere Product Center](http://www.ibm.com/developerworks/data/tutorials/dm0608lee/) nebo PIM
Physical MDM - drive Transactional MDM, [WebSphere Customer Center](http://www-01.ibm.com/software/data/masterdata/customer/) -  <!--a href="wcc.html"-->WCC<!--/a-->, MDM Server
Virtual MDM - drive MDM Hub, nebo MDS - Master Data Service
[informaticamdm.html](informaticamdm.html)Informatica MDM


### Data Explorers


[IBM Watson Explorer](dataexplorer.html) - IBM InfoSphere Data Explorer ... Aplikace na prochazeni dat - objevuje, spojuje, nabizi a umoznuje prohledavani dat
[ELK (Elastic stack)](https://www.quora.com/What-is-the-ELK-stack) - Log management platforma - prijimani logu a eventu, hledani v logach, analyza logu (bezpecnost, perfomance, ..). Vice na [qbox](https://qbox.io/blog/welcome-to-the-elk-stack-elasticsearch-logstash-kibana)
[Elasticsearch](https://en.wikipedia.org/wiki/Elasticsearch) ... vyhledavaci engine postaveny na [Apache Lucene](https://en.wikipedia.org/wiki/Apache_Lucene)
[Kibana](https://en.wikipedia.org/wiki/Kibana) ... vizualizacni plugin do Elasticsearch
[Logstash](https://wikitech.wikimedia.org/wiki/Logstash) ... Nastroj na managovani udalosti a logu
[Apache Lucene](https://en.wikipedia.org/wiki/Apache_Lucene) ... java knihovna na ziskavani informaci
[Apache Soir](https://en.wikipedia.org/wiki/Apache_Solr) ... Vyhledavaci engine postaveni na [Apache Lucene](https://en.wikipedia.org/wiki/Apache_Lucene)
[Apache Kafka](https://en.wikipedia.org/wiki/Apache_Kafka) ... stream processing platforma (streamy jako logy, audio, video, ...) - [pekny tutorial](https://www.tutorialspoint.com/apache_kafka/apache_kafka_integration_spark.htm)
[Apache Spark](https://en.wikipedia.org/wiki/Apache_Spark) ... cluster framework pouzitelny napr. s Kafka. Komponenty - Spark SQL, Spark streaming, GraphX, MLib Machine Learning


### Nastroje na rizeni rustu dat

IBM InfoSphere Optim Grow ... Aplikace na spravu politiky rustu dat - presouvani dat na levnejsi media, zalohovani, mazani atd.

### Nastroje na kryptovani dat

[Infosphere Guardium Data Encryption - GDE](gde.html) ... Nastroj na enkrypci a zpristupneni dat na zaklade politik

### Big Data


Netezza
[Teradata Warehouse](../db/td) - datovy sklad pro strukturovana data v zadu peta bajtu
Hadoop ... clusterovy filesystem - spojovani datovych ulozist na tisicovkach nodu - datove uloziste na nestrukturovana data
[FPA](http://dmg.org/pfa/docs/motivation/) ... Portable Format for Analytics ... metoda k vyuziti hadoop a jinych nastroju na analyzu dat
Aster DB - discovery platvorm - reseni na polostrukturovana data - ukladani, transformace nestrukturovanycn na polostrukturovana
Hortonworks - Nahravani nestrukturovany dat pomoci Aster do datoveho skladu

