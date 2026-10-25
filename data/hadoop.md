# Apache Hadoop

### Architektura

- Node - jednotlivy pocitac
- Rack - 30-40 Nodu na stejnem switchi - velky sitovy provoz
- Cluster - Racky managovane pomoci Hadoop

### Komponenty

- Distribuovane filesystemy: Hadoop Distributed File System (HDFS), nebo IBM Spectrum Scale
- MapReduce Engine - Framework na provadeni kalkulaci na datach v FS a obsahujici casovac a resource manager

### Projekty souvisejici s Hadoop

- Lucene je knihovna na engine textoveho vyhledavani napsana v Java
- Hbase je Hadoop databaze
- Hive poskytuje data warehousing nastroj k extrakci, transformani a natazeni (ETL) dat, a dotazovani techto dat ulozenych v Hadoop souborech
- Pig je high level jazyk, ktery produkuje MapReduce kod k analyze velkych mnozin dat
- Spark je cluster computing framework
- ZooKeeper je centralizovany configuracni sluzba a jmenny registr pro velke distribuovane systemy
- Ambari spravuje a monitoruje Hadoop clustery pomoc intuitivniho web UI
- Avro je data serialization system
- UIMA je architekture pro vyvoj, nachazeni, kompozici a nasazovani pro analyzu nestrukturovanych dat
- Yarn is a large-scale operating system for big data applications
- Mapreduce is a software framework for easily writing applications which processes vast amounts of data
- Highly extensible, highly scalable Web crawler Nutch 1.x enables fine grained configuration, relying on Apache Hadoop™ data structures, which are great for batch processing.
- Jaql is primarily a query language for JavaScript Object Notation (JSON)
- [IBM BigInsight Quick Start Edition](https://ibm-open-platform.ibm.com/biginsights/download-pages/download-qse-vm/?&S_TACT=M1610EPW)

#### HDFS

FS na existujicich FS operacniho systemu, navrzeny k toleranci selhani komponent a k obsahovani velikych souboru. Male soubory - pomaly pristup. Hledani draha operace. Designovano na streamy nebo sekvencni data. Hadoop blok je soubor na disku o jiste velikosti (napriklad 128MB).
