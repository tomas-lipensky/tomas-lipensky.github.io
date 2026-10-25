# OpenStack

## Odkazy

[Popis YAMLu](http://docs.ansible.com/ansible/YAMLSyntax.html) - YAML Ain't Markup Language - na Ansible strankach  
[Heat Orchestration Template](http://docs.ansible.com/ansible/YAMLSyntax.html) - [YAML](http://yaml.org/) soubor na popsani Heat obrazu  
[Uvod do tvoreni Heat obrazu](https://support.rackspace.com/how-to/building-cloud-orchestration-templates/), [Heat obrazy1](https://developer.rackspace.com/blog/openstack-orchestration-in-depth-part-1-introduction-to-heat/) a [Heat obrazy 2](https://developer.rackspace.com/blog/openstack-orchestration-in-depth-part-2-single-instance-deployments/) na popsane naRackspace  
[OpenStack Orchestration In Depth, Part I: Introduction to Heat](https://developer.rackspace.com/blog/openstack-orchestration-in-depth-part-1-introduction-to-heat/)  
[OpenStack Orchestration In Depth, Part II: Single Instance Deployments](https://developer.rackspace.com/blog/openstack-orchestration-in-depth-part-2-single-instance-deployments/)  
Sebastien Han's blogs: [Delete VM in error state](https://www.sebastien-han.fr/blog/2012/07/10/delete-a-vm-in-an-error-state/), [where does my instance run](https://www.sebastien-han.fr/blog/2012/12/20/where-does-my-instance-run/), [rsyslog](https://www.sebastien-han.fr/blog/2012/12/05/openstack-and-rsyslog/)  

## Start/Stop/Status

[Managing IBM Cloud Orchestrator services manually](https://www.ibm.com/support/knowledgecenter/SS4KMC_2.4.0/com.ibm.sco.doc_2.4/c_managing_ico_services_manually.html)  
/opt/ibm/ccs/scui/scoStart.sh ... spusti elf-service user interface  
ps -ef | grep scui ... ukaze bezici procesy Self-service user interface  
/opt/ibm/pcg/startServer.sh ... spusti Public Cloud Gateway  
ps -ef | grep pcg ... ukaze bezici procesy Public Cloud Gateway  
nova-manage --version ... verze OpenStacku  

## OpenStak komponenty

Nova ... sprava virtualnich masin  
Cider ... blokova zarizeni - disky  
Swift ... (sklad objektu) sbira a uchovava nestrukturovana data pomoci http  
Neutron ... sitova komponenta  
Keystone ... Sluzba identit uzivatelu OpenStacku  
Glance .. Spravce diskovych obrazu  
Ceilometer ... monitoruje a uctuje za sluzby  
Horizon ... webovy portal na praci s OpenStack sluzbama  
Heat ... API na managovani sluzeb  
Trove ... poskytovani databazi  

## Sluzby

cinder service-list ... sezanm Cinder sluzeb  
nova-manage service list ... seznam Nova sluzeb  

## OpenStack logy

/var/log/nova/scheduler.log  
/var/log/powervc/nova-powervc.log  

## OpenStack prikazy

source /root/openrc  
nova list ... sezanm serveru a jejich status  
nova show IP ... informace o serveru  
nova service-list  
service openstack-nova-compute restart  
nova-manage service list ... seznam sluzeb a jejich status, vcetne availability zon  
nova-manage host list ... seznam Hostovacich sluzeb (ESX serveru)  
nova --os-region-name REGION availability-zone-list ... vylistovani availability-zon v jinem regionu  
openstack extension list -c Alias -c Name --network ... seznam rozsireni  

## Openstack HA

nova host-update compute-01 --maintenance enable ... prepne jeden node HA OpenStacku do maintenance modu  
nova-manage service disable --host=NODE1 --service=SERVICE1 ... vypne sluzbu SERVICE1 na damen node NODE1 opestacku  

## Availability zone. agregace, hostovaci masiny

**Agregace (host agregate)** - je skupinovani hostu s asociovanymi metadaty. Host muze byt prirazen do vice agregaci. Agregace muze tvorit availability zonu.
[Pekny clanek na RedHat dokumentaci](https://access.redhat.com/documentation/en-us/red_hat_openstack_platform/8/html-single/architecture_guide/)  

nova aggregate-list ... seznam agregaci a availability zon  
nova aggregate-create test-aggregate blabla ... vytvori agregaci test-aggregate v availability zone blabla  
nova aggregate-set-metadata 1 coolhardware=true ... prida metadata do agregace  
nova host-list ... seznam hostu a availability zon  
nova aggregate-add-host 3 openstack ... propoji agregaci s hostem  
nova aggregate-details test-aggregate ... informace o agregaci  
openstack availability zone list ... seznam availability zon  
nova availability-zone-list ... seznam sluzeb a jejich status, vcetne availability zon  
nova host-describe CLUSTER1 ... popise host CLUSTER1  
nova hypervisor-servers CLUSTER1 ... seznam instanci ktere jedou na hostu (a asouciovanem hypervizoru)  

### Virtualni stroje - Stacks (Nova)

heat stack-list  
heat stack-show STACKNAME  
heat resource-list STACKNAME - ukaze nova instacni a ostatni zdroje pouzite pri sestavovani Stacku  
openstack stack create --template server_console.yaml --parameter "image=cirros" MYSTACK ... vytvori stack z Yaml souboru  
nova service-list  
nova list ... seznam virtyalnich stroju  
openstack server list = nova list  
nova-manage vm list ... seznam VM
nova show ee602ea2-59de-4c57-a242-db86e345a78f | grep tenant_id | awk '{ print $4 }' ... ukaze id PROJEKTu, kde se nachazi VM  
db2 connect to NOVA; db2 -x "select HOST from NOVA.INSTANCES where UUID = '503d0a17-7e54-704e-8e5e-8e68d596a8aa' "|sed -e 's/  *$//g' ... napise k instance UUID host na vCentru  

### Hypervizory - Clustery ESX hostovacich masin

nova hypervisor-list ... seznam clusteru ESX hostovacich masin  
nova hypervisor-show 1 ... ukaze hypervizor  
nova hypervisor-servers CLUSTER2 ... seznam hostovanych serveru na hypervizoru CLUSTER2  
sudo nova-manage vm list | column -t ... seznam vsech VM a hypervizoru (i smazanych, co byly a jsou hostovany)  
cat /var/lib/nova/instances/compute_nodes ... seznam hypervizoru - compute nodu  

### Obrazy - images

[openstack image](http://docs.openstack.org/user-guide/common/cli-manage-images.html) list  
openstack image show RHEL6.6-ICO2.5  
/etc/glance/glance-api.conf ... konfiguracni soubor  
openstack image set --property short-id=fedora23 name-of-my-fedora-image ... nastavi kratky nazev pro dlouhy nazev  
/var/log/nova/discovery.log ... objeveni novych zmen v obrazeh  
glance image-list ... seznam obrazu  
glance image-delete 91c7a986-002f-46d2-bc20-99a2c7ef2e2 ... smaze obraz v ICO  
service nova-discovery restart ... restartuje sluzbu nova-discovery  

### Volumes - disky

/etc/cinder/[cinder.conf](https://docs.openstack.org/kilo/config-reference/content/section_volume-misc.html) ... konfiguracni soubor  
openstack volume create --image 8bf4dc2a-bf78-4dd1-aefa-f3347cf638c8 --size 8 --availability-zone nova my-new-volume  
cinder create --availability-zone nova --storage-type GOLD --display-name TL-disk1 10 ... vytvori 10GB disk TL-disk1 f availability zone (jina, nez v Nove, [definuje se v cinder.conf](https://ask.openstack.org/en/question/28019/how-to-create-new-availability-zone-in-cinder-there-is-no-info-in-mans/)) a storage type GOLD  
openstack volume list  
openstack volume create --image 376bd633-c9c9-4c5d-a588-342f4f66d086 --size 1 --availability-zone nova test ... vytvori disk z obrazu  
openstack server add volume 84c6e57d-a6b1-44b6-81eb-fcb36afd31b5 573e024d-5235-49ce-8332-be1576d323f8 --device /dev/vdb ... pripoji disk k instanci  
openstack volume show 573e024d-5235-49ce-8332-be1576d323f8 ... ukaze info o disku  
openstack server remove volume 84c6e57d-a6b1-44b6-81eb-fcb36afd31b5 573e024d-5235-49ce-8332-be1576d323f8 ... odebere disk z instance (VM)  
openstack volume set 573e024d-5235-49ce-8332-be1576d323f8 --size 10 ... zmeni velikost disku  
openstack volume delete my-new-volume ... smaze disk (pokud nelze, musi se aplikovat [toto](https://ask.openstack.org/en/question/66918/how-to-delete-volume-with-available-status-and-attached-to/))  

### Site

openstack network list ... seznam siti  
openstack network show VL123 ... popis site  
neutron router-list  
neutron subnet-list  
neutron port-list  
neutron agent-list  
neutron port-list ... seznam obsazenych portu (IP adres)  
neturon port-show portID ... informace o obsazenem portu  
neturon port-delete portID ... smazani obsazeneho portu (napriklad pokud masina byla smazana mimo OpenStack)  

### flavors

[openstack flavor](http://docs.openstack.org/admin-guide/cli-manage-flavors.html) list ... seznam moznych velikosti kontejneru  
openstack flavor create FLAVOR_NAME --id FLAVOR_ID --ram RAM_IN_MB --disk ROOT_DISK_IN_GB --vcpus NUMBER_OF_VCPUS ... vytvori novy kontejner  
openstack help flavor create ... napoveda  
openstack flavor delete FLAVOR_I ... smazani kontejneru  

## Uzivatele, projekty, role

openstack project list ... seznam projektu  
openstack project show admin ... informace o projektu admin  
openstack user list  
openstack role list  
openstack role assignment list --user USER_NAME --project PROJECT_ID --names  
openstack role add --user demo --project test-project new-role  
openstack role create new-role  
openstack user delete USER_NAME  
openstack user set USER_NAME --enable  
openstack user set USER_NAME --name user-new --email new-user@example.com  
openstack user create --project new-project --password PASSWORD new-user  
openstack project delete PROJECT_ID  
openstack project set PROJECT_ID --disable  
openstack project set PROJECT_ID --name project-new  
openstack project create --description 'my new project' new-project --domain default  
openstack security group list  
openstack security group rule list default  
openstack security group show default  

## Drivery

[VMware driver and OpenStack Kilo (version)](https://docs.openstack.org/kilo/config-reference/content/vmware.html)  
[VMware and VMDK support](https://docs.openstack.org/kilo/config-reference/content/vmware-vmdk-driver.html)  
[VMware - Storage Policy Based Management (SPBM) - Storage profily pro VM](https://specs.openstack.org/openstack/nova-specs/specs/kilo/implemented/vmware-spbm-support.html)  
[VMware - Cinder storage profile support](https://wiki.openstack.org/wiki/Cinder/VMwareVmdkDriver/vmdk-storage-policy-volume-type)  

## Podpurne nastroje

[Cloudbase-init](http://wiki.cloudbase.it/cloudbaseinit-doc) ... bootstrap Windows  
[Cloud-init](https://raymii.org/s/tutorials/Automating_Openstack_with_Cloud_init_run_a_script_on_VMs_first_boot.html) ... bootstrap Linuxu a AIXu  
[Popis fazi bootstrapu cloud-initu](http://cloudinit.readthedocs.io/en/latest/topics/boot.html) nebo to same na [Archlinux wiki](https://wiki.archlinux.org/index.php/Cloud-init)  
[Userdata pro cloud-init](http://cloudinit.readthedocs.io/en/latest/topics/examples.html) nebo [DigitalOcean]() nebo [na gitlabu](https://gist.github.com/arnaudmorinol/4d2c9ab52a97afd31f5b)  

## Databaze objektu

db2 connect to NOVA  
db2 "select HOST from NOVA.INSTANCES where UUID = '$i' "  

db2 connect to cinder  
db2 'select * from CINDER."volumes" FETCH FIRST 2 ROWS ONLY'
