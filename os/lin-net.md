# LINUX - Site, sitove nastaveni

### Obsah

Konfiguracni soubory  
Nastaveni sitoveho provozu  
Bezdratova sit  
Modem a GRPS/EDGE/4G pripojeni  
Etherchannel = bonding  
Testovani provozu, prohlizeni site, ...  
IPv6  
NAT a routing  
Kernel a ovladace zarizeni pro sitove zarizeni  
Bezpecnost - Firewall  
Programy a nastroje pro komunikaci  
Network Manager  

#### Konfiguracni soubory

/etc/sysconfig/network/[ifcfg*](etc-ifcfg)  
/etc/sysconfig/network/config  
/etc/hosts  
/etc/resolv.conf (8.8.8.8 - Google DNS, 208.67.222.222, 208.67.222.220 - OpenDNS)  
/etc/nsswitch.conf ... nastaveni Name serwice switch - odkuz se prekladaji adresy na IP atd  
/etc/modprobe.conf ... konfigurace modulu vcetne tg3 - modul sitove karty  
/etc/rc.d/rc.local ... startovani sitovky po startu  
echo "alias net-pf-10 off\nalias ipv6 off" > /etc/modprobe.conf ... zakaze pouzivani IP6  
/etc/network/interface ... nove nastaveni site (Ubuntu 18.04)  
/etc/netplan ... nastaveni sitovych karet  
[systemd-resolve](https://wiki.archlinux.org/index.php/Systemd-resolved) --set-domain=home.local -i vpn0 ... nastaveni domeny pomoci systemd-resolve  
systemd-resolve %%--%%status ... status  
systemd-resolve %%--%%set-dns=10.0.0.138 -i wlp2s0 ... nastaveni DNS  
/etc/systemd/network/soubor1

```
[Match]
Name=enp0s4

[Network]
DHCP=yes
DNS=192.168.1.1
```

sudo systemctl restart systemd-resolved ... restart demona  

#### Nastaveni sitoveho provozu

ifconfig -a ... ukaze vsechny sitove karty vcetne nastaveni adres  
ip a l ... ukaze vsechny sitove karty vcetne nastaveni adres  
ifconfig etho 192.168.1.1 netmask 255.255.255.0  
ifconfig 1 10.1.1.1 netmask 255.255.255.0  
ifconfig eth0 del 1.2.3.4/24  
ifconfig eth0 hw ether 00:11:22:33:44:55 ... nastavi MAC adresu sitove karty  
ethtool eth0 ... ukaze parametry sitovky  
mii-tool -v eth0 ... ukaze parametry sitove karty  
mii-tool -F 100baseTx-FD eth0 ... nastaveni full duplexu  
ethtool -s eth0 autoneg off duplex full ... nastaveni full duplexu  
ifdown eth0; ifup eth0 ... restart sitovky  
sysctl -a|grep eth0 ... nastaveni patametru jadra  
sysctl -p ... nacte nastaveni site z /etc/sysctl.conf  
route add default gw 1.2.3.4 ... prida do routovaci tabulky defaultni gw 1.2.3.4  
route add -net 192.168.37.0 netmask 255.255.255.0 gw 192.168.2.101  
route add 192.168.37.141 gw 192.168.2.101  
ip addr show ... ukaze nastaveni sitovych karet  
ip a l ... seznam sitovych karet a jejich nastaveni  
ip addr add 192.168.2.1/24 dev eth0 ... nastavi sitovou kartu  
ip addr add 192.168.3.1/24 brd + dev eth0 ... druha sitova adresa pro sitovku  
ip a del 192.168.3.1/24 dev eth0 ... Odebere sitovou adresu  
ip addr flush dev eth0 ... vynulavani nastaveni sitovky  
ip link set dev eth0 up ... aktivuje sitovou kartu - virtualne prispoji na sitove vrstve  
ip l set eth0 down ... deaktivuje sitovou kartu - virtualne odpoji na sitove vrstve  
ip neigh show ... ukaze sousedy (jako arp -a)  
ip route add  
ip route list (ip route show)  
ip r l (ip r s) ... seznam routovaci rabulky  
ip route add default via 192.168.0.254  
ip route add 129.39.133.132 255.255.255.255 via  62.187.136.32  
/sbin/ip route add 192.168.195.160/27 via 192.168.196.1 dev eth2  
ipcalc -p 192.168.195.160 255.255.255.224 Napise suffix  
ipcalc -h 10.240.8.4 ... napise sitove jmeno k adrese 10.240.8.4 (pouzito napr. /usr/sbin/dhclient-script)
vconfig ... nastavovani virtualnich sitovych karet z VIO serveru na P-Series  
modprobe 8021q ... povoleni VLANU  
setup ... RedHat, Fedora atd konfiguracni textovy agent  

### Bezdratova zarizeni

rfkill list all ... ukaze sitova zarizen a jejich stav - vypnuto/zapnuto  
### Bezdratova sit

aircrack BIT.ivs ... Vypocita WEP, nebo WPE klic ze stopy site v souboru BIT.ivs  
airodump-ng ... uklada pakety, ktere vycmucha bezdratova sitova karta ve vzduchu  
airodump-ng wlan0 -w BIT --channel 4 ... uklada pakety do souboru BIT  
aireplay-ng ... vysila pakety za ucelem ziskani stopy sitoveho provozu na mozne vypocitani klice  
iwconfig wlan0 up ... povoli wifi kartu  
iwconfig wlan0 mode managed key 11111111 ... Nastavi hodnotu 64-bit WEP klice a nastaveni karty jako klienta  
iwconfig wlan0 key 1111-1111-1111-1111 ... nastavi hodnotu 128-bit WEP klice  
iwconfig wlan0 essid "ESSID" ... povel k pripojeni k siti ESSID  
iwconfig wlan0 mode master ... Nastaveni karty jako access Pointu  
iwconfig wlan0 mode managed ... Nastaveni karty jako klienta  
iwconfig wlan0 rate 11M ... Nastavi rychlost karty  
iwconfig wlan0 channel 2  ... Nastavi kanal, na kterem bude pracovat  
iwconfig wlan0 freq 2.422G ... nastavi kmitocet - kazdemu kanalu odpovida frekvence  
iwconfig wlan0 commit ... u nekterych WiFi karet je treba timto prikazem odeslat nastaveni  
iwpriv ... nastaveni parametru Wifi karty, pokud to dovoluje  
iwlist ... listuje parametry Wifi karty, prohledava site okolo a ukazuje zarizeni pripojene k Wifi  
iwlist wlan0 scan ... vylistuje site v okoli  
iwlist wlan0 frequency ... vylistuje seznam frekvenci a kanalu, ktere karta podporuje  
iwspy wlan0 ... pokud to karta podporuje tak se timto ziskavaji statistiky s provozu WiFi site  
kismet ... detektor siti, cmuchac an detektor napadani v 802.11 bezdratovych sitich  

##### Wifi nastaveni pomoci prikazu

ifconfig wlan0  
iwlist wlan0 scan  
iwconfig wlan0 essid NETWORK_ID key WIRELESS_KEY  
dhclient wlan0  

##### Wifi [router](http://www.linuxreaders.com/2011/02/16/ubuntu-fedora-box-as-wifi-router/)

yum install [hostapd](http://wireless.kernel.org/en/users/Documentation/hostapd) -y  
vi /etc/hostapd/hostapd.conf:

```
# Customize these for your local configuration...
interface=wlan0
hw_mode=g
channel=6
ssid=LinuxReaders
 
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=3
wpa_passphrase=linuxreaderscom
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

chkconfig hostapd on
service hostapd restart
ifconfig wlan0 address 192.168.9.1 netmask 255.255.255.0
echo 1 > /proc/sys/net/ipv4/ip_forward
/sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

### Modem a GRPS/EDGE/4G pripojeni

pppd call XXX ... iniciuje spojeni s GRPS operatorem nastavenem v [/etc/ppp/peers/xxx](etc-ppp-peers-XXX)  
[/etc/chatscripts/xxx](etc-chatscripts-xxx) ... [AT prikazy](at.html) pro komunikaci s modemem, na ktery se odkazuje /etc/ppp/peers/xxx  
[/etc/ppp/chap-secrets](etc-ppp-chap-secrets) ... autentifikacni udaje pro pppd  
killall -HUP pppd ... ukonci spojeni s operatorem a ukonci pppd  

### DNS over TLS/HTTPS

[apt install stubby](https://www.linuxbabe.com/ubuntu/ubuntu-stubby-dns-over-tls) ... Stubby, sluzba pro prenos dns over tls, v novych verzich dns-over-https  
/etc/systemd/resolved.conf ... nativni cesta systemd-resolved na pouziti DNSSEC a DNS-over-TLS  
### Etherchannel = bonding

echo -e "alias bond0 bonding\n  
options bond0 mode=active-backup arp_interval=1000\n  
arp_ip_target=9.156.175.1,9.156.175.8 primary eth0 arp_validate_all" &gt;&gt; /etc/modprobe.conf  
cat /etc/sysconfig/network-scripts/ifcfg-bond0

```
device=bond0
BOOTPROTO=static
BROADCAST=9.33.5.255
IPADDR=9.33.5.3
NETMASK=255.255.255.0
NETWORK=9.33.5.0
ONBOOT=yes
GATEWAY=9.3.5.1
```

cat /etc/sysconfig/network-scripts/ifcfg-eth0

```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
MASTER=bond0
SLAVE=yes
USERCTL=no
```

stehne eth1  
cat /proc/net/bonding/bond0  

### Testovani provozu, prohlizeni site, ...

dig www.domena.cz ... provadi name resolving - preklady IP adres a jmen, dela dotazy na DNS server  
host www.domena.cz  
lsof -i ... ukaze otevrene porty  
lsof -i:8080 ... okaze, ktery proces uziva port 8080  
nepim .. (www.nongnu.org/nepim) test sitoveho provozu, stroj 1
nepim -c 192.168.1.1 -d -u .. stroj 2, (-u udp provoz)
netstat ... sitove informace a statistiky  
netstat -pant ... ukaze na kterem portu jedou jake sluzby  
netstat -tupnl ... otestuje, ktere porty jsou otevrene na tomto serveru  
netstat -i -e ... vypis IP adres vsech zarizeni  
netstat -p ... ukaze, ktere procesy pouzivaji sit  
`nmap' -p0-65535 a.b.com` ... Otestovani vzdalenych portu 0-65535 na server a.b.com, zda jsou otevrene  
`nmap -sP 192.168.0.*` ... prohleda zadane adresy, zkouma, ktere adresy jedou  
`nmap server.com` ... otestuje, ktere porty jsou otevrene  
nslookup www.domena.cz ... provede name resolving, ukazuje informace o dns atd., jako dig  
nslookup -debug www.domena.com ... detailni informace, vcetne TTL a master DNS (owner)  
nslookup -type=CNAME www.domena.com ... ukaze typ CNAME, alternativne A, TXT, SOA, MX, atd.  
ping  
rpcinfo -p localhost ... otevrene porty pres rpc  
ssldump -i any port 443 and host 9.220.24.160 ... ukaze SSL komunikaci (handshake atd)  
[strace](https://en.wikipedia.org/wiki/Strace) e trace=read,write -e read=29,30 -e write=29,30 -p 12343 ... smiruje cteni/zapis na socketu (pid 12343, socket 29,30)  
[tcpdump](../web/network_flow.htmp#tcpdump) ... cmuchac paketu  
[tcpdump](https://www.rationallyparanoid.com/articles/tcpdump.html) -n -i any src host 1.2.3.4 dst net 10.1.2.0/24 port 80 ... na vsech zarizenich (-i any) ukaz pakety (IP a port cislo: -n) z IP adresy 1.2.3.4 na sit 10.1.2.0/24. port 80  
tracepath ... ukaze cestu paketu jako traceroute  
traceroute  
tshark -ni eth0 -R "tcp.srcport eq 110 or tcp.dstport eq 110" ... (balicek wireshark) zobrazuje obsah paketu, ktere jdou na port, nebo z portu 110  

### IPv6

[IPv6](http://tldp.org/HOWTO/html_single/Linux+IPv6-HOWTO/)

host -t AAAA www.seznam.cz  
ifconfig eth0 inet6 add 2001:0db8:0:f101::1/64 ... prida IPv6 adresu sitove karte  
ifconfig eth0 inet6 del 2001:0db8:0:f101::1/64  
ip6tables ... (balicek iptables_ipv6)  
ip -6 addr show ... ukaze IPv6 adresu sitovych karet  
ip -6 addr add 2001:0db8:0:f101::1/64 dev eth0 ... konfigirece ip adresy  
ip -6 addr del 2001:0db8:0:f101::1/64 dev eth0
ip -6 tunnel show ... ukaze IPv6 tunely  
ip -6 route list  
ip -6 r add default dev eth0  
ip tunnel add sit1 mode sit ttl 10 remote 1.2.3.4 local 1.3.2.4 ... 4to4 tunel  
ip link set dev sit1 up ... 4to4 tunel  
ip -6 route add <prefixtoroute1> dev sit1 metric 1 ... 4to4 tunel  
ip tunnel add tun6to4 mode sit ttl 10 remote any local 1.2.3.4 ... 6to4 tunel  
ip link set dev tun6to4 up  ... 6to4 tunel  
ip -6 addr add <local6to4address>/16 dev tun6to4  ... 6to4 tunel  
ip -6 route add 2000::/3 via ::192.88.99.1 dev tun6to4 metric 1 ... 6to4 tunel  
ping6 -c1 ::1 -I lo  
ping6 -I eth0 fe80::8cda:24ff:fe62:786c ... ping6 musi vdy obsahovat zarizeni, ze ktereho pingame  
route -A inet6  
ssh -6 ::1%lo ... ssh pripojeni  
tcpdump -t -n -i eth0 -s 512 -vv ip6 or proto ipv6  
traceroute6  
tracepath6  

### NAT

[NAT](http://how-to.wikia.com/wiki/How_to_set_up_a_NAT_router_on_a_Linux-based_computer) routing

echo 1 /proc/sys/net/ipv4/ip_forward ... povoleni forwardovani sitoveho toku z jedne sitovky na druhou  
iptables -A FORWARD -i $EXTIF -o $INTIF -j ACCEPT ... forwardovani sitoveho toku z jedne sitovky na druhou  
iptables -A FORWARD -i $INTIF -o $EXTIF -j ACCEPT ... forwardovani sitoveho toku z jedne sitovky na druhou  
route add default gw 123.456.789.123 dev eth1  
route add -net 192.168.0.0/24 dev eth0  
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE  
iptables -t nat -D PREROUTING 3 ... smaze 3 postroutovaci pravidlo  

**1:1 NAT:**  
iptables -t nat -A PREROUTING -d 192.168.3.1 -j SNAT --to 172.16.1.131  
NAT 1:1 - forwardowani packetu:
iptables -t nat -A PREROUTING -i eth1 --source 9.158.168.221 -p tcp --dport 22 -j DNAT --to-destination 192.168.2.8:22 ... prichazejici pakety z IP presmeruj na 192.168.2.8, port 22  
iptables -t nat -A POSTROUTING -o eth1 --source 192.168.2.8 -j SNAT --to-source 9.158.168.221 ... vracejici se pakety z 192.168.2.8 posli zpet na ip 9.158.168.221  
1.--  
iptables -t nat -I POSTROUTING -s 192.168.56.102 -j SNAT --to-source 9.158.161.207  
iptables -t nat -I PREROUTING -d 9.158.161.207 -j DNAT --to 192.168.56.102  
iptables -vnL -t nat ... ukaze natovaci taboulku a statistiku paketu k jednotlivym pravidlum  

#### =Kernel a ovladace zarizeni pro sitove zarizeni

ethtool ... nastaveni sitove karty  
sysctl -a ... vypise parametry jadra sitoveho nastaveni  
sysctl ... meni a vypisuje sitove parametry jadra  
[brctl](http://www.linuxfoundation.org/collaborate/workgroups/networking/bridge) ... Virtualni switch v Linuxu. Konfigurace v jadru: networking - 802.1d Ethernet Bridging (balicek bridge-utils)  
[brctl](http://www.virtualize.cz/index.php?title=Linux_bridge&oldid=450) addbr AAA ... vytvori novy bridge AAA  
brctl delbr AAA ... smaze existujici bridge AAA  
brctl addif AAA eth0 ... prida sitovou kartu do bridge AAA  
brctl delif AAA eth0 ... odebere sitovou kartu eth0 z bridge AAA  
brctl show ... ukaze nastaveni bridgu  
brctl showmacs ... ukaze MAC adresy  
ip l s AAA up ... aktivuje bridge AAA  
dhclient AAA ... ziska IP z DHCP serveru  
ip addr add 10.1.1.18/16 brd + dev br0 ... manualni nastaveni IP  
tunctl -t tap0 -u user ... vytvori virtualni sitovou kartu  
ip l s tap0 up ... aktivuje sitovou kartu  
brctl addif br0 tap0 ... prida tap0 do bridge br0  

### Bezpecnost - Firewall

.rhosts  
#### povoleni/zakaz pristupu tcp_wrappers

/etc/hosts.allow  
/etc/hosts.deny  
ldd /usr/sbin/sshd | grep libwrap ... zjisti, zda sluzba lze blokovat pres hosts.deny/allow  
##### Firewall filtry - iptables

iptables --list ... ukaze filtry  
iptables -L INPUT ... ukaze filtry pro prichozi pakety  
iptables -nvL --line-numbers ... ukaze vsechny zaznamy v tabulce s cisly pravidel a pocty paketu  
iptables -A INPUT -j LOG ... zapne logovani paketu do /var/log/messages  
iptables -A INPUT -j REJECT ... odmitne vsechny ostatni packety  
iptables -t filter -A INPUT -p tcp -s 192.168.0.1 -o eth0 -j DROP ... prida na konec pravidlo: zahodit tcp pakety ktere prichazi kartou eth0 z IP adresy 192.168.0.1  
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT ... prijme vsechny pakety se stavem ESTABLISHED a RELATED  
iptables -I INPUT 3 -s 127.0.0.1 -sport 23: -i lo -j ACCEPT ... Vlozi na 3. pozici pravidlo: prijmout packety z IP adresy 127.0.0.1 z loopback a jdouci z portu 23 a vice  
iptables -I INPUT -d '!' 127.0.0.2 -j ACCEPT ... Vlozi na jako prvni pravidlo: prijmout packety krome na IP adresu 127.0.0.2  
iptables -D INPUT 1 ... smaze prvni pravidlo z prichozich filtru  
iptables -Z INPUT ... vynuluje pocitadla paketu  
iptables -N MOJE ... vytvori novy seznam providel s nazvem MOJE  
iptables -X MOJE ... smaze seznam pravidel s nazvem MOJE  
iptables -A INPUT-j MOJE ... na konec pravidel INPUT prida pravidla MOJE  
ipravles -t net -F POSTROUTING ... zmaze vsechny pravidla z NATovaci tabulky POSTROUTING  
iptables -L -t nat ... ukaze natovaci tabulku  
iptables --list PREROUTING -t nat ... ukaze nat tabulku  
iptables -L -t mangle ... ukaze mangle tabulku  
/sbin/iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o 4.3.2.1 -j MASQUERADE ... vse, co prijde ze site 192.168.1.0/24 zmeni source adresu na 4.3.2.1  
iptables-save >> iptables.cfg ... ulozi nastaveni do souboru  
iptables-restore &lt; iptables.cfg ... nacte nastaveni ze souboru  
[firewall-cmd](https://www.certdepot.net/rhel7-get-started-firewalld/) --state ... status firewallu v novem RH/F  
firewall-cmd --get-active-zones  
firewall-cmd --zone=dmz --add-port=2888/tcp --permanent  
firewall-cmd --reload  
ufw allow 22 ... povoli port ssh v UFW  
systemctl stop ufw.service ... vypne Ubuntu Firewall  

### Programy a nastroje pro komunikaci:

##### telnet

curl telnet://1.2.3.4:port ... telnet spojeni  
telnet 1.2.3.4:80  
nc 1.2.3.4 80  
cat < /dev/tcp/127.0.0.1/22 ... otevření spojení bez síťových nástrojů  
(echo > /dev/tcp/skinner/22) >/dev/null 2>&1 && echo "It's up" || echo "It's down" ... zjištění, zda je port otevžený  

##### http/https

wget ... stahovani www a ftp do souboru\  
curl ... vymakanejsi stahovani www a ftp do souboru  
lynx, links, w3m ... textovi w3 klienti  

##### ssh

ssh ... pripojeni ke vzdalenemu pocitaci pomoci Secure Shell na port 22  
[~/.ssh/config](config.txt)\\ ... uzivatelnske nastaveni ssh  

##### ssl

Ochrana proti "man in middle" utokum - kryptovani dat

`openssl` ... [Vice na Linux - sluzby - apache2](http://tomas.lipensky.cz/linux/services.html#httpd)  
openssl s_client -connect bart.math.muni.cz:21 ... otestuje, zda bezi openssl na danem portu  

##### Posta POP3,IMAP

mutt, pine ... textovi smtp/pop3 klienti  
fetchmail -u <username> -a -p POP3 --bsmtp temp.txt <server>.com ... stahne maily z smtp serveru do souboru  

##### [socks](http://en.wikipedia.org/wiki/SOCKS)

[transocks](http://transocks.sourceforge.net/) ... forwardovani casti sitoveho provozu pres socks  
[transocks_ev](http://oss.tiggerswelt.net/transocks_ev/) ... forwardowani casti sitoveho provozu pres socks(+ [instalace](http://board.raidrush.ws/showthread.php?t=637066))  
tsocks = toxsocks ... forwardovani casti provozu pres socks  
connect-proxy ... otevre spojeni pres socks server  
proxychains telnet server.com ... otevre spojeni pres libovolny pocet proxy serveru nastavenych v /etc/proxychains.conf. Priklady [Volne dostupnych proxy serveru](http://aliveproxy.com/proxy-list-port-8080/)  

##### COM, LPT komunikace

rx ... prijima soubory pod protokolem x(z,y)modem
minicom ... ovladani a komunikace pres porty

##### Wifi

[WICD](http://wicd.sourceforge.net/) - Manazer WIFI pripojeni  

##### Ostatní síťové nástroje

`rsync` ... prenos velikych objemu dat  
`rdist` ... synchronizace souboru na ruznych serverech  
`telnet` ... tcp pripojeni na telnet server nebo na jakykoli port  
`nc` ... netcat vytvareni tcp/udp spojeni na porty, cteni, zapis - viz [UNIX-Prikazy](http://tomas.lipensky.cz/unix/commands.html)  
`whois seznam.cz` ... informace o domene z whois serveru  

#### Network manager

/etc/NetworkManager/dispatcher.d ... konfigurace akci network managera  
[nmcli](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec-Using_the_NetworkManager_Command_Line_Tool_nmcli.html) nm wifi on ... zapne Wifi v Network manageru  
nmcli dev wifi list ... seznam wifi siti  
nmcli c show ... seznam sitovych karet, i virtualnich  
nmcli c modify "Wired connection 1" ipv4.dns-search "example.com, priklad.cz", nastavi DNS  
nmcli c modify "vpn1" ipv4.dns 10.20.30.40 ... nastavi DNS  
nmcli c down "Wired connection 1" && nmcli c up "Wired connection 1", restartuje kartu  
nm-applet --sm-disable ... spusti network manager applet  

### Windows remoting

remmina ... pripojeni ke vzdalene plose  
rdesktop ... pripojeni ke vzdalene plose  
dir \\tsclient\Downloads ... pristup ke sdilenemu adresari (tsclient = Terminal Server client)
