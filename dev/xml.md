# WEB - xml, DTD, XSLT

## XML

eXtensible Markup Language

### XML dokument

&lt;?xml veraion="1.0"?&gt; ... specifikace XML verze  

## XSL

[xsl](http://www.w3.org/Style/XSL/) - eXtensible Stylesheet Language - transformace xml

xsltproc [test.xsl](xml/test.xsl) [test.xml](xml/test.xml) ... transformace xml podle vzoru  

### DTD

### XML

cat a.xml | xmllint --xpath "string(//*[name()='ManagedObjectReference'])" - ... vypise hodnotu uzlu ManagedObjectReference  
cat a.xml | xmllint --xpath "string(//*[name()='ManagedObjectReference'][$i]/@type)" - ... vypise prepinac "type" z i-teho uzlu ManagedObjectReference  

## XSLT

[XLST tutorial na w3schools](https://www.w3schools.com/xml/xsl_intro.asp)  
[XLST info na whoishostingthis](http://wiht.link/XSLT-intro)

##### Konverzni programy

xsltproc
saxon
4SXLT
Xalan

eXtensible Stylesheet Language Transformations ... cast specifikace XSL pro transformace XML do jinych formatu (XML, HTML, txt, csv, pdf, ...)

##### Hlavicka

&lt;?xml veraion="1.0"?&gt; ... specifikace XML verze, pripadny parametr encoding (UTF-8, windows-1250, ...) pro kodovani znaku  
&lt;xsl:stylesheet version="1.0" xmlns="http://www.w3.org/1999/XSL/Transform"&gt; ... Specifikace XSLT  
&lt;xsl:stylesheet type="text/css" href="first.css"&gt; ... Specifikace kaskadoveho stylu  

##### Telo - obvykle prikazy

&lt;xsl:template match="/PLANETS"&gt; ... vzor pro vsechny nalezene bloky PLANETS v korenu  
&lt;xsl:template match="PLANET"&gt; ... vzor pro vsechny nalezene bloky PLANET v aktualnim bloku  

&lt;xsl:value-of select="NAME"/&gt; ... Vlozi obsah podbloku NAME  
&lt;xsl:value-of select="."/&gt; ... Vlozi obsah aktualniho bloku  
&lt;xsl:value-of select="@COLOR"/&gt; ... Vlozi obsah argumentu COLOR u aktualniho bloku (.) - napriklad pro &lt;PLANET COLOR="red" NAME="MARS"&gt;  

&lt;xsl:apply-templates&gt; ... Instrukce pro nalezeni vhodneho vzoru (template) a jeho implementaci  
&lt;xsl:apply-templates select="DISTANCE"&gt; ... Instrukce pro nalezeni vzoru (template) DISTANCE a jeho implementaci  

&lt;xsl:text&gt; ... Vlozi dany text (mezery, tabulatoru atd.)  
&lt;xsl:text disable-output-escaping="yes"&gt;&amp;!lt;DOCTYPE html PUBLIC "*W3C*DTD XHTML 1.0 Transitional//EN"&amp;gt;  ... Vlozi dany text pricemz preklada &amp; znaky  

&lt;xsl:output indent="yes"&gt; ... definice vystupu - vystupni hodnoty budou odsazeny podle bloku  
&lt;xsl:output method="xml"&gt; ... definice vystupu - vystupni hodnoty budou v jazyce (specifikaci) XML - vytvori hlavicku verze XML  

##### Telo - specialni vyrazy

&lt;xsl:copy&gt; ... zkopiruje (vypise) aktualni uzel (viz. [copy.xsl](xsl/copy.xsl))  
&lt;xsl:strip-space elements="*"&gt; ... smaze vsechny prazdne uzly (viz. [copy.xsl](xsl/copy.xsl)) a smaze prebytecna bila mista (tabulatory, mezery, nove radky)  
&lt;xsl:preserve-space elements="MASS DISTANCE"&gt; ... zanechan vsechny prazdne uzly a bila mista (prebije strip-space pro dane uzly) u uzlu MASS a DISTANCE  

## XPath

[XPath na w3schools](http://www.w3schools.com/xsl/xpath_intro.asp) ... prochazeni a filtrovani XML  

## XQuery

[XQuery na w3schools](http://www.w3schools.com/xsl/xquery_intro.asp) ... vyhledavani v XML jako v SQL (for $x in doc("books.xml")/bookstore/book where $x/price&gt;30 order by $x/title return $x/title
