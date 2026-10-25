# AIX - HACMP - High Availability Cluster Multi-Processing

### start/stop

smitty clstart ... 
(/usr/es/sbin/cluster/utilities/clstart)  
smitty clstop ... 
(/usr/es/sbin/cluster/utilities/clstop)  

### info

lssrc g cluster
lssrc -a | grep cluster
ps ax | grep cluster
/usr/sbin/cluster/clstat

lssrc -ls clstrmgrES ... Cluster Information Services - info o jedoucim clusteru\\  
lssrc -ls grpsvcs ... detailni informace o Group Services - demon, co kontroluje Volume Groupy v clusteru
lssrc -ls gsclvmd ... Concurrent Logical Volume Manager - VGID atd
/usr/es/sbin/cluster/utilities/cltopinfo ... info o nadefinovanem clusteru  
/usr/es/sbin/cluster/utilities/clRGinfo ... ktere Resources Group jsou kde online  
/usr/es/sbin/cluster/utilities/clshowsrv -v ... ukaze bezici sluzby pro Cluster  
/usr/es/sbin/cluster/clinfo
/usr/es/sbin/cluster/clstat
/usr/es/sbin/cluster/utilities/cldisp ... ukaze Resources a ktere skripty je spousti  
/usr/es/sbin/cluster/samples/clverify
/usr/es/sbin/cluster/diag/clver -c -V normal -t -r -V normal
cat /var/hacmp/clverify/clverify.log
/usr/es/sbin/cluster/utilities/get_local_nodename ... jmeno node 
ps -ef | grep $(lsvg dataVG | grep IDETNTIFIER | cut -d":" -f3) ... informace o tom, zda dataVG je v clusteru
netmon.cf ... monitoruje sitove spojeni s ostatnimi clustery

### kontrola, verifikace

smitty clverify
/usr/sbin/cluster/diag/clverify cluster topology check
/usr/sbin/cluster/diag/clverify cluster config networks
/usr/sbin/cluster/diag/clverify cluster config resources

### logy

Problem Determination Tools - HACMP Log Viewing and Management - Change/Show a Cluster Log Directory  
odmget -q HACMPlogs  
tail /var/hacmp/adm/cluster.log  
tail /tmp/hacmp.out  
ls -lt /var/hacmp/log/ | head  
tail f50 /tmp/hacmp.out
/usr/sbin/cluster/history/cluster.mmddyyyy  ... if crasshed

### operace

smitty cm_hacmp_resource_group_and_application_management_menu ... prenaseni sluzeb  
smitty cm_change_a_resource_group_select ... hacmp failover policy setting  
smitty cm_change_show_resource_distribution_preferen ... adjust rules how service IP should behave at network cards during failovers  
smitty cm_change_resources_for_a_rg_select ... do mutual cross nfs mounts  
smitty cm_cfg_snap_menu ... delani snapu  
smitty cm_config_hacmp_communication_interfaces_devices_menu_dmn ... setup heartbeat over disk  
/usr/es/sbin/cluster/utilities/clRGmove -s 'false'  -u -i -g 'DB_DEV_R -G' -n 'odadev2006' ... nastartuje resource DB_DEV_R na node odadev2006  
/exploit/HACMP/scripts/HA_environment

### demoni

clstrmgr
grpsvcs
snmpd

### nastaveni

##### disky

/etc/cluster/disktype.lst ... ['lsdev -Cc disk -l hdisk9 -F PdDvLn' SCSIDISK|SSA|FCPARRAY|ARRAY|FCSCSI]
/etc/cluster/lunreset.lst ... [
/etc/cluster/conraid.dat ... pro concurent mode ve starem HACMP

v /etc/enviroment:
MISSINGPV_VARYON=TRUE ... Force varyon
HACMP_MIRROR_VARYON=TRUE ... HACMP force varyon
/usr/sbin/cluster/sbin/cl_updatevg ... update clusteru?

##### klienti

/usr/es/sbin/cluster/etc/clinfo.rc

##### [RSCT RM](http://post.doit.wisc.edu/library/aix51/nav/Books/nav_8.htm) - resource monitoring

/var/ct/IW/log/mc ... log soubory
/usr/sbin/rsct/cfg ... konfiguracni soubory
/usr/sbin/rsct/bin ... binarni soubory
IBM.AuditRM ... (Audit Log resource manager)
IBM.ERRM ... (Event Response resource manager)
IBM.FSRM ... (File System resource manager)
IBM.HostRM ... (Host resource manager)
ctrmc ... (Resource Monitoring and Control subsystem) 

### [Balicky - announcement letter](http://www-03.ibm.com/systems/p/advantages/ha/)

lslpp -L cluster.*  
Prerekvizity:
bos.adt.libm
bos.adt.syscalls
dos.data
Tivoli
Netview
RSCT
<b>Min. klient</b>
cluster.adt.es
cluster.doc.en_US.es
cluster.es
cluster.es.cspoc
cluster.license
cluster.man.en_US.es
cluster.man.en_US.cspoc
cluster.msg.en_US.es
<b>Dalsi</b>
cluster.doc.en_US.es
cluster.es.cfs
cluster.es.nfs
cluster.es.plugins
cluster.es.worksheets
cluster.hativoli
cluster.haview
cluster.mn.en_US.es.dara
cluster.msg.[lang].[hativoli|haview]

rsct.basic.[hacmp|rte]
rsct.pt.storagerm
rsc.core.[errm|hui|hostrm|rmc|sec|utils]

Snapshot:
smitty cm_cfg_snap_menu  
/usr/es/sbin/cluster/snapshots/*.odm  
/usr/es/sbin/cluster/snapshots/*.info  
tail -f /var/hacmp/adm/cluster.log  

### problemy

Resource ve stavu RELEASING ... Zkontrolovat hacmp.out, zjistit, zda skript na stop uz skoncil, najit proces /bin/ksh /usr/es/sbin/cluster/events/config_too_long 360 TE_FAIL_NODE a zabit, reboot serveru  

##### odkazy

http://www.emc.com/interoperability/matrices/EMCSupportMatrix.pdf
http://www.storage.ibm.com
http://www-03.ibm.com/systems/storage/
[http://www-03.ibm.com/systems/systems/p/library/hacmp_docs.html](http://publib.boulder.ibm.com/infocenter/clresctr/vxrx/index.jsp?topic=/com.ibm.cluster.hacmp.doc/hacmpbooks.html)
http://www-03.ibm.com/support/techdocs/atsmastr.nsf/Web/Flashes
http://www-03.ibm.com/support/techdocs/atsmastr.nsf/Web/Technotes
http://www-03.ibm.com/support/techdocs/atsmastr.nsf/WebIndex/FLASH10390
http://www-1.ibm.com/servers/storage/support/software/sdd.html
http://www-1.ibm.com/support/docview.wssrs=540&context=ST52G7&uid=ssg1S4000065&loc=en_US&cs=utf-8&lang=en
[Implementing HACMP Cookbook](http://publib-b.boulder.ibm.com/abstracs/sg246769.html?open)
http://www.redbooks.ibm.com/
[Advanced POWER Virtualization on IBM Systems p5: Introductio and Configuration](http://www.redbooks.ibm.com/abstracts/sg247940.html?Open)
ftp://ftp.software.ibm.com/storage/fastt/fastt500/HACMP_config_info.pdf
