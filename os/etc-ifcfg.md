/etc/sysconfig/network-scripts/ifcfg-eth0:
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.1.255
HWADDR=
IPADDR=192.168.1.111
NETMASK=255.255.255.0
NETWORK=192.168.1.0
ONBOOT=yes
TYPE=Ethernet

/etc/sysconfig/network-scripts/ifcfg-eth0:1
DEVICE=eth0:0
BOOTPROTO=none
ONPARENT=yes
IPADDR=XXX.XXX.XXX.XXX
NETMASK=255.255.255.0
BROADCAST=XXX.XXX.XXX.255

/etc/sysconfig/network-scripts/ifcfg-eth1:
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes

/etc/sysconfig/network-scripts/ifcfg-eth0-range0:
IPADDR_START=192.167.1.5
IPADDR_END=192.167.1.100
CLONENUM_START=0
NETMASK=255.255.255.0

/etc/sysconfig/network-scripts/ifcfg-br0:
DEVICE=br0
TYPE=Bridge
BOOTPROTO=dhcp
ONBOOT=yes
DELAY=0
STP=off

/etc/sysconfig/network-scripts/ifcfg-eth2:
TYPE=Bridge
IP=xxx.xxx.xxx.xxx
BOOTPROTO=static
ONBOOT=yes
