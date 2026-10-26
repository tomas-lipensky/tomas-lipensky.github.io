---
title: Mobilni aplikace
---

## Externi odkazy

[Linuxjournal.com - Developing Portable Mobile Web Applications](http://www.linuxjournal.com/article/10789?page=0,1), [Zdrojovy kod](ftp://ftp.linuxjournal.com/pub/lj/listings/issue197/10789.tgz)  

## Jednoducha webova aplikace z Linuxjournalu, viz Externi odkazy

napsani prenosne javove aplikace mezi systemy (iPhone, iTab, Android) neni snadne. Pro kazdy typ prenosneho zarizeni se aplikace musi vyvijep pod zvym vlastnim vyvojovym prostredi - SDK.
Lze vsak vytvorit monilni aplikace jako HTML stranky + Javaskriptovy ovladaci prvek (MVC - Model View Controler koncept), jelikoz HTML5 jiz podporuje mnoho funkci, jako treba zapis dat,
geolokace, stav baterie atd. Jednotlive mobilni zarizeni pouzivji ruzny engine ve webovem prohlizeci, ale oboji - iPhone/iTab a Android uzivaji [WebKit](http://iwebkit.net) (i kdyz ruznych verzi). Jednotny vzhled zajisti
knihovna [jQTouch](http://www.jqtouch.com), zapis se provadi pomoci SQLite.  
Vysledna aplikace se bud zabali SDKckem do formy aplikacniho balicku, nebo se z aplikace udela tzv. HTML5 Offline Application a to tak, ze se prida do znacky &lt;html&gt; atribut **manifest="webnotes.manifest"**.
Pokud se umisti aplikace na Web, pak se do nastaveni Apache Httpd serveru prida **AddType text/cache-manifest .manifest**.

[index.html](mobilap1/index.html)  
[javascript/webnotes.js](mobilap1/webnotes.js)
