# WEB - http

Sitovy protokol ktery slouzi hlavne na prenos HTML stranek. Pracuje na TCP protokolu, je typu state-less, navaze spojeni, ziska co chce a ukonci spojeni. HTTP protokol se pripojuje k webovym (http) serverum, jako treba [Apache](/linux/services.html#httpd).
HTTP oddeluje pozadavek (request) od odpovedi (reply) prazdnym radkem.

[HTTP na cs.wikipedia.org](http://cs.wikipedia.org/wiki/Hypertext_Transfer_Protocol)  
[HTTP na en.wikipedia.org](http://en.wikipedia.org/wiki/Http)  
[parametry HTTP hlavicky](http://en.wikipedia.org/wiki/List_of_HTTP_headers)  
[status kody HTTP](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes)  

==Otestovani http sluzby, primitivni ziskani dat z http serveru (http 1.0):==

```
telnet tomas.lipensky.cz 80
GET /
```


==Otestovani http sluzby, http/1.1 minimalni ziskani dat z http serveru:==

```
telnet tomas.lipensky.cz 80
GET / HTTP/1.1
Host: tomas.lipensky.cz
```


==Otestovani http sluzby, http/1.1 minimalni ziskani dat z http serveru:==

```
telnet tomas.lipensky.cz 80
GET / HTTP/1.1
Host: tomas.lipensky.cz
```


==Otestovani http sluzby pres http proxy==

```
telnet proxy.server.com 8080
CONNECT google.com:80 HTTP/1.0
```


==Otestovani http sluzby, http/1.1 minimalni ziskani dat z http serveru:==

```
telnet tomas.lipensky.cz 80
POST / HTTP/1.1
Host: tomas.lipensky.cz
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Accept: text/xml,application/xml,application/xhtml+xml,text/html;q=0.9,text/plain;q=0.8video/x-mng,image/jpeg,image/gif;q=0.2,*/*;q=0.1
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Aplive: 300
Connection: keep-alive

Color=dark&taste=bitter
```


==HTTP Proxy==

```
telnet 1.2.3.4 8080
CONNECT 1.2.3.5:80 GET /
```


##### Dalsi prikazy pro http komunikaci

wget, curl, GET ... viz [Unix - prikazy](/unix/commands.html)
