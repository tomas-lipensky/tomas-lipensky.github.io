---
title: JVM a prepinace
---

1.Dhttp.proxyHost=webcache.mydomain.com ... nastaveni http proxy serveru  
2.Dhttp.proxyPort=8080 ... nastaveni http proxy portu  
3.DsocksProxyHost=socks.mydomain.com ... nastaveni socks proxy serveru jako vychozi komunikacni prostredek  
4.DsocksProxyPort=1080 ... nastaveni socks proxy portu  

java [-Xdump:help](http://www-01.ibm.com/support/docview.wss?uid=swg21242497) ... help k prepinaci -Xdump  

1.[Xdump](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/tools/dump_agents.html):java+heap+system+snap:events=user ... nastavi JVM ze pri signalu se vytvori java core dump, system core dump, heap dump a snap dump  
kill -3 PID ... s predchozi konfiguraci se da signal JVM a vytvori se dumpy  
dump /f soubor ... Na Windows po stazeni WinDbg lze udelat to same  
$JAVA_HOME/jre/bin/jextract systemcoredumpsoubor ... zprocesuje vytvoreny dump. Ten se da pak poslat na SW support
