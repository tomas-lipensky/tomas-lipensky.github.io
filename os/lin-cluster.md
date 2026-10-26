---
title: LINUX - Cluster
---

## Externi odkazy

[xCAT](http://www.alphaworks.ibm.com/tech/xCAT) - Extreme Cluster Administration Toolkit - kolekce Perk a ksh skriptu atd. k ovladani clusteru  
[CSM](http://www-1.ibm.com/servers/eserver/clusters/software/) Cluster System Management - zpusob na centralni zpravovani clusteru  
[ECT](http://www.alphaworks.ibm.com/tech/ect4linux) Enhanced Cluster Tools . extra funkce pro CSM  
[OSCAR](http://oscal.openclustergroup.org) - kolekce opensource nastroju pro clustering  
[LVS](http://www.linuxvirtualserver.org/)Linux Virtual Server Project - poskytuje Loadbalancing  
[[http://www-306.ibm.com/software/tivoli/products/sys-auto-linux|Tivoli System Automation for Linux  
[Lunux-HA](http://www.linux-ha.org) projekt - poskytuje Heartbeat a [fake](http://www.vergenet.net/linux/fake/) - IP takeover  
[Monit](http://www.tildeslash.com/monit/) - umoznuje spravovat, monitorovat a provadet akce  
[DRBD](http://www.drbd.org) - sitovy mirroring disku  
Filesystemy pro Cluster: [http://opengfs.sourceforge.net](http://opengfs.sourceforge.net)Open Global File System]], [General Parallel File System for Linux](http://www-1.ibm.com/servers/eseerver/clusters/software/gpfs.html),
[Journaled File system](http://www-124.ibm.com/developerworks/opensource/jfs/), [ext3](http://olstrans.sourceforge.net/release/OLS2000-ext3/)  

## RedHat clustering

system-config-cluster  
cluquorumd ... Quorum daemon  
clusvcmgrd ... Service manager daemon  
clurmtabd ... Synchronizes NFS mount entries in /var/lib/nfs/rmtab with a private copy on a service's mount point  
clulockd ... Global lock manager (the only client of this daemon is clusvcmgrd)  
clumembd ... Membership daemon  
/etc/cluster.xml  
clustat ... Cluser Status  
clufence ... Cluster fence  
/sbin/service clumanager start/stop  
/sbin/service cluster start/stop
