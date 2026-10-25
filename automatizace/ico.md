# ICO a SCO

Ibm Cloud Orchestrator a SmarCloud Orchestrator

## Interni odkazy

[OpenStack](openstack.html)  

## Externi odkazy

[KC: ICO 2.5 - Managing virtual images](http://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/pc/pct_manage_cat_vi.html)  
[Knowledge Center - ICO 2.4](http://www.ibm.com/support/knowledgecenter/SS4KMC_2.4.0.2/com.ibm.sco.doc_2.4/kc_welcome-ico.html)  
[Support portal - ICO](https://www-947.ibm.com/support/entry/myportal/product/tivoli/ibm_cloud_orchestrator?productContext=-1579644971)  

[DW wiki o SCO a ICO](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/IBM%20SmartCloud%20Orchestrator/page/Welcome)  
[Infocenter o SCO](http://pic.dhe.ibm.com/infocenter/tivihelp/v48r1/index.jsp?topic=%2Fcom.ibm.sco.doc_2.2%2Fwelcome.html)  
[deployment automation](https://www.ibm.com/marketplace/cloud/deployment-automation/us/en-us)  
[ICO 2.5 Content Development Guide](https://www.ibm.com/support/knowledgecenter/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/ICOv25_Content_Development_Guide.pdf)  

## URL

IP:PORT/ProcessCenter/login.jsp  

## Start/Stop/Status

[[https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/t_start_stop_sco.html|
/opt/ibm/ico/orchestrator/scorchestrator/SCOrchestrator.py --start ... Start ICO]]  
[[https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/t_start_stop_sco.html|
/opt/ibm/ico/orchestrator/scorchestrator/SCOrchestrator.py --stop ... Stop ICO]]
[[https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/t_start_stop_sco.html|
/opt/ibm/ico/orchestrator/scorchestrator/SCOrchestrator.py --status ... Status ICO sluzeb]]
[Managing IBM Cloud Orchestrator services manually](https://www.ibm.com/support/knowledgecenter/SS4KMC_2.4.0/com.ibm.sco.doc_2.4/c_managing_ico_services_manually.html)  

/opt/ibm/ccs/scui/scoStart.sh ... spusti elf-service user interface  
ps -ef | grep scui ... ukaze bezici procesy Self-service user interface  
/opt/ibm/pcg/startServer.sh ... spusti Public Cloud Gateway  
ps -ef | grep pcg ... ukaze bezici procesy Public Cloud Gateway  

## Komponenty

Workload Deployer (konfigurace v /opt/ibm/rainmaker/purescale.app/private/expanded/ibm/rainmaker.cloud-4.0.0.1/config/zero.config)  
Storehouse ... The Storehouse je repozitar obsahujii system artifakty, virtual application pattern workload artifakty ,virtual application pattern deployment runtime artifakty a virtual application pattern troubleshooting artifakty  
kernelservices  
scui - Web gui  
zso - workload manager  

## Logy

BPM: /opt/ibm/ico/BPM/v8.5/profiles/Node1Profile/logs/SingleClusterMember1/SystemOut.log  
/opt/ibm/ico/scui/logs/scoui.log ... logy grafickeho interfacu (SCO UI)  
OpenStack: /var/log/heat  
/var/log/ico_install .. instalacni a import/export logy  
/var/log/cloud-deployer ... logy na DB2 serveru - cloud deployeru  
/opt/ibm/ico/HTTPServer/logs ... http logy  
/opt/ibm/ico/WebSphere/Plugins/logs ... plugin logy  
/var/ibm/InstallationManager/logs ... instalacni logy  

## Udrzba

rm /opt/ibm/ico/scui/core.* ... mazani core dumpu  
/opt/ibm/cloud-deployer/ico.version ... verze ICO  
/opt/ibm/ico/orchestrator/pdcollect/pdcollect.py ... kolekce logu pro PMR  
/opt/ibm/ico/pcg/encryptPassword.sh ... enkypce hesla na pouziti pro /opt/ibm/ico/pcg/etc/admin.json a /opt/ibm/ico/pcg/etc/credentials.json  
/opt/ibm/ico/pcg/refreshEndpoint.sh ... refreshne informace o ICO enpointu (po zmene config.json souboru)  
[Zmena hesel](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/r_how_to_change_the_various_passwords.html)  
Po pridani dalsiho region serveru nebo update CMwO se musi spustit konfiguracni skripty ICO  

## BPM udrzba

/opt/ibm/ico/BPM/v8.5/bin/wsadmin.sh
AdminTask.setTraceSpecification(’[-persist true -traceSpecification *=info:WLE.wle_javascript=audit ]’); AdminConfig.save(); ... vyplne logovani v wsadminovi  
AdminTask.setTraceSpecification(’[-persist true -traceSpecification *=info ]’); AdminConfig.save(); ... znovu zapne logovani  
/opt/ibm/ico/BPM/v8.5/bin/PropFilePasswordEncoder.sh  ... zakoduje heslo pro pouziti v /opt/ibm/ico/BPM/v8.5/profiles/DmgrProfile/properties/soap.client.props  a /opt/ibm/ico/BPM/v8.5/profiles/Node1Profile/properties/soap.client.props  

## Konfigurace

/opt/ibm/ico/pcg/etc/config.json  
/opt/ibm/ico/pcg/etc/admin.json  
/opt/ibm/ico/pcg/etc/credentials.json  
/opt/ibm/ico/pcg/etc/log4j.properties  
/opt/ibm/ico/scui/etc/config.json  

## Management z Deployment serveru

[CMwO](icm.html) prikazy, CMwO v adresari /opt/ibm/cmwo  

## Obrazy

**ICO 2.4**  
[Procedura na vytvoreni image template na ICO 2.4](http://www.ibm.com/support/knowledgecenter/SS4KMC_2.4.0/com.ibm.sco.doc_2.4/t_creating_smartcloud_orchestrat.html)  
[http://www.redbooks.ibm.com/abstracts/sg248042b](http://www.redbooks.ibm.com/abstracts/sg248042b).html?Open|Creating Smart Virtual Appliances with IBM Image Construction and Composition Tool]] ... nastroj na customizaci obrazu po deployi  
virtual solutions activation engine ... Cast IBM Image Construction and Composition Tool ktera po prvnim spusteni virtualni masiny nastavi obraz na pozadovane vlastnosti  
[DW: Virtual appliances and the Open Virtualization Format](http://www.ibm.com/developerworks/library/l-open-virtualization-format-toolkit/) - [OVF](https://www.ibm.com/support/knowledgecenter/SSSHEC_7.6.0/deploy/cpt/cpt_aboutovf.html) format a toolit ktery pouziva virtual solutions activation engine  
OVA (Open Virtual Applience) je tar balicek obsahujici OVF soubory a potrebne soubory, popisujici vlastnosti virtualni masiny (HW na kterem pojede, jmeno, virtualni disky atd)  
**ICO 2.5**  
[Pridani immage do ICO 2.5](http://www.ibm.com/support/knowledgecenter/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/pc/pct_add_images_OpenStack.html)  
[Cloudbase-init - tutorial](http://cloudbase-init.readthedocs.io/en/latest/tutorial.html#execution)  
[Cludbase-init - documentation](https://media.readthedocs.org/pdf/cloudbase-init/latest/cloudbase-init.pdf)  
**YAML**  
[Popis YAMLu](http://docs.ansible.com/ansible/YAMLSyntax.html) - YAML Ain't Markup Language - na Ansible strankach  
[Heat Orchestration Template](http://docs.ansible.com/ansible/YAMLSyntax.html) - [YAML](http://yaml.org/) soubor na popsani Heat obrazu  
[Uvod do tvoreni Heat obrazu](https://support.rackspace.com/how-to/building-cloud-orchestration-templates/), [Heat obrazy1](https://developer.rackspace.com/blog/openstack-orchestration-in-depth-part-1-introduction-to-heat/) a [Heat obrazy 2](https://developer.rackspace.com/blog/openstack-orchestration-in-depth-part-2-single-instance-deployments/) na popsane naRackspace  

## ICO CLI

[deployer](http://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.4.0.2/com.ibm.sco.doc_2.4/cc/cct_initcli.html) -h SERVER -u USER -p PASSWORD ... interaktivni mod  
deployer -h SERVER -u USER -p PASSWORD -c "deployer.hypervisors" ... prikaz  
deployer -h SERVER -u USER -p PASSWORD -f skript.jy a1 a2 ... jython skript s argumenty a1, a2  

## Ukoly

**[Pridani noveho region serveru](https://www.ibm.com/support/knowledgecenter/SS4KMC_2.4.0/com.ibm.sco.doc_2.4/c_depl_region_server.html)**
mkdir -p /opt/stack/vmware/wsdl/5.0  
cd /opt/stack/vmware/wsdl/5.0  
for i in vimService.wsdl vim.wsdl core-types.xsd query-messagetypes.xsd query-types.xsd
vim-messagetypes.xsd vim-types.xsd reflect-messagetypes.xsd reflect-types.xsd; do
wget --no-check-certificate https://$VMWAREAPI_IP/sdk/$i; done  
opravit XML u reflect-messagetypes.xsd reflect-types.xsd  
ds wizard  

## URL

IP/orchestrator/v2/categories ... [REST API](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/c_core_services_api.html)  
/orchestrator/v2/[offerings](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/r_offering_instances.html)  
/orchestrator/v2/offerings/ID/launch ... spusti offering, vstup je pomoci POST ({"parm":{"OperationParameter":
"&lt;variable type=\"Sample_BusinessObject\|
&lt;field1 type=\"String\|<![CDATA[Hello]]>&lt;\/field1>
&lt;field2 type=\"String\|<![CDATA[Phone]]>&lt;\/field2> &lt;\/variable>"}})  
/orchestrator/v2/[instancetypes](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/r_resource_instances_api_v2.html)  
IP/orchestrator/v2/[tasks](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/r_task_engine_apiv2.html)  
/orchestrator/v2/instancetypes/project/instances  
https://IP/orchestrator/v2/instancetypes/stacktemplate/instances/241076 ... heat template  
/kernel/tasks/1521 ... informace o requestu 1521  
https://ico_server.example.com:443/orchestrator/v2/instancetypes/project/services/69/launch ... [akce](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/t_managing_entities_actions.html)  
[https://<ico_server_fqdn>:443/orchestrator/v2/offerings/<offering-id>/launch](https://www.ibm.com/support/knowledgecenter/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/c_launching_offering_via_offering_api.html)  
https://SERVER/orchestrator/v2/offerings/9/parameters ... ukaze parametry offeringu  
https://SERVER/orchestrator/v2/offerings/9/acl ... ukaze acl parametry offeringu  
https://SERVER/orchestrator/v2/offerings/9/acl ... ukaze grafickou reprezentaci offeringu  
/kernel/tasks  
/kernel/bpm/runbook/ ... list of all BPM processes  
/kernel/bpm/humanService  
/kernel/bpm/task ... Inbox  
https://mpllnx0276.mpl.michelin.com/teamworks/executeServiceByName  
/resources/services  
/resources/automationcategories  
/rest/bpm/wle/v1/process  
/rest/bpm/wle/v1/process/2920  

## Business process manager programovani

[IBM Cloud Orchestrator: Create a new management policy](https://developer.ibm.com/cloudorchestrator/videos/ibm-cloud-orchestrator-create-a-new-management-policy-2/)  
[Create a new use case for ICO Content Pack](https://developer.ibm.com/cloudorchestrator/2016/06/14/how-to-create-a-use-case-for-ico-content-pack-or-toolkit/)  
[Developers corner](https://developer.ibm.com/cloudorchestrator/docs/docs-overview-page/)  
https://developer.ibm.com/cloudorchestrator/videos/category/ibm-cloud-orchestrator-content/  

## Rozsireni

[Dockerfile and IBM Cloud Orchestrator](https://andrewyuau.wordpress.com/2014/10/23/dockerfile-and-ibm-cloud-orchestrator/)  
[IBM Cloud Orchestrator + Docker = ICOcker?](https://andrewyuau.wordpress.com/2014/10/21/ibm-cloud-orchestrator-and-docker/)  

- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;UrbanCode&nbsp;Deploy](https://www.ibm.com/us-en/marketplace/ico-content-pack-for-urbancode-deploy)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;Docker&nbsp;Integration](https://www.ibm.com/cz-en/marketplace/ico-content-pack-for-docker-integration)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;Tivoli&nbsp;Storage&nbsp;Manager](https://www.ibm.com/cz-en/marketplace/ico-content-pack-tivoli-storage-manager)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;Chef](https://www.ibm.com/ae-en/marketplace/cloud-orchestrator-content-pack-for-chef)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;IBM&nbsp;Endpoint&nbsp;Manager](https://www.ibm.com/cz-en/marketplace/ico-content-pack-for-endpoint-manager)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;IP&nbsp;Address&nbsp;Management](https://www.ibm.com/us-en/marketplace/ico-content-pack-ip-address-management)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;Control&nbsp;Desk](https://www.ibm.com/us-en/marketplace/ico-content-pack-for-control-desk)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;Pattern&nbsp;Management](https://www.ibm.com/uk-en/marketplace/ico-content-pack-for-pattern-management)
- [IBM&nbsp;Cloud&nbsp;Orchestrator&nbsp;Content&nbsp;Pack&nbsp;for&nbsp;ServiceNow](https://www.ibm.com/us-en/marketplace/ico-content-pack-for-servicenow)

## Problemy, trouble shooting

[[https://www.ibm.com/support/knowledgecenter/SS4KMC_2.5.0.1/com.ibm.ico.doc_2.5/t_pdcollect_run.html|
/opt/ibm/ico/orchestrator/pdcollect/pdcollect.py]] ... Problem Detemination Collect nastroj na sbirani dat pro IBM support  

### SCOrchestrator_Scripting_Utilities_Toolkit (SCOSUTK)

Umoznuje kopirovat soubory na servery a spoustet je pomoci ssh nebo RXA

### SCOrchestrator_Support_IaaS_Toolkit (SCOIAAS)

### SCOrchestrator Multi-Tenancy Toolkit (SCOMT)

#### BPD

Create Group Action,
Create Network in Project Action,
Create Project Action,
Create User Action,
Delete Group Action,
Delete Networks of Project Action,
Delete Project Action,
Delete User Action,
Disable Project Action,
Edit Project Action,
Edit User Action,
Enable Project Action,
Modify Availability Zones in Proj,
Modify Quota of Project Action,
Modify Users in Project Action
#### Integration Services

Check Assigned Resources For Project
Check Context User Can Access Domain
Check Context User Can Access Group
Check Context User Can Access Project
Check Context User Can Access User
Create Group
Create Network
Create Network (Neutron)
Create Project
Create User
Delete Group
Delete Network
Delete Network (Neutron)
Delete Networks of Project
Delete Project
Delete User
Disable Project
Get All AvailabilityZones
Get All Networks in Region
Get All Networks of Project
Get All Networks of Project (Ne
Get All Networks without Project
Get All Public Images
Get All Quota Limits of Domain
Get All Quota Limits of Project
Get Default Quota Limits in Reg
Get Domain
Get Domain from InstanceId
Get Domain from Login Context
Get Domain from OperationCont
Get Domain, User, Project and R
Get Domains
Get Group
Get Groups
Get Groups of Project with Role
Get Groups of User
Get Images of Project
Get InstanceId from OperationC
Get Networks
Get Networks (Neutron)
Get Networks without Project in
Get Ports (Neutron)
Get Project
Get Project from InstanceId
Get Project from OperationCont
Get Projects
Get Projects of Group with Role
Gets the projects where the given group is member
bpm_admin 9/14/16 4:38 PM
Get Projects of User with Role
Get Quota Limits For Domain
Get Quota Limits For Project in
Get Regions for Project And Ser,
Get Roles,
Get Roles for Tenant Users,
Get Roles of User in Project,
Get Subnets (Neutron),
Get User,
Get User Default Project,
Get User from InstanceId,
Get User from OperationContext,
Get Users,
Get Users of Group,
Get Users of Project with Role,
GetAvailabilityZonesForDomain,
GetAvailabilityZonesForProject,
GetAvailabilityZonesForRegion,
GetAvailabilityZonesForRegion,
Modify Project,
Modify User,
Set AvailabilityZones for Project,
Set Networks in Project,
Set Quota Limits For Project in,
Set Roles of User in Project,
Set Users in Project with Role,
Team Filter Service - All Users w,
Team Service - All Users in Domain,
Team Service - All Users in Proje,
Team Service - All Users with Ro,
#### BO

AvailabilityZone,
Domain,
Group,
Image,
KeystoneRole,
Network,
NeutronFixedIP,
NeutronNetwork,
NeutronPort,
NeutronSegment,
NeutronSubnet,
Project,
ProjectQuotaLimits,
RoleAssignment,
User

### SCOrchestrator Email Notification Toolkit (SCOEMAI)

### [SCOrchestrator_Toolkit](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0/com.ibm.ico.doc_2.5/enablement/scotoolkit.html) (SCOTLKT)

### SCOrchestrator_Azure_Toolkit (SCOAZUR)

### SCOrchestrator OpenStack Services (SCOOS)

#### BPD

Approve and Fetch User Email, Deploy Lamp Template, Deploy Single Virtual Machine,
  Deploy Single Virtual Machine with approval, Wait for VM Connection status  
#### Integration Service

Get Image, Get Instance Name, Send Email Notification, test_store_lamp  
#### BO

Image, SingleServerDeployment  

### SCOrchestrator Heat Support Toolkit (SCOHEAT)

<H5>BPO</H5>
 Delete Heat Stack,
Delete Heat Template,
Deploy Heat Template,
No Operation For Heat Template,
Update Heat Template,
Wait For Deletion of Heat Stack,
Wait For Status of Heat Stack,
#### Integration Services

Add Default ACL Entries,
Delete Single Heat Stack,
Delete Single Heat Template,
Get Available Templates,
Get Endpoints,
Get Heat Stack,
Get Heat Stack Instances,
Get Heat Stack Resources,
Get Heat Stacks From OpenStack,
Get Heat Template,
Get IaaS Regions for Service,
Get Services,
Get Services For Type,
Get Stack Instances,
Get Stack Template,
Get VM Instances For Stack,
Lookup Parameters,
Parse YAML,
Post Heat Template,
Store Heat Template,
Tag Heat VM MetaData,
updateHeatTemplate,
Upload Document,
Validate Heat Template,
Validate Template,
#### BO

ACLEntry,
Endpoint,
FileData,
Custom Controls,
HeatNetwork,
HeatStackDeploymentInfo,
HeatStackDetails,
HeatStackResource,
HeatTemplateFile,
HeatTemplateParameter,
HeatTemplateResource,
HeatVolume,
Image,
KeystoneService,
LinkedServer,
SingleFileImporterOutput,
YamlParseException
### [SCOrchestrator_OpenstackBlockStorage_Toolkit](https://www.ibm.com/support/knowledgecenter/en/SS4KMC_2.5.0.2/com.ibm.ico.doc_2.5/enablement/Cinder/cinder_intro.html) (SUPCIND)

#### BPD

Attach Script To Image
Attach Volume
Attach Volume Utility
Create Volume
Create Volume Utility
Create Volumes
Delete Volume
Detach Volumes
Manage Volumes
Script Upload Process
Unregister Scripts Process
#### Integration Services

Attach Volume Service
Configure Volume
Configure Volume for Windows
Create Volume Service
Delete Volume
Detach Volume
Detect Devices on Linux
Detect Devices on Windows
Format Volume on Linux
Format Volume on Windows
Get Attached Package List
Get Disk Info on Linux
Get Disk Info on Windows
Get Image Metadata
Get Info and Attach Volume for
Get List of Packages
Get Message
Get New Device
Get Pck Name of Image
Get Volume
Get Volume Attachment MetaData
GetAllRegisteredScripts_na
List Images
List Images 2
List Volume Types
List Volumes
Load Message Bundle
Partition Format Mount Volume
Partition Format Mount Volume
Remove Script Package
Set Volume Attachment MetaData
Set Volume Metadata
test
test_image
test_scriptname
Umount Attached Volume Partiti
Unset Volume Metadata
Update Image List
Update Image Metadata
Write File IS
#### BO

AttachVolumesToInstanceRequ
CinderBreadcrumbsObject
Image_Package_Data
PackageImagesBO
Script_Upload
VMCredentials
Volume
Volume_Attachment
VolumeManager
VolumeType
### SCOrchestrator Nova Support Toolkit (SCONOVA)

#### BDP

Attach Multiple Volumes,
Attach Volume,
Delete Virtual Machines,
Deploy Single Virtual Machine,
Register KeyPair,
Resize Virtual Machine,
Start Virtual Machines,
Stop Virtual Machines,
Unregister KeyPair,
Wait For Deletion Of VM,
Wait For Flavor Of VM,
Wait For Status Of VM,
#### Integration Service

Add MetaData To Server,
Add VM Tag To Database,
Check Extension Implemented B,
Check Key In Nova Key Store For,
Check Key in Use By Virtual Mac,
Check Key In Use For Region,
Check Nova KeyPair,
Check PCG Region,
This integration service uses the generic IaaS client,
Create Key In Nova Key Store Fo,
Create KeyPair in Nova Key Store,
Delete Key For Region,
Delete KeyPair from Credential,
Delete KeyPair from Nova Key S,
Delete Metadata Password,
Delete Metadata password,
Delete Servers,
Encrypt MetaData and UserData,
Get Availability Zones,
Get Create Key from Nova Key S,
Get Flavor,
Get Flavors,
Get Images,
Get Instance,
Get KeyPair from Nova Key Store,
Get KeyPairs from Credential St,
Get KeyPairs from Nova Key Store,
Get OpenStack API Extensions F,
Get Project User Domain Details,
Get Server,
Get Server Details,
Get Servers,
Get Single KeyPair from Credent,
Get Volume,
Get Volumes,
Has IaaS Service Endpoint in Reg,
Post Server,
Post Server Attach Volume,
Register KeyPair Service,
Sort Regions,
Start Servers,
Stop Servers,
Store KeyPair in Credential Store,
Tag Nova VM MetaData,
#### BO

Flavor,
FlavorSelection,
Image,
Instance,
Key,
NetworkAddress,
NovaKey,
OpenStackExtension,
ResizeVMData,
Server,
ServerDeployment,
ServerDetails,
ServerSelection,
Volume,
VolumeAttachment,

Umozni Deploy serveru, deploy se schvalenim a mailem a start/stop/delete VM

### Dashboards (SYSD)

### SCOrchestrator Service Composition Toolkit (SCOSCT)

### SCOrchestrator_Persistence_Base_Toolkit (ICPBTKT)

Umozni ulozit, ziskat, zmenit a smazat hodnotu v DB a zikat klice hodnot

### SCOrchestrator Coach Extension Toolkit (SCOCET)

### Content Management (SYSCM)

### Coaches (SYSC)

### System Data (TWSYS)

### SAP Guided Workflow (SGW)

### System Governance (TWSYSG)

## Databaze

CMNDB ... The common database  
BPMDB ... Process Server database  
PDWDB ... Performance Data Warehouse database  
db2 connect to CMNDB ... pripojeni k DB2  
db2 list tables for schema BPMUSER ... seznam tabulek  
db2 describe table BPMUSER.ACCOUNT  
db2 select \* from BPMUSER.LSW_TASK | tail ... tasky provadene BPMkem na ICO workflow  
db2 select \* from BPMUSER.LSW_USR_XREF ... uzivatele  
db2 select \* from BPMUSER.LSW_USR_GRP_XREF ... skupiny  
LSW_USR_GRP_MEM_XREF ... prirazeni uzivatelu do skupin
