# BSD

## Externí odkazy

[Load balancing u 2 internetovych pripojeni](http://www.root.cz/clanky/vyuziti-dvou-internetovych-pripojeni-ve-freebsd/)  

## Nastavení síťe

/etc/rc.conf: ifconfig_em0="inet 10.11.12.1 netmask 255.255.255.0 name wan0" ... nastavení síťové karty a přejmenování hned po startu  
ifconfig em0 name wan1 ... přejmenování zařízení  
em0 descr popis ... přidání popisu síťové karty  
setfib ... umí rozdělit síťovou zátěž  
ipfw list ... výpis firewallu  
ipfw nat 1 config ip 10.11.12.1 unreg_only  
ipfw add 5000 nat 1 all from any to any via em0 * nat ... konfigurace nat, * poznamka  
sysctl net.fibs ... Ukáže počet podporovaných routovacích tabulek
