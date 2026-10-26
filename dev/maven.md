---
title: maven
---

## Maven

Maven je buildovací nástroj, který pracuje s [pom.xml](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) souborem, který definuje informace o produktu - název produktu, závislosti atd.

## Odkazy

[https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) ... maven za 5 minut - pěkný úvod  
[pluginy](https://maven.apache.org/plugins/index.html)  

## souborová struktura

~/.m2/settings.xml ... společná nastavení pro všechny projekty, typicky hesla, cesty k repozitářům, [profily](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) atd  
~/.m2/[settings-security.xml](https://maven.apache.org/guides/mini/guide-encryption.html) ... heslo na šifrování hesel v settings.xml  
~/.m2/repository ... cache stažených knihoven  
pom.xml ... project object model - soubor v projektu, který definuje název balíčku, verzi, závislosti atd.  

## Syntaxe

mvn -v ... verze Mavenu  
mvn [mezerou_oddělené_fáze/pluginy](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html) [přepínače](https://maven.apache.org/ref/3.9.11/maven-embedder/cli.html)

## Přepínače

1.DskipTests ... nebude dělat testy kódu, -D nastavuje systémové pproměnné Mavenu  
2.Dmaven.test.skip=true ... to samé  
3.Daether.connector.https.securityMode=insecure ... nekontroluje TLS certifikáty pro stahování artefaktů  
4.T 4 ... builduje ve 4 vláknech  
5.X ... debug mód, vypisuje hodně informací o tom, co dělá  
6.s ~/.m2/settings.jine.xml ... použití jiného settings.xml s kredencema  

## Příklady

mvn help:active-profiles ... informace o aktivních profilech  
mvn help:active-profiles -P-dev,prod ... to samé, jen se deaktivuje profil dev a aktivuje profil prod  
mvn help:all-profiles ... seznam všech profilů  
mvn dependency:tree -X ... seznam závislostí  
mvn -help ... help  
mvn help:evaluate -Dexpression=project.version -q -DforceStdout ... ukáže aktuální verzi projektu z pom.xml  

mvn deploy:deploy-file -Durl=https://maven.corp.com/repo -DrepositoryId=my.server -Dfile=your-artifact-1.0.jar ... nahraje soubor do repozitáře  
mvn deploy:deploy-file -Durl=https://maven.corp.com/repo -DrepositoryId=my.server -Dfile=your-artifact-1.0.jar -Daether.connector.https.securityMode=insecure ... nekontroluje certifikáty  
mvn deploy -DskipTests -DaltReleaseDeploymentRepository="jfrog::default::https:*www.jfrog.io/artifactory/release" -DaltSnapshotDeploymentRepository="jfrog::default::https:*www.jfrog.io/artifactory/snapshot" ... vyreleasování do jiného repozitáře, než je uvedeno v pom.xml  

mvn deploy:deploy-file -DgroupId=cz.lipensky.spotless
1.DartifactId=spotless-eclipseformat
2.Dversion=1.0.0
3.Dpackaging=xml
4.Dfile=spotless.eclipseformat.xml
5.DgeneratePom=true
6.DrepositoryId=maven-java-releases
7.Durl=https://nexus.server/repository/maven-java-releases/ ... release do repozitáře z paramentrové řádky, -D jsou proměnné
