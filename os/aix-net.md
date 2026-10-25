# AIX - sitove nastaveni, tcp/ip

#### info

arp testhost ... ukaze ARP zaznam pro testhost  
dig -x 10.217.1.206 ... prelozi ip na jmeno  
entstat -d ent7 ... statistiky hardware karty ent7
hostid
hostname ... jmeno serveru, zmena jmena
entstat -d en1 ... statistiky a nastaveni karty en1
entstat -d ent1 | grep -i link ... Zjisti pripojeni sitoveho kabelu do jineho zarizeni
entstat -d ent1 | grep -i "Logical Port Number" ... Vypise u HEA (IVE) integrovane sitove karty logicke cislo portu  
ifconfig -a ... seznam sitovych zarizeni a jejich sitove nastaveni a stav
lsattr -El inet0 ... Nastaveni internetu - routovani, IP adresa atd.
lsattr -El eth0 ... Nastaveni ovladace 1. sitove karty (IP adresa, podsit, routovani, ...)
lsattr -El en0 ... Nastaveni fyzickeho sitoveho zarizeni  
lscfg -vl en0 ... Informace o vitalnich datech zarizeni - seriove cislo, umisteni atd.  
lsdev -l ent1 -F physloc ... vypise fyzicke umisteni sitove karty  
lsdev -Cc if ... seznam sitovych karet v systemu  
lsfilt ... ukaze IP filtry  
lsof -i ... otevrene porty
lsof -nc midmand ... ukaze otevrene porty prelozene podle /etc/services na midnamnd  
lsof -i tcp:22 ... ukaze ktery process pouziva port 22  
lsslot -c slot | grep -i hea ... vypise vsechny integrovane HEA (IVE) sitove karty  
mktcpip ... vytvori IP adresu pro tento pocitac  
netstat ... network statistics
netstat -in ... mac adresy karet a jejich adresy
netstat -v ent0 ... statistiky karty etn0
netstat -r ... routovaci tabulka
netstat -an|grep LISTEN ... vypis portu, ktere naslouchaji  
netstat -an -f inet ... vypis pouzivanych portu  
netstat -an | grep 162 ... Ukaze, zda je otevreny port 162  
netstat -Aan; echo "sockinfo f100060000cfd398 tcpcb" | kdb |grep proc ... ukaze, ktery program pouziva dany socket (a port)  
nslookup testserver ... prelozi jmeno na IP pomoci DNS serveru\\ar
nslookup testserver ... prelozi jmeno na IP pomoci DNS serveru  
no ... (netvork options) ukazuje a meni nastaveni parametru site
odmget -q"attribute=route" CuAt ... pernamentni routovaci tabulka (ukozena v odm)
rmsock f1000500008243b8 tcpcb ... Ukaze jaky process pouziva dany tcp ip (netstat -Aa)  
route get testhost ... otestuje pres jakou gateway posle server packet na server testhost  
rpcinfo -p ... otevrene porty
tcpdump ... sledovani paketu na sitovych kartach  
tcpdump -i en1 -n -T snmp -w /tmp/tcpdump.out udp port 162  
tcpdump -i en1 -n -T snmp -r /tmp/tcpdump.out udp port 162 | grep 62.187.136.4  
tcpdunp -i en0 host 1.2.3.4 ... Ukazuje pakety mezi pocitacem a adresou 1.2.3.4  
traceroute 1.2.3.4  
tracert 1.2.3.4  

#### start/stop

/etc/rc.tcpip ... stusteni site pri startu

#### konfigurace

chdev -l 'en1' -a alias4=128.0.1.4,255.255.255.0 ... (= smit inetalias) prida alias sitove karty
chdev -l 'en1' -a delalias4=128.0.1.4,255.255.255.0 ... (= smit inetalias) smaze alias sitove karty
chdev -l inet0 -a delroute=net,-netmask,255.255.255.0,62.184.61.0,10.6.11.3 ... smaze pernamentne routu
chdev -l inet0 -a delroute=net,-netmask,,default,10.6.11.3 ... smaze pernamentne default routu
chdev -l 'en0' -a alias4='IP','Net Mask' ... priradi alias IP adresu  
chdev -l 'en0' -alinux delalias4='IP','Net Mask' ... odstrani alias IP adresu  
mktcpip -hostname VIO1 -inetaddr 1.2.3.4 -start -netmask 255.0.0.0 -gateway 1.2.3.1 ... nastavi sitovou konfiguraci  
chdev -dev en3 -attr netaddr=10.0.0.5 netmask=266.0.0.0 state=up ... nastavi dalsi sitovou kartu a adresu  
/etc/resolv.conf ... Nastaveni DNS serveru

#### ether channel - virtualni adapter

lsdev -Cc adapter | grep -i ether ... virtualni adaptery
lsattr -El ent7 ... parametry virtualnich adapteru a prim/sec karty + ping test
lsattr -El ent7 ... parametry Etherchannelu ent7
entstat -d ent7 ... stav karty (link), statistiky, MAC adresa
smitty ethercannel ... konfigurace ethercannel pres smitty
chdev -l eth7 -a backup_adapter=ent5 ... zmeni backup adapter pro etherchannel ent7
ethchan_config ... zmena dalsich parametru pro etherchannel

#### connect

tn (telnet)
ftp

===PROXY===

```
/etc/squid
pdconfig
```


#### Preklad adres na IP

/etc/netsvc.conf ... poradi prekladu adres - lokalni, bind atd  

#### Firewall

lsfilt -a -v4 -O ... vylistuje pravidla. Pokud neexistuje /dev/ipsec4_filt, filtrovani paketu neni zaple  
smitty ipsec4 ... zapne ipsec - packet filtering  
xpfilt -v4 -f /tmp/ip_sec/ -l all -r ... export filtru  
impfilt -v4 -f /tmp/ip_sec/ ... import filtru  
mkfilt -v4 -u
