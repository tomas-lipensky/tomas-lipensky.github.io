# CISCO

#### Obsah:

<dl>
<dd>[Mody:](#mody)</dd>
<dd>[uzivatelsky](#mo-user)</dd>
<dd>[privilegovany](#mo-priv)</dd>
<dd>[konfiguracni](#mo-conf)</dd>
<dd>[Router:](#router)</dd>
<dd>[Smerovani](#ro-route)</dd>
<dd>[Firewall](#ro-firewall)</dd>

<dd>[NAT](#ro-nat)</dd>
<dd>[VLANy na routeru](#ro-vlan)</dd>
<dd>[WAN](#ro-wan)</dd>
<dd>[Switch:](#switch)</dd>
<dd>[porty](#sw-port)</dd>
<dd>[STP](#sw-stp)</dd>
<dd>[VLANy](#sw-vlan)</dd>
<dd>[firewall](#sw-firewall)</dd>
<dd>[IPv6](#ipv6)\\</dd>

</dl>

#### Okazy

[Cisco IOS](http://www.samuraj-cz.com/serie/cisco-ios/)  
[Pocitacove site](http://www.samuraj-cz.com/serie/pocitacove-site-computer-networks/)  
[Priprava na CCNA](http://www.samuraj-cz.com/clanek/priprava-na-cisco-ccna/)  
[GNS](http://www.gns3.net/download) - Graphical Network Simulator - graficka simulace site, konfigurace routeru  

<a name="mody|]]
## Mody

<a name="mo-user|]]
#### uzivatelsky EXEC mod

disconnect 4 ... prerusi telnetove spojeni c. 4  
<b>en</b> (enable) ... prepnuti do privilegovaneho modu  

logout ... odpojeni ze systemu  
ping ip 192.168.2.1 ... pingne ip adresu 192.168.2.1  
resume 4 ... obnovi telnetove spojeni c. 4  
sh arp ... ukaze routovaci tabulku  
sh cdp neighbors detail ... ukaze CDP (Cisco Discovery Protocol) sousedy a jejich IP  
sh cdp traffic  
sh cdp entry *  
sh controllers s1/0 ... podrobne informace o zarizeni Serial 1/0  
sh flash ... ukaze obsah flash pameti  

sh hist (show history) ... ukaze historii  
sh hosts ... ukaze preklady jmen na IP  
sh int (show interface) ... seznam adapteru i s parametrama  
sh ip arp ... ukaze arp tabulku  
sh ip eigrp neighbors ... ukaze eigrp sousedy  
sh ip eigrp topology ... ukaze eigrp topologii  
sh ip ospf ... ukaze nastaveni OSPF routovani  
sh ip ospf database ... ukaze databazi routeru v OSPF databazi  
sh ip ospf interface f0/1 ... ukaze OSPF informace tykajici se FastEthernet0/1 zarizeni  

sh ip ospf neighbor ... ukaze OSPF sousedy  
sh ip protocols ... informace o zarizenich, routach atd.  
sh ip route ... ukaze routovaci tabulku  
sh ip route eigrp ... ukaze eigrp routovaci linky  
show ip interface brief  
sh memory  
sh processes ... ukaze bezici procesy na Cisco  
sh run (show running-config) ... ukaze aktualni nastaveni routeru  
sh run | begin interface ... ukaze aktualni nastaveni zacinajici prvnim slovem interface  

sh run | include 1.2.3.4 ... ukaze radky obsahujici text 1.2.3.4  
sh term (show terminal) ... ukaze nastaveni terminalu  
sh sessions ... ukaze vsechny pripojeni na switch, Ctrl_Shift+F6 - docasne prerusi spojeni, ctrl-z ukonci spojeni  
sh start (show startup-config) ... ukaze startovaci nastaveni  
sh users ... ukaze pripojene uzivatele  
sh ver (show version) ... ukaze verzi IOS, pamet, ...  
show protocols  
telnet 192.168.2.1 ... navazani telnetoveho spojeni  
terminal history size 25 ... zmeni historii terminalu  

traceroute ip 192.168.2.6  

<a name="mo-priv|]]
#### Privilegovany mod

<b>vse co v EXEC (normalnim) modu + nasledujici prikazy:</b>  
clock set 11:15:11 25 aug 2010 ... nastavi cas a datum  
clear line 4 ... zrusi aktivni vty linku 4  
copy run start ... zkopiruje aktualni konfiguraci do startovaci  

conf t (config terminal) ... prejde do konfiguracniho modu  
debug all ... ukazuje vsechny udalosti  
debug eigrp packet ... ukazuje eigrp pakety  
debug interface serial ... debuguje seriove linky  
debug ip rip ... pokud je aktivovany debug mod  
debug ip eigrp  
debug ip eigrp packet  
debug ip eigrp notification ... ukazuje zmeny eigrp  
debug ip ospf packet  

debug ip ospf hello  
debug ip ospf adjacency  
del nvram:start-config  
del vlan.dat ... smaze u switche informace o vlanech  
dir nvram:  
dir flash:  
disable ... navrat z privilegovaneho modu  
reload ... udela studeny restart celeho zarizeni  
terminal monitor ... aktivuje debug mod  

un all (undebug all) ... vypne terminal monitor  

<a name="mo-conf|]]
#### konfiguracni mod

banner motd # Ahoj, vitej # ... nastavi uvitaci hlasku  
boot system tftp ... nastavi bootovani z tftp  
clear counters ... vynuluje pocitadla interfejsu  
config-register x2101 ... zmeni startovaci [registr](registry.txt)  

crypto key generate rsa general-keys modulus 1024 ... vytvori SSH klic  
do show int ... ukaze interfejsy i z konfiguracniho modu  
enable password HESLO ... nastavi heslo HESLO pri vstupu do privilegovaneho modu  
enable secret HESLO ... nastavi zasifrovane heslo HESLO pri vstupu do privilegovaneho modu  
ip domain-name lipensky.cz ... nastavi jmeno domeny  
ip domain-lookup ... nastavi hledani jmena vcetne domeny  
ip host R1 1.2.3.4 ... nastavi preklad jmen pro R1  
ip http server ... aktivace SDM (Security Device Manager)  
ip http secure-server ... aktivace klice pro ssl spojeni  

ip http authentication local ... nastavi autentifikace, pote je treba vytvorit uzivatele - username  
ip name-server 1.2.3.5 ... nastavi adresu DNS serveru  
ip subnet-zero ... umozni pouzivat pod-site (pod A, pod B, pod C)  
ip ssh authentication-retries 2 ... pocet pokusu na prihlaseni  
ip ssh time-out 60 ... nastaveni timeout pro ssh  
hostname JMENORouteru ... nastaveni promptu  
int (interface) ... nastaveni adapteru  
int loopback 0 ... zastaveni loopback (testovaciho) zarizeni  
int s0/0/0 ... nakonfiguruje seriovy port (serial)  

int s0/0/0; ip address 1.2.3.4 255.255.255.0 ... priradi IP adresu a sit  
int s0/0/0; ip address 1.2.4.4 255.255.255.0 secondary ... priradu druhou IP adresu  
int s0/0/0; clock rate 1000000 nastavi 1000000 bps  
int s0/0/0; bandwitch 265000 ... nastaveni prutoku u Serioveho portu v kilobitech  
int s0/0/0; delay 300000  
int e0/0 ... nastaveni Ethernet0/0  
int fa0/0; no shutdown ... povoli pouzivani FastEthernet portu  
int fa0/0; description SALES LAN ... nastaveni popisu zarizeni fast ethernet 0/0  
int range f0/3-4 ... nastaveni vice zarizeni najednou  

line aux; password AUX ... nastavi heslo AUX pri pouziti portu AUX  
line console 0; login ... povoli login pres konzoli  
line console 0; password CONSOLE ... nastavi heslo CONSOLE pri pouziti loginu z postu console  
line vty 0 1180; transport input ssh telnet ... nastaveni telnetu a ssh pri pripojeni pres terminal  
line vty 0 1180; access-list 1 ... aktivace ACL pro telnet pristup  
service password-encryption ... nastavi kodovani hesel, aby nebyly videt v sh run  
no service password-encryption ... vypne kodovani hesel  
username cisco privilege 15 password 0 cisco ... vytvori uzivatele cisco s heslem cisco pro CDP  

<a name="router|]]
## Router - smerovac

<a name="ro-route|]]
#### routing - smerovani

<h6>Staticky (AD =1)</h6>
ip 0.0.0.0 0.0.0.0 1.2.3.4; ip classless ... defaultni route  

ip route 1.2.3.0 255.255.255.0 1.2.3.4 ... konfigurace staticke routy pro sit 1.2.3.0/24 na router 1.2.3.4  
ip default-network 1.2.3.4; ip classless ... defaultni route  
<h6>EIGRP (AD = 90)</h6>
router eigrp 10 ... Nastavovani EIGRP routovani, AS (autonomous system 10)  
router eigrp 10; network 10.0.0.0 ... nastavi eigrp na site 10.0.0.0  
router eigrp 10; passive-interface serial 0/1 ... nastavi seriovy port jako pasivni - nevysila, ani neprijma EIGRP data  
router eigrp 10; redistribute rip metric 1000000 20000 255 1 1500 ... redistribuje RIP tabulku do EIGRP pomoci nadefinovane metriky  
router eigrp 10; maximum-paths 6 ... nastaveni maximalniho poctu ruznych cest na 6 ze 4  
router eigrp 10; maximum-hops 140 ... zvysi maximalni pocet skoku pri routovani z 100 na 140  

router eigrp 10; no auto-summary ... bez auto-summary (distribuuje podsite mezi 2 routry)  
ip summary-address eigrp 10 192.168.10.64 255.255.255.224 ... nastavi podsit, takze se pozivaji podsite, ne site  
<h6>OSPF (Open shortest path first) (AD = 110)</h6>
router ospf 1 ... Nastavovani Open Shortest Path First routovani (cislo procesu 1)  
router ospf 1; network 10.0.0.0 0.127.255.255 area 0 ... bude se distribuovat sit 10.0.0.0/9 v oblasti 0  
roiter ospf 1; area 1 range 192.168.10.64 255.255.255.224 ... nastavi podsit misto pouzivani cele site  
int s0; ip ospf priority 2 ... zmeni prioritu zarizeni pri volbe Designated Router (DR) a Backup DR (BDR)  
<h6>RIP (AD = 120)</h6>
router rip ... nastavovani RIP routovani  

router rip; network 10.0.0.0 ... bude se distribuovat sit 10.0.0.0  
router rip; version 2 ... Nastaveni RIPv2  
router rip; redistribute eigrp 10 metric 1 ... redistribuce eigrp AS 10 na RIP s metrikou 1  
router rip; passive-interface s0 ... nastavi, ze Serial0 nebude vysilat update, ale jen prijimat  
no router rip ... zakaze rip  

<a name="ro-firewall|]]
#### firewall

<b>standartni 1-99, 1300-1999</b>  
access-list 10 deny host 172.16.30.2 ... zakaze prichozi pakety z 172.16.30.2  
access-list 10 deny 172.16.30.3 ... zakaze prichozi pakety z 172.16.30.3  
access-list 10 deny 172.16.32.0 0.0.15.255 ... zakaze prichozi pakety z 172.16.32.0/20  
access-list permit any ... povoli vse  
access-list permit 0.0.0.0 255.255.255.255 ... povoli vse  
int Ethernet 0 ... nastavovani Ethernet 0  
int Ethernet 0; ip access-group 10 out ... aplikuje firewall pravidlo 10 na vystup  
<b>extended - rozsireny 100-199, 2000-2699</b>  

access-list 110 deny tcp any host 1.2.3.4 eq 23 log ... zakaze pakety odkudkoli na 1.2.3.4 na port 23. Loguje se  
access-list 110 permit ip any any ... povoli vse  
int fa0/0; access-group 110 in ... aplikuje se pravidlo 110 na prichozi pakety  
<b>jmenne</b>  
ip access-list standard RULE1 ... vytvori pojmenovane pravidlo  
ip access-list standard RULE1; deny 1.2.3.4 ... zakaze zdrovove pakety z 1.2.3.4  
ip access-list standard RULE1; permit any ... povoli ostatni  
int e3;ip access-group RULE1 out ... aplikuje pravilo RULE1 na vystupu Ethernet 3  
<b>casove</b>  

time-range ho-http  
time-range ho-http; periodic weekend 06:00 to 12:00  
ip access-list extended Time-http  
ip access-list extended Time-http; remark tcp 1.2.3.4 any eq www time-range no-http ... zaznamena pristupy z 1.2.3.4  
ip access-list extended Time-http; deny tcp any any eq www time-range no-http  
ip access-list extended Time-http; permit any any  
int e2; ip access-group Time-http; ... aplikuje pravidlo Time-http na e2  
do sh access-list ... ukaze seznam pravidel  
do sh access-list 10 ... ukaze access-list 10  

do sh ip access-list  

<a name="ro-nat|]]
#### NAT - Network Address Translation

ip nat inside source static 10.1.1.1 170.46.2.2 ... nastavi staticky NAT  
int e0; ip address 10.1.1.10 255.255.255 nastavi adresu  
int e0; ip nat inside  
int s0; ip address 170.46.2.1 266.266.266.0  

int s0; ip nat outside  

ip nat pool todd 170.168.2.2 170.168.2.254 netmask 255.255.255.0 ... dynamicky NAT  
ip nat inside source list 1 pool todd  
access-list 1 permit 10.1.1.0 0.0.0.255  
int e0 address 10.1.1.10 255.255.255.0  
int e0; ip nat inside  
int s0; ip address 170.168.2.1 255.255.255.0  
int s0; ip nat outside  

ip nat pool POOL2 170.168.2.1 170.168.2.1 netmask 255.255.255.0 ... dynamicky PAT  
ip nat inside source list 1 pool POOL overload  
access-list 1 permit 10.1.1.0 0.0.0.255  
int e0 address 10.1.1.10 255.255.255.0  
int e0; ip nat inside  
int s0; ip address 170.168.2.1 255.255.255.0  
int s0; ip nat outside  
do sh nat translation  

do debug ip nat  

<a name="ro-vlan|]]
#### vlany na routeru

int fa0/1; ... nastavovani fa0/1  
int fa0/1; no ip address ... zadna IP adresa  
int fa0/1; no shutdown ... zarizeni zapneme  
int fa0/1; int f0/1.1 ... udelam podzarizeni  

int fa0/1; int f0/1.1; encalupsation dotq1 ... trunk ve standartu 802.1Q  
int fa0/1; int f0/1.1; ip address 192.168.10.129 255.255.255.240 ... IP adresa podzarizeni  
int fa0/1; int f/1.2 ...  
int fa0/1; int f/1.2; encalupsation dot1q ...  
int fa0/1; int f/1.2; ip address 192.168.10.46 255.255.255.240 ...  

<a name="ro-wan|]]
#### WAN

<h6>HDCL (High-Level Data-Link Control protocoL</h6>
int s1/0; encalupsation hdlc  
<h6>PPP</h6>
hostname R1  
username R2 password HESLO ... nastavi jmeno routeru partnera a heslo  
int s0  
int s0; encalupsation ppp ... nastavi uzavirani paketu typu PPP  
int s0; ppp authentication chap pap ... nastavi CHAP authentikaci, pokud partner nema, tak PAP authentikaci  

debug ppp authentication ... ukazuje ppp autentifikacni pakety  
<h6>PPPoE</h6>
int f0/0  
int f0/0; pppoe enable group global  
int f0/0; pppoe-client dial-pool-number 1  
int f0/0; ip address negotiated  
int f0/0; ppp authentication chap callin  
int f0/0; ppp chap hostname R2  
int f0/0; ppp password 0 HESLO  

<h6>Frame Relay - jedno zarizeni</h6>
int s0  
int s0; encalupsation framerelay (ietf) ... nastavi obalovani paketu Frame Relay (ietf kdyz partner neni Cisco)  
int s0; interface-dlci 101 ... nastavi DLCI (data link connection identifiers) na 101  
int s0; frame-relay lmi-type cisco ... nastavi LMI (Local Management Interface) na cisco  
do sh frame pvc  
do sh frame lmi ... lmi statistiky  
do sh frame map  
do debug frame-relay lmi  

<h6>Frame Relay - jedno zarizeni</h6>
int s0  
int s0; encalupsation framerelay (ietf) ... nastavi obalovani paketu Frame Relay (ietf kdyz partner neni Cisco)  
int s0; int s0.16 point-to-point ... nastavi podinterfejs  
int s0; int s0.16 point-to-point; ip address 1.2.3.4 255.255.255 ... nastavi ip adresu  
int s0; int s0.16 point-to-point; interface-dlci 16 ... nastavi DLCI na 16  
int s0; int s0.16 point-to-point; no ip directed-broadcast  
int s0; int s0.104 point-to-point ... nastavi podinterfejs  
int s0; int s0.104 point-to-point; ip address 1.2.4.4 255.255.255 ... nastavi ip adresu  

int s0; int s0.104 point-to-point; interface-dlci 104 ... nastavi DLCI na 16  
int s0; int s0.104 point-to-point; no ip directed-broadcast  
do sh frame-relay pvc  
<h6>Frame Relay Switch</h6>
frame-relay switching  
int s0/0  
int s0/0; encalupsation frame-relay  
int s0/1  
int s0/1; encalupsation frame-relay  

int s0/0  
int s0/0; frame intf-type dce ... nastavi zarizeni na DCE (Data Communication equipment)  
int s0/0; frame-relay route 102 interface Serial0/1 201  
int s0/0; clock rate 64000  
int s0/1  
int s0/1; frame intf-type dce ... nastavi zarizeni na DCE (Data Communication equipment)  
int s0/0; frame-relay route 201 interface Serial0/0 102  
int s0/0; clock rate 64000  
<h6>ISDN</h6>

(config)# dialer-list 1 protocol ip permic ... definice datovych toku pro isdn  
(config)# access-list 1 all  
(config)# int br0  
(config-if)# dialer-group 1 ... aktivace ACL na interfejsu  

<a name="switch|]]
## Switch - prepinac

sh int trunk ... ukaze vsechny trunk porty  
sh mac- | i Po1 ... ukaze MAC adresy na intefejsu Po1 (Port channel - Ether channel - Agregations)  
sh mac- | i d813 ... Ukaze MAC adresu v ARP tabulce, ktera obsahuje D8:13  
sh mac address ... ukaze switchovaci tabulku  
show mac-address-table | include Fa0/16  
sh port-security interface f0/6  
sh parser macro ... ukaze dafinice maker  
sh parser macro brief ... ukaze seznam maker  

sh run in G0/34 ... Ukaze aktualni nastaveni interfejsu G0/34  
sh spanning-tree ... ukaze to STP (spanning tree protokol - zabranuje smyckam)  
sh spanning-tree uplinkfast ... uplinkFast statistiky  
sh spanning-tree backbodefast ... backbodeFast statistiky  
sh vlan 1  
sh vlan brief ... ukaze seznam vlanu  
sh vtp status ... ukaze status VTP  
ip default-gateway 1.2.3.4 ... nastavi defaultni routu - jen pro switch  

<a name="sw-port|]]
#### nastavovani portu

int f0/1 ... nastaveni fastethernet0/1 portu  
int f0/1; switchport port-security mac-address sticky ... uci se mac adresy  
int f0/1; switchport port-security maximum 1 ... maximum mac address k f0/1 portu je 1  
int f0/1; switchport port-security violation shutdown ... v pripade poruseni pravide vypne port  
mac-address-table static aaa.bbbb.cccc vlan 1 int fa0/5 ... nastavi statickou MAC adresu  

<a name="sw-stp|]]
#### STP - Spaning-tree protocol

spanning-tree vlan 1 priority 4096 ... nastavi prioritu switche ve vlan 1 na 4096 pro volbu korenoveho switche  
spanning-tree vlan 1 root primary ... nastavi switch jako root switch v STP  
spanning-tree vlan 2 ... zapne ST pro VLAN 2  
no spanning-tree vlan 3 ... vypne ST pro VLAN 3  
spanning-tree mode pvst ... nastavi mod STP PVST (per VLAN Spanning-Tree - STP po jednotlivych VLANech)  

spanning-tree portfast default ... nastaveni portfast pro vsechny porty  
int range FastEthernet 0/1 - 13; spanning-tree portfast ... nastavi se portfast (ne switch ale koncove zarizeni) na 12 FastEthernet portech  
int f0/1; spanning-tree uplinkfast ... Pri vypadku Root Portu okamzite zapne zalozni linku - rychlejsi konvergence v pripade vypojeni jednoho spojeni  
int f0/1; spanning-tree backbonefast ... rychlejsi update STP v pripade vypojeni neprimeho spojeni spojeni  
int f0/1; spanning-tree mode rapid-pvst ... RSTP (802.1w)  
int f0/1; spanning-tree bdpuguard enable ... hlida fortfast port - kdyz dojde BPDU, tak se port vypne  
int f0/1; spanning-tree bdpufilter enable ... hlida portfast portu. Pokud prijde BDPU, tak se na portu vypne portfast  
int f0/2; spanning-tree port-priority 48 ... nastavovani priority portu (podle toho se vybere designated/root port, ostatni jsou non-designated)  
int f0/2; spanning-tree vlan 3 port-priority 48 ... nastavovani priority portu (podle toho se vybere designated/root port, ostatni jsou non-designated) pro vlan 3  

int f0/2; spanning-tree guard root ... nastavi kontrolu root portu. Pokud si novy root bridge vynuti zmenu na designated, pak se port zakaze  
show spanning-tree ... zobrazi informace o spanning-tree pro kazdou VLAN  
show spanning-tree vlan 2... zobrazi informace o spanning-tree pro VLAN 2  
show spanning-tree uplinkfast  
show spanning-tree backbodefast  
show spanning-tree summary ... strucne informace o STP  
show spanning-tree detail ... detailní info o STP  
show spanning-tree interface f0/1 ... info o STP pouze pro daný interface  
show spanning-tree bridge detail ... stru&#269;né p&#345;ehled STP instancí  

int port-channel 1 ... nastavi ethernet channel  
int port-channel 1; int range f0/1-2 ... nastavi f0/1 a f0/2 na etherchannel  
int port-channel 1; int range f0/1-2; switchport mode trunk ... nastavi trunk mode  
int port-channel 1; int range f0/1-2; switchport mode nonegotiate ... vypne vyjednavani o spojeni a trunku  
int port-channel 1; int range f0/1-2; channel-group 1 mode desirable  
do sh int fa0/1 etherchannel ... ukaze nastaveni etherchannelu  

<a name="sw-vlan|]]

#### VLAN - Vurtual LAN

vlan 2 ... nastavi vlan 2  
vlan 2; name Sales ... pojmenuje vlan 2  
int f0/0; switchport access vlan 2 ... povoli pristup z f0/0 jen na vlan 2  
int f0/1; switchport mode trunk ... povoli trvale trunk mode pro f0/1  
int f0/1; switchport mode nonnegotiate ... nikdy nevyjednava. Lze pouzit na access, nebo trunk port  
int f0/1; switchport mode access ... nastavi f0/1 na nontrunk a premlouva partnery, aby take byli nontrunk  
int f0/1; switchport mode dynamic auto ... je nontrunk a kdyz soused nabidne trunk, tak se konvertuje na trunk  

int f0/1; switchport mode dynamic desirable ... je nontrunk, ale premlouva ostatni, aby spolu konvertovali na trunk  
int f0/1; switchport trunk allowed ... povoli trunk mod - zasilani vlan informaci  
int f0/1; switchport trunk pruning vlan 3-4 ... povoli trunk mod jen na vybrane vlany  
int f0/1; switchport trunk encapsulation dot1q ... prepne trunk mod na 802.1Q  
int f0/1; switchport trunk encapsulation isl ... prepne trunk mod na ISL  
int f0/1; switchport trunk allowed vlan add 2-5 ... prida  do povolenych vlanu 2-5  
int f0/1; switchport trunk allowed vlan all ... prida  do povolenych vlanu vse  
int f0/1; switchport trunk allowed vlan none ... zrusi do povolene vlany  
int f0/1; switchport trunk allowed vlan remove 2-5 ... odebere z povolenych vlanu 2-5  

int f0/1; switchport trunk native vlan 40 ... zmeni administrativni vlan z 1 na 40  
int f0/1; no switchport trunk native vlan ... zrusi administrativni vlan a bude ted vlan 1  
vtp mode server ... nastavi VTP (vlan trunk protokol) na switchi na server  
vtp mode client ... nastavi VTP na klienta  
vtp domain AAA ... nastavi jmeno domeny  
vtp password HESLO ... nastavi heslo  
do show vlan  
do show vtp password ... ukaze heslo  
do show vtp status ... ukaze nastaveni VTP  

do sh trunk  

<a name="sw-firewall|]]
#### switch firewall

mac access-list extended RULE2 ... vytvori RULE2  
mac access-list extended RULE2; deny any host 000d.29bd.4b85 ... zakaze tok na definovanou MAC  
mac access-list extended RULE2; permit any any ... povoli vse ostatni  
do show access-list ... ukaze access-listy  

do show access-group  
int f0/6; mac address-group RULE2 ... aplikuje RULE2 na f0/6  

<a name="ipv6|]]
## IP verze 6

int f0/1; ipv6 enable ... zapne ipv6 pro f0/1  
ipv6 dhcp pool test ... nadefinuje dhcp server  

ipv6 dhcp pool test; domain-name priklad.cz ... nadefinuje jmeno domeny  
ipv6 dhcp pool test; prefix-delegation pool test lifetime 3600 3600 ... nastavi lifetime  
int fa 0/0; ipv6 dhcp server test ... aktivuje nadefinovany dhcp server  
ipv6 router rip 1 ... aktivuje RIPng, proces 1  
int f 0/0; ipv6 rip 1 enable ... nastavi RIPng pro Fastethernet 0/0  
ipv6 router eigrp 10 ... aktivuje EIGRPv6 AS=10 (Autonomni system)  
ipv6 router eigrp 10; no shutdown ... spusti EIGRPv6  
int f 1/0; ipv6 eigrp 10 ... aktivuje EIGRPv6 pro AS 10  
ipv6 router ospf 10 ... aktivuje OSPFv3, proces cislo 10  

ipv6 router ospf 10; router-id 1.1.1.1 ... nastavi cislo OSPFv3 routeru  
int f 1/1; ipv6 ospf 10 area 0.0.0.0 ... aktivuje OSPFv3, oblast 0, pro zarizeni f 1/1  
ipv6 unicast routing ... povoli  IPv6 forwarding  
int f 0/0; ipv6 address 2001:bd8:3c4d:1::/64 eui-64 ... nastavi IPv6 adresu, zbytek doda automaticky podle MAC adresy f0/0  
int tunnel 0 ... vytvori tunel  
int tunnel 0; ipv6 address 2001:bd8:1:1::/64 ... priradi IPv6 adresu tunelu  
int tunnel 0; tunnel source 192.168.30.1 ... priradi ip adresu tunelu  
int tunnel 0; tunnel destination 192.168.30.2 ... nastavi cil tunelu  
int tunnel 0; tunnel mode ipv6ip ... nastavi ip6to4 typ tunelu
do sh ipv6 protocols  

do sh ipv6 rip  
do sh ipv6 route  
do sh ipv6 ospf neigbor  
do debug ipv6 rip  
do debug ipv6 ospf packer  
un all ... vypne debug  
do debug ospf hello
