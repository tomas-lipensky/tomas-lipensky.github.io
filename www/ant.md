# Ant

Apache ANT - program, ktery je alternatuvou pro make pro jaovoske aplikace. Ma za ukol zautomatizovat vytvareni programu pomoci nadefinovanych cilu, tedy napriklad kompilace, provadeni testu atd.

### Obsah

Externi odkazy  
Minimalni definice  
Zakladni prikazy Antu  
Priklad projektu na WebSphere  

### Externi odkazy

### Minimalni definice

&lt;?xml version="1.0" encoding="iso-8859-2" standalone="yes"&gt; ... definice xml dokumentu  
&lt;project name="minimalni projekt" basedir="." default="pozdrav"&gt; ... cely dokument musi byt uzavren ve znackach projekt  
&lt;target name="pozdrav"&gt; ... devinice cile. Musi existovat alespon 1 cil - vychozi, ktery je u parametru default ve znacce project  
&lt;!-- Vypise pozdrav --&gt; ... komentar  
&lt;echo message="Ahoj"\&gt; ... Vypis na obrazovku  
&lt;/target&gt; ... ukonceni cile  
&lt;/project&gt; ... ukonceni projektu  

### Zakladni prokazy ANTu

&lt;priject name="a" depends="b,c"&gt; ... definice cile, nazev je povinny, zavislosti jsou nepovinne. zavislosti provedou akce b a c pred akci a  

====Priklad projektu na WebSphere====

```
&lt;project name="Jmeno projektu" default="init"&gt;
  &lt;property file="ant.properties"/&gt;
  &lt;target name="init"&gt;
    &lt;tstamp/&gt;
    &lt;echo message="--- boild of ${ant.project.name} started at ${TSTAMP} on ${TODAY} by ant v.${ant.version} ---"/&gt;
  &lt;/target&gt;

  &lt;target name="stopApplication" description="Stop the specified appli"&gt;
    &lt;echo message="--- Stopping the ${applicationnName}"/&gt;
    &lt;wsadmin script="${softwareDir}\stopApplication.py" lang="jython" profile="{$softwareDir}\profile.py" port="${portNB}" conntype="soap"&gt;
      &lt;arg value="${applicationName}&gt;
      &lt;arg value="${clusterName}"&gt;
    &lt;/wsadmin>
  &lt;/target&gt;

  &lt;taskdef name="wsadmin" classname="com.ibm.websphere.ant.tasks.WsAdmin"/&gt;
&lt;/project&gt;
```

&lt;property name"applicationName" value="APP1"&gt;
