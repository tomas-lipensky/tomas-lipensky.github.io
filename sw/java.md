# Java aplikace

## Interni a Externi odkazy:

[Aplikacni servery](../web/index.html)  
[Programovaci jazyk java](../dev/java.html)  
[J2EE](../web/j2ee.html)  
[Testcontainers](https://testcontainers.com/guides/getting-started-with-testcontainers-for-java/) ... definování Docker test kontejnerů v Maven projektu, konterjer se vytvoří pouze na test v režii Maven buildu  

## Nastroje z prikazove radku a JVM prepinace

java balik.program ... spusti balik/program.class  
java -jar a.jar ... spusti a.jar  
jar ... baleni, rozbalovani javovskych souboru (trid) do jednoho balicku (puziva zip)  
jar tf util.jar ... vylistuje tridy z balicku  
javap -classpath util.jar com.myproject.add ... vylistuje metody pro tridu com/myproject/add.class z baliku util.jar  
kill -3 PID ... provede thread dump procesu - nezabije  

### JVM přepínače

java -version ... verze javy  
java -XshowSettings:vm -version ... ukáže max. velikost heapy, další požnosti: all, locale, properties  
1.XX:+PrintFlagsFinal ... ukáře parametry javy  
2.XX:MinRAMPercentage=50.0 -XX:MaxRAMPercentage=80.0 ... procentualní nastavení velikosti heapy, užitečné na kontejnerech  
3.Xdump:directory=/logs ... nastavení cesty pro dumpy  
4.Xdump:java:defaults:file=javacore_last.txt ... název souboru pro tread dump  
5.Xdump:heap:defaults:file=heapdump_last.phd ... název soubory pro heap dump  
6.Xdump:system:none ... vypne systémový dump  
7.Xdump:snap:none ... vypna snap dump  
8.Xdump:jit:none ... vypne jit dump  
9.Xdump:java:events=systhrow,filter=java/lang/OutOfMemoryError ... thread dump když je OutOfMemoryError  
10.Xdump:heap:events=systhrow,filter=java/lang/OutOfMemoryError ... heap dump, když je OutOfMemory  
11.Xss256k ... velikost stacku  

### Balicek java-VERZE-openjdk-devel:

javac balik/program.java ... zkompiluje zdrojovy kod v adresari balik na balik/program.class  
javadoc ... vytvari html prehled trid a funkci pomoci komentaru /** */  
javap program ... zkompiluje program.java do program.p mezikodu javy  
jcmd 7 help ... seznam možných operací  
jcmd 7 Dump.java ... vytvoří javacore.txt  
jcmd 7 GC.run ... provede garbage collection  
jdmpview -core /application/heapdump.20240213.122917.7.0003.phd ... prohlížení dumpu  
jdb ... java debugger  
jmap -histo 7 ... ukáže která třídá má kolik paměti  
jps ... vypise vsechny java procesy - PID + zkracene jmeno tridy  
jps -l ... vypise vsechny java procesy - PID + plne jmeno tridy  
jps -m ... vypise vsechny java procesy - PID + zkracene jmeno tridy + parametry, ktere jdou do tridy main  
jps -v ... vypise vsechny java procesy - PID + zkracene jmeno tridy + vsechny parametry  
jstat [-class](http://download.oracle.com/javase/1,5.0/docs/tooldocs/share/jstat.html) PID 5000 5 ... Statistiky o chovani classloaderu procesu PID po 5 sekundach, 5 opakovani  
jstat -compiler ... Statistics of the behavior of the HotSpot Just-in-Time compiler.  
jstat -gc ... Statistics of the behavior of the garbage collected heap.  
jstat -gccapacity ... Statistics of the capacities of the generations and their corresponding spaces.  
jstat -gccause ... Summary of garbage collection statistics (same as -gcutil), with the cause of the last and current (if applicable) garbage collection events.  
jstat -gcnew ... Statistics of the behavior of the new generation.  
jstat -gcnewcapacity ... Statistics of the sizes of the new generations and its corresponding spaces.  
jstat -gcold ... Statistics of the behavior of the old and permanent generations.  
jstat -gcoldcapacity ... Statistics of the sizes of the old generation.  
jstat -gcpermcapacity ... Statistics of the sizes of the permanent generation.  
jstat -gcutil ... Summary of garbage collection statistics.  
jstat -printcompilation ... HotSpot compilation method statistics.  
jinfo PID ... informace o java procesu a o jave  
jmap PID ... Prirazeni pameti v procesu  
ps -T -p 7 ... seznam vláken procesu, včetně třídy  

### Ostatni nastroje

[IBM Monitoring and Diagnostic Tools for Java - Health Center](http://www.ibm.com/developerworks/java/jdk/tools/healthcenter/) - monitorovaci a vysetrovaci nastroj na IBM Java procesy  
[ANT](../dev/ant.html) ... nastron na sestavovani aplikaci (kompilace, balickovani atd.)  
JCoverage ... Nastroj na vyhodnoceni pokryti kodu testovacimi prodecurami JUnit  
JSwat ... graficky jdb  
JUnit ... testovani procedur  
Pmd ... staticke testovani zdrojoveho kodu  
JMeter ... testovani vykonnosti http, ftp, ldap, soap atd. aplikaci  
[Maven](../dev/maven.html) ... sprava projektu  

## Scénáře

### Analýza CPU náročnosti

top -H -p 6 ... interaktivní sledování vláken a jejich CPU zdrojů  
ps -eT -o pid,tid,pcpu,comm ... seznam vláken, nýzvů tříd a jejich CPU využití  
kill -3 6 ... pošle signál do JVM, ať se vygenerují dumpy  
printf "0x%x\n" 65 ... převede Thread ID 20 na hexadecimální tvar vyskytující se v javacore, např. na 0x65  
grep 0x41 -A3 -B3 javacore.20260316.122151.7.0001.txt ... nalezne thread 65 v Javacore dumpu  
grep THREADINFO javacore.XXX.txt ... seznam tříd
