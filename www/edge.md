---
title: Edge
---

dscontrol highavailability status ... status loadbalanceru  
dscontrol highavailability takeover ... prepnuti sluzby loadbalanceru na druhy node (active &gt; pasive, pasive &gt; active)  
dscontrol manager status ... status Edge managera  
ps -ef com.ibm.internet.nd.server.SRV_KNDConfigServer ... Tento proces ma jet na active node LoadBalanceru  
dscontrol manager report ... report loadbalancivani - ktere destinace jsou aktivni atd.  
dscontrol executor report ... Statistiky loadbalancovani  
dscontrol cluster status b2c-2010 ... status jednotliveho clusteru  
dscontrol logstatus ... info o logu  
dscontrol manager status ... info o logu managera  
dscontrol port status b2c-2010:443 ... status portu  
dscontrol server status b2c-2010:443:cws08 ... status serveru  
dscontrol server down b2c-2010+vip6:80+443:cws08 ... oznaci server, ze je dole  
dscontrol server up b2c-2010+vip6:80+443:cws08 ... oznaci server, ze je zase v provozu  
cd  /opt/ibm/edge/lb/servers/configurations/dispatcher/; dscontrol file save configuration-au-aaaa-mm-jj ... backup konfigurace (po pridani,vyjmuti serveru, clusteru nebo VIP se doporucuje restart)  
/opt/ibm/edge/lb/servers/configurations/dispatcher/default.cfg ... konfiguracni soubor  
dscontrol file newload default.cfg ... nacte zmeny v konfiguraci
