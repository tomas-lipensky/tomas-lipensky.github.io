# Automatizace

## Architektura

Automatizacni nastroje jsou aplikace, ktere slouzi k automaticke opakujici se cinnosti k ovladani jinych komponent. Obsahuji vetsinou nasledujici vrstvy:

- Prezentacni - webovy portal - aplikaci na aplikacnim serveru ktera slouzi k manazovani automatizace
- Vyvojove prostredi (IDE) k definovani automatizaci
- Automatizacni jadro (engine) vykonavajici automatizaci

## DevOps

Development &amp; Operations - nastroje na pruzny, rychly a bezpecny vyvoj a aplikaci na produkci.

[Objednani poskytovani u IBM: ](http://w3.devops.ibm.com/devops/#/toolchain/onboard)GitHub, Gerrit, Jenkins, uDeploy, Slack, Mural  
[GitHub enterprise](http://w3.devops.ibm.com/devops/#/toolchain/advanced/ghe) ... 150$/osoba/rok - portal - SCM, code review, trackovani problemu, publikace a integrace  
Github free ... volna verze  
Gerit ... volny webovy nastroj na spolupraci vyvojaru. Vyvojari vidi upravy jinych a mohou je schvalit/zamitnout. Spoluprace s SCM  
Slack ... 150$/osoba/rok - komunikacni nastroj se spolupracovniky s mnoha moznostmi  
Mural ... Vizualni organizace myslenek.

## Artifact repository

[Apache Archiva](https://archiva.apache.org/index.cgi)  
Nexus repository manager  
JFrog Artifactory  

## Automatizace integraci a nasazovani (Continues integration = CI, Continuous Deployment = CD)

[IBM UrbanCode (AnthillPro)](urbancode.html)  
[Jenkins](jenkins.html) / Travis  
[VSTS / Azure Devops](vsts.html) ... Visual Studio Team Services  
[Octopus](octopus.html) ... CD od Microsoft  
Buildbot — Python reseni na automatizaci kompilacnich/test cyklu k validaci zmen v kodu  
[Porovnani CI nastroju](https://en.wikipedia.org/wiki/Comparison_of_continuous_integration_software)  

## Automatizace konfiguraci a operaci, management cloudu

Pure AS ... Kompletni reseni HW+SW pro vytvareni a spravu aplikacnich serveru a aplikaci (a samozrejme nosnych virtualnich serveru)  
Pure DB ... Kompletni reseni HW+SW pro vytvareni a spravu databazi (a samozrejme nosnych virtualnich serveru)  
TPM - Tivoli Provisioning Manager ... Portal pro automatizaci instalaci serveru a aplikaci (TPM for Software, TPM for Images System x Edition, TPM Express for Inventory, TPM for Software distribution, IBM SmartCloud Cost Management/Patch management, IBM Clout Management Suite for System z  
[ICO - IBM Cloud Orchestrator](ico.html)  
OpenStack

## Automatizace instalace

cobbler ... reseni automatickou instalaci linuxu  

### Orchestrace provisioningu VM a kontejneru

[Vagrant](vagrant.html)  
[Kubernetes](Kubernetes)  
Boxgrinder  
Docker  
Hashicorp  

## Automatizace administrace stanic - planovane ukoly

Tivoli Endpoint Manager - BigFix - vzdalene spousteni skriptu (healthchecky, opravy, deploye atd.)  
[RES - automation management](http://www.ressoftware.com/uk/product/res-automation-manager/features)  

## Configuration management

[Chef](chef.html) - Opscode Chef / [programovani v Chef](chef-recipe.html)  
[Puppet](http://en.wikipedia.org/wiki/Puppet_%28software%29)  
Ansible  
[DSC](dsc.html) - MS Desired State Configuration  
Salt  
Vargant  
[Redhat Spacewalk](http://spacewalk.redhat.com/)  
NuGet a Chocolatey ... balickovaci system a deployment sluzba na automatizace konfigurace Windows  
[Porovnani CM nastroju](https://en.wikipedia.org/wiki/Comparison_of_open-source_configuration_management_software)  

## Automatizace na zaklade udalosti

Automatizace vyvolane na zaklade jistych udalosti (eventu), jako treba udalosti v monitoringu - incidenty.

<P>
IPSoft  
[TSA](http://www-03.ibm.com/software/products/en/tivoli-system-automation) - Tivoli System Automation ... reseni pro spravu automatizaci pro operatory - webovy portal nabizejici spousteni automatizaci (HA, performance) na zaklade pravidel  

## Cloud

IaaS - Infrastructure as a Service - automatizace datacentra - virtualni stroje, site  
SaaS - Software as a Service - automatizace aplikaci - vytvareni a manazovani aplikaci  
PaaS - Platform as a Service - vytvareni aplikacnich reseni z komponent (Napriklad BlueMix)  
Private cloud ... intranetovy cloud (Napriklad Pure atd)  
Public cloud ... internetovy cloud (Napriklad SoftLayer, Amazon atd)  
Hybrid cloud ... hybrid mezi Private a Public  

## Cloud platformy a abstrakce virtualizaci

poskytuji management objektu (virtualnich serveru, kontejneru, disku, ...), nacenovani ceny, separuji ucty (projekty) atd.

[OpenStack](https://wiki.openstack.org/wiki/Main_Page) ... OpenSource Cloud Computing platforma  
[Heat](https://wiki.openstack.org/wiki/Heat) ... Orchestracni engine, Heat template (v textove forme)  
[OpenWhisk](https://openwhisk.apache.org) ... abstrakce virtualizaci bezserverovych kontejneru (Docker)  
VMware vSphere  
Kubernetes and Containers  
[IBM Cloud Private](icp.html)  
BlueMix Private ... Zjednoduseny BlueMix ve vlastnim datacentru  
Azure Stack ... zjednoduseny Azure ve vlastnim datacentru  
[Terraform](https://www.terraform.io) ... nastroj na managovani konfigurace infrastruktury (pomoci chef, heat, ...)  

## Public cloud

[Prehled poskytovatelu na Wikipedia.org](https://en.wikipedia.org/wiki/Category:Cloud_computing_providers)  

[BlueMix](bluemix.html) ... IBM Cloud / BlueMix / [Softlayer](softlayer.html)  
    [Azure](azure.html) ... Microsoft Azure  
    [AWS](aws.html) ... Amazon AWS  
    Rackspace  
    [IBM Blue Box](https://www.blueboxcloud.com/products/blue-box-local) - Private Cloud as a Service - postaveny na OpenStack reseni, Bluemixu - Cloud-like prostredi v zakaznickem datacentru  

## Private cloud

[xCAT](https://sourceforge.net/p/xcat/wiki/Main_Page/) ... Extreme Cluster/Cloud Administration Toolkit
