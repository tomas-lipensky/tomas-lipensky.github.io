---
title: Ant
---

Apache ANT - program, ktery je alternatuvou pro make pro jaovoske aplikace. Ma za ukol zautomatizovat vytvareni programu pomoci nadefinovanych cilu, tedy napriklad kompilace, provadeni testu atd.

## Externi odkazy

## Minimalni definice

&lt;?xml version="1.0" encoding="iso-8859-2" standalone="yes"&gt; ... definice xml dokumentu  
&lt;project name="minimalni projekt" basedir="." default="pozdrav"&gt; ... cely dokument musi byt uzavren ve znackach projekt  
&lt;target name="pozdrav"&gt; ... devinice cile. Musi existovat alespon 1 cil - vychozi, ktery je u parametru default ve znacce project  
&lt;!-- Vypise pozdrav --&gt; ... komentar  
&lt;echo message="Ahoj"\&gt; ... Vypis na obrazovku  
&lt;/target&gt; ... ukonceni cile  
&lt;/project&gt; ... ukonceni projektu  

## Zakladni prokazy ANTu

&lt;priject name="a" depends="b,c"&gt; ... definice cile, nazev je povinny, zavislosti jsou nepovinne. zavislosti provedou akce b a c pred akci a  

### Priklad projektu na WebSphere

```xml
<project name="Jmeno projektu" default="init">
  <property file="ant.properties"/>
  <target name="init">
    <tstamp/>
    <echo message="--- boild of ${ant.project.name} started at ${TSTAMP} on ${TODAY} by ant v.${ant.version} ---"/>
  </target>

  <target name="stopApplication" description="Stop the specified appli">
    <echo message="--- Stopping the ${applicationnName}"/>
    <wsadmin script="${softwareDir}\stopApplication.py" lang="jython" profile="{$softwareDir}\profile.py" port="${portNB}" conntype="soap">
      <arg value="${applicationName}>
      <arg value="${clusterName}">
    </wsadmin>
  </target>

  <taskdef name="wsadmin" classname="com.ibm.websphere.ant.tasks.WsAdmin"/>
</project>
```

&lt;property name"applicationName" value="APP1"&gt;
