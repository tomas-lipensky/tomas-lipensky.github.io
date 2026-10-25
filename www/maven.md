# Java aplikace - Maven

Apache Maven - nastroj na spravu projektu. Umoznuje vest projekt od definice projektu, kompilaci zdrojovych kodu v Jave, testovani kodu, vytvareni dokumentaci, vytvareni internetovych stranek a distribuci balicku.

## Externi odkazy

[maven.apache.org](http://maven.apache.org/)  

## Zalozeni projektu a uvod od aplikace Maven

maven -b  -p POM.xml -d ~/maven -o AKCE1 AKCE2 ... spusti akce AKCE1 a AKCE2, nezobrazi logo (-b), zpracuje projekt POM.xml v adresari ~/maven, bude pracovat v offline modu (-o)  
maven -b gennapp ... (maven-genapp-plugin) Vytvori novy projekt - vytvori project.xml a prvotni adresarovou strukturu  
project.xml ... Definice obecnych vlastnosti projektu  

## Prace s projektem

maven -b pom:contentvalidate ... (maven-pom-plugin) zkontroluje platnost POMu v projekt.xml  
maven -b pom:validate ... (maven-pom-plugin) zkontroluje posloupnost xml znacek, nepovinne, ale zlepsi prehlednost POMu  
maven -b pom:deploy ... zazalohuje POM do centralni databaze, ve jmenu bude verze  
maven -b pom:deploy-snapshot ... zazalohuje POM do centralni databaze, ve jmenu bude datum  
maven -b pom:install ... zazalohuje POM do lokalni databaze, ve jmenu bude verze  
maven -b pom:install-snapshot ... zazalohuje POM do lokalni databaze, ve jmenu bude datum  
maven -b java:preparefilesystem ... (maven-java-plugin) Pripravi adresarovou strukturu pro kompilaci - tato procedura je obsazena i v java:compile  
maven -b java:compile ... provede prelozeni kodu  
maven -b java:jar-resources ... zkopiruje zavislosti do adresare s prelozenym kodem  
maven -b pmd:report ... provede otestovani zdrojovych kodu programem pmd pravidly v souboru urcenym vlastnosti maven.pom.rulesetfiles  
maven -b pmd:cpd-report ... vyhledava stejne zdrojove kody  
maven -b test:compile ... (maven-test-plugin) provede preklad testovacich modulu  
maven -Dtestmatch=\*kus_nazvu\* test:match ... spusti jen testy s konkretnim kusem nazbu  
maven -b test:prepare-filesystem ... pripravi adresarovou strukturu pro testy  
maven -Dtestcase=TEST1 test:single ... provede pouze 1 test  
maven -b test:test ... provede vsechny testy  
maven -b test:test-resources ... provede zkopirovani zavislosti potrebnych pro testy  
maven -b test:ui ... spusti graficky interface pro testy  
maven -b junit-report:report ... provede konverzi vysledku testu do jednoho souboru junit-report.xml  
maven -b jcoverage:on ... spusti analyzu pokryti zdrojoveho kodu testy  
maven -b jcoverage:html-report ... zkonvertuje zpravu z jcoverage:on do html  
maven -b jar:jar ... vytvori archiv ze zkompilovanych souboru
maven -b jar:snapshot ... provede shapshot archiv - archiv s casovym udajem v nazvu  
maven -b jar:deploy(-snapshot) ... umisti archiv do cetralniho uloziste  
maven -b jar:install(-snapshot) ... umisti archiv do lokalniho uloziste  
maven -b javadoc:generate ... provede vygenerovani dokumentace  
maven -b javadoc:deploy(-snapshot) ... provede nahrani dokumentace do centralniho uloziste  
maven -b javadoc:install(-snapshot) ... provede nahrani dokumentace do lokalniho uloziste  
maven -b xdoc:init ... vytvori adresarovou struktoru  
maven -b xdoc:validate ... zkontroluje vytvorene dokumenty xdoc (z javadoc)  
maven -b xdoc:generate-from-pom ... nacte data z POMu  
maven -b xdoc:transform ... provede transformace dokumentace  
maven -b site:generate ... vygeneruje webove stranky projektu  
maven -b site:run-reports ... provede vybrane testy a zaktualizuje jejich vysledky na webobove strance  
maven -b site:ftpdeploy ... nahraji se stranky pres ftp  
maven -b site:sshdeploy ... nahraji se stranky pres ssh  
maven -b site:fsdeploy ... nahraji se stranky v ramci FS  
maven -b site:deploy ... provede site:generate + nahrani stranek  
maven -b dist:build ... vytvori archiv se zdrojovymi kody i s programem + s dokumentaci pomoci maven-javadoc-pluginu  
maven -b dist:build-bin ... vytvori archiv s progrramem a dalsi s dokumentaci  
maven -b dist:build-src ... vytvori archiv se zdrojovymi kody  
maven -b dist:build-setup ... pripravi adresarovou strukturu (danou vlastnosti maven.dist.dir)  
maven -b dist:prepare-bin-filesystem ... pripravi adresare pro archivy s programy  
maven -b dist:prepare-src-filesystem ... pripravi adresare pro archivy se zdroji  
maven -b dist:deploy ... provede prenos archivu na vzdaleny server  
maven -b dist:deploy-bin ... prenese pouze archiv s binarkou  
maven -b dist:deploy-snapshot ... prenese pouze archiv s aktualnim obrazem stavu projektu  
maven -b dist:deploy-src ... prenese pouze archiv se zdroji  

## Vlastni cile

Definuji se pomoci souboru maven.xml
