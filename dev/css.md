---
title: WEB - CSS (Cascading Style Sheets)
---

## Odkazy

[atributy](http://www.jakpsatweb.cz/css/css-vlastnosti-hodnoty-prehled.html)  
[w3schools.com - moc pekne stranky s popisem i prikladama](http://www.w3schools.com/css/css_border.asp)  

====Pouziti:====

```html
&lt;LINK href="special.css" rel="stylesheet" type="text/css"&gt;
```

nebo

```html
&lt;HEAD&gt;
 &lt;STYLE type="text/css"&gt;
   H1 {border-width: 1; border: solid; text-align: center}
pre.code {font-size:8pt;padding:0.5em;border:1px dashed #000;color:Black;overflow:visible;}
#myid {border-width: 1; border: solid; text-align: center}
 &lt;/STYLE&gt;
&lt;/HEAD&gt;
&lt;BODY&gt;
...
&lt;pre class="code"&gt
&lt;h1 id="myid"&gt
...
&lt;BODY&gt;
```

nebo:

```
&lt;P style="font-size: 12pt; color: fuchsia"&gt;
```

## Priklady

<pre style="font-size:8pt;padding:0.5em;border:1px dashed #000;color:Black;overflow:visible|
font-size:8pt;padding:0.5em;border:1px dashed #000;color:Black;overflow:visible
</code>

<pre styyle="font-size:120%;|
font-size:120%;
</code>

<pre style="clear:both;border-top:1px solid #000;padding-left:1em;margin-top:1em;|
clear:both;border-top:1px solid #000;padding-left:1em;margin-top:1em;
</code>

<pre style="vertical-align:super;font-size:80%;|
vertical-align:super;font-size:80%;
</code>

<pre style="vertical-align:super;font-size:80%;font-weight:bold;|
vertical-align:super;font-size:80%;font-weight:bold;
</code>

<pre style="font-size:80%;background-color:#fff;border-spacing:0px;border-collapse:collapse;|
font-size:80%;background-color:#fff;border-spacing:0px;border-collapse:collapse;
</code>

<pre style="display:none;|
display:none;
</code>

<pre style="background:transparent url(/wiki/lib/images/interwiki.png) 0px 1px no-repeat;padding-left:16px;|
background:transparent url(/wiki/lib/images/interwiki.png) 0px 1px no-repeat;padding-left:16px;
</code>

<pre style="background-image:url(/wiki/lib/images/interwiki/wp.gif)|
background-image:url(/wiki/lib/images/interwiki/wp.gif)</code>

<pre style="font-size:140%;border-bottom:none;|
font-size:140%;border-bottom:none;</code>

<pre style="font-size:160%;font-weight:bold;|
font-size:160%;font-weight:bold;</code>

<pre style="color:Black;background-color:transparent;font-family:"Lucida Grande",Verdana,Lucida,Helvetica,Arial,sans-serif;font-size:100%;font-weight:normal;margin-left:0;margin-right:0;margin-top:0;margin-bottom:1em;padding-left:0;padding-right:0;padding-top:0.5em;padding-bottom:0;border-bottom:1px solid #000;clear:left;|
color:Black;background-color:transparent;font-family:"Lucida Grande",Verdana,Lucida,Helvetica,Arial,sans-serif;font-size:100%;font-weight:normal;margin-left:0;margin-right:0;margin-top:0;margin-bottom:1em;padding-left:0;padding-right:0;padding-top:0.5em;padding-bottom:0;border-bottom:1px solid #000;clear:left;</code>

<pre style="border:0;float:left;margin:0 1.5em 0 0;|
border:0;float:left;margin:0 1.5em 0 0;</code>

<ul style="line-height:1.5em;list-style-type:square;margin:0 0 1em 3.5em;padding:0;|
ul: line-height:1.5em;list-style-type:square;margin:0 0 1em 3.5em;padding:0;</ul>

<ol style="line-height:1.5em;margin:0 0 1em 3.5em;padding:0;font-weight:normal;|ol: line-height:1.5em;margin:0 0 1em 3.5em;padding:0;font-weight:normal;</ol>

<ol style="list-style-type:decimal;|
ol: list-style-type:decimal;
</ol>

<ol style="list-style-type:upper-roman;|
ol: list-style-type:upper-roman;</ol>
