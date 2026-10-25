# chef

### Chef

Configuration management nastroj. Jednotlive configuracni kroky jsou nazyvany recepty. Sady receptu jsou kucharky.  
Chef muze fungovat jako server/klient - klient uklada konfiguraci prostredi do serverove databaze, recepty pak mohou tato data uzivat. Druhy rezim prace se "Chef-solo".
Objekty:  
- Repozitar - obsahuje kucharky
- kucharky - obsahuji recepty, atributy (default.rb), definice (/definitions), soubory (/files), klihovny (/libraries), metadata (metadata.rb), [vestavene](https://docs.chef.io/resources.html) a [vlastni](https://docs.chef.io/lwrp.html) resources  (maji ruzne typy - package, template, service) a vzory (/templates), testy. Kucharky mohou mit verze
- recept - postupy
- (template) vzor - staticka reprezentace souboru pro knihovny
- runlist - usporadany seznam receptu vybranych pro klienta
- environment - prostredi - prod, preprod, test
- politiky - role (web server, db), environment (prod), data bags (hesla atd), kucharky (verzovane)
- role - obsahuji 0 a vic atributu a runlistu. Kazdy node muze mit 0 a vice roli

### Odkazy

[Chef kucharky a recepty](chef-recipes) - popis programovani Chef cookbook a recipe  
[www.chef.io](https://www.chef.io/) ... domovska stranka  
[learn.chef.io](https://learn.chef.io/) ... tutorial Chefu  

### Komponenty

[Chef Development Kit](https://downloads.chef.io/chef-dk/)  
[Chef Supermarket](https://supermarket.chef.io/cookbooks) - webovy repozitar volnych kucharek (cookbooks). Nastroje:
1. [Bekrshef](https://docs.chef.io/supermarket.html)-zavislosti mezi supermaketma  
2. [Stove](https://github.com/sethvargo/stove) - nastron na baleni a publikovanic chef kucharek
[Privatni supermarket](https://github.com/chef/supermarket), [Supermarket na ominibusu](https://github.com/chef/omnibus-supermarket) - kitched-based prostreni pro omnibus balicky  

Chef Analytics - platforma na analyzu historickych akci a behu a notifikaci  
Chef Server - ma na starosti ulozeni receptu/kucharek/konfiguraci - tzv. chef-repo, obsahuje GUI  
Chef Client - managovany node - klient co se umi pripojit k serveru a stahnout recepty a vykonat je, predat statistiky pro server  
WorkStation - vyvojova stanice obvykle s Development Kitem na vytvareni a testovani kucharek  

Chef Vault - bezpecnostni vrstva na mangovani data bags - json hodnot, obsaujici treba kredence  
[Kitchen](http://kitchen.ci/) - prostreni pro testovani receptu/kucharek - soucast DK  
ChefSpec - testovaci nastroj na testovani resourcu a receptu - rozsireni RSpec (soucast DK)  
Foodcritic - testovaci nastrok (soucast DK)  
Chef Automate - nabizi nastroj pro spojite dodavani infrastrukturt i aplikaci, pouziva inSpec a Habitat  
InSpec - testing framework for infrastricture - complience and security rules  
Habitat - zabaleni aplikace a automatizace do jednoho celku  
Ohai - nastroj na detekci atributu nodu a poskytnuji jich klientovi, soucasti instalace klienta i DK  
chef-zero ... nastroj na provadeni receptu bez Chef serveru.  

### Chef server

chef-server-ctl status ... status sluzeb  
chef-server-ctl reconfigure  
chef-server-ctl org-list ... seznam organizaci  
chef-server-ctl user-list ... seznam uzivatelu  
chef-server-ctl org-user-add ORG USER ... prida uzivatele USER do organizace ORG  
chef-server-ctl tail ... seznam log souboru a poslednich zaznamu  
[chef-server-ctl](https://docs.chef.io/server_users.html) user-create TLIP Tomas Lipensky tlip@email.ad 'heslo' ... vytvori noveho uzivatele  
/var/opt/opscode/nginx/ca/chef-server.crt ... verejny certifikat k https Chef serveru, pouzije se v klientech v trusted_certs  
/etc/chef-server/*pem ... klice  
chef generate repo my_chef_repo my_chef_repo; cd my_chef_repo ... vytvori repozitar  
chef generate cookbook cookbooks/cookbook_httpd ... vytvori cookbook  
chef generate template cookbooks/cookbook_httpd index.html ... vytvori template - index.html.etb  
chef generate recipe cookbooks/cookbook_httpd index_page ... vytvori recept v kucharce  
knife exec -E 'api.delete("/association_requests/0a42df32f017ea88e4465168a755a4e1")' -s 'https://localhost/organizations/spolek' -u pivotal -k /etc/opscode/pivotal.pem ... odebere pozvanku do organizace  
knife raw /groups -s 'https://localhost/organizations/spolek' -u pivotal -k /etc/opscode/pivotal.pem ... Seznam skupiv v organizaci  
knife raw https://mpllnx0189.mpl.michelin.com:443/organizations/michelin/search/node?q=*:* ... API prikaz search - vystup JSON  
knife exec -E "search(:node,'*:*').select{|n|n.run_list.empty?}.each{|n| puts n.name}" ... Jiny zpusob hledani, konkretne nody s prazdnym runlistem, vystup JSON  

### Chef workstation

chef-apply hello.rb ... aplikuje Ruby recept  
knife configure  ... zkonfiguruje workstation  
/etc/chef/*.pam, ~/.chef, c:\chef ... klic pro workstation  
knife ssl fetch -s https://chefserver:443 ... ziska klic ze serveru a prida to do trusted store - veri serveru  
knife ssl check -s https://chefserver:443 ... otestuje klic pro node  
$HOME/.chef/[knife.rb](https://docs.chef.io/config_rb_knife.html) ... konfiguracni soubor klienta (knife)  
knife client list ... z workstation vylistuje nody  
knife client show CLIENT ... ukaze informace o klientovi  
knife user list ... z workstation ukaze uzivatele  
[knife node](https://docs.chef.io/knife_node.html) list ... seznam nodu  
[knife bootstrap windows winrm 1.2.3.4 -A administrator -P heslo](https://developer.rackspace.com/blog/step-by-step-walkthrough-to-using-chef-to-bootstrap-windows-nodes-on-the-rackspace-cloud/) ... vzdaleny bootstrap windows klienta (pekny popis na Rackspace)  
knife [search](https://docs.chef.io/knife_search.html) node "tags:*ubuntu* OR roles:*ubuntu* OR NOT fqdn:*ubuntu* (etc.)" -a chef_environment ... hledani, vystup v txt, filtr na hodnoty (ukaze jen chef_environment)  
knife search "platform:ubuntu* AND chef_environment:*_T_*" -a chef_environment ... AND podminka  
[knife exec -E "nodes.find(“role:web_server”) {|n| n.run_list.remove(“role[web_server]“); }"](https://gist.github.com/ipedrazas/aadbaeb808f5ace5d3ce) ... odebere role web_server vsem nodum s roli web_server  
knife exec -E "nodes.transform(“chef_environment:_default”) { |n| n.chef_environment(“production-VM”) }" ... zmena chef environmentu  
knife exec -E "nodes.transform(“NOT platform:win*“) {|n| puts n.run_list &lt;&lt; “role[linux]“; n.save }" ... prida role do runlistu  

#### Rozsireni

Pomoci Chef DK lze rozsirovat knife o dalsi moduly, napr.:

[chef gem install knife-acl](https://github.com/chef/knife-acl) ... nainstaluje novy gem knife-acl  
[knife acl](http://www.rubydoc.info/gems/knife-acl/0.0.12) add group clients nodes cheftest1 update ... prida skupine clients k nodu cheftest1 pravo update  

### Chef klient

Chef klient je specialni uzivatel, ktery reprezentuje identitu (osobu) pocitace, ktera se pripojuje
Chef nodu na Chef server. Chef node je reprezentace masiny. Vytvoreni managovane masiny se sesklada
z registrace node a klienta na Chef serveru, instalaci Chef klient programu na vzdalene masine a
nastaveni C:\chef nebo /etc/chef, nebo ~/.chef profilu pro chef-client ([client.rb](https://docs.chef.io/release/11-18/config_rb_client.html)). To vze se da udelat
vzdalene z Chef workstation pomoci prikazu "chef bootstrap", kde se pomoci ssh, ci winrm pripoji chef k
serveru, stahne instalacku, nainstaluje, nakonfiguruje profil vcetne klicu, zaregistruje node a clienta
v chef serveru.

#### Instalace

[knife bootstrap](https://docs.chef.io/install_bootstrap.html) windows winrm 95.138.188.93 -x Administrator -P A7not3si5ELo ... provede vse z workstation co je popsano nize  
[knife client](https://docs.chef.io/knife_client.html) create cheftest1 ... vytvori novou identitu cheftest1 na chef serveru, vytvori klic  
knife node create cheftest1 ... vytvori novy objekt node cheftest1 na chef serveru  
rpm -i chef-12.9.41-1.el6.x86_64.rpm ... instalace klineta  
mkdir /etc/chef ... vytvori adresar pro konfiguraci  
cp chef-validator.pem /etc/chef/validation.pem ... zkopiruje validation privatni klic nutny k registraci klienta/node  
knife ssl fetch -s https://chefserver:443 ... ziska verejny klic chef serveru a prida jej do klicenky duveryhodnych serveru pro knife prikaz  
cp -r $HOME/.chef/trusted_certs /etc/chef/ ... prekopiruje klicenku do konfiguracniho adresare klienta

```
echo '
log_level        :info
log_location     STDOUT

chef_server_url  "https://chefsrv.ico25.com/organizations/tlorg"
validation_client_name "tlorg-validator"
client_key       "c:/chef/test_node.pem"
validation_key   "c:/chef/validation.pem"

file_cache_path  "c:/chef/cache"
file_backup_path "c:/chef/backup"

node_name        "test_node"

trusted_certs_dir "c:/chef/trusted_certs"' > c:/chef/client.rb
```

knife ssl check -c C:\chef\client.rb ... overi SSL certifikaci vudci [client.rb](https://docs.chef.io/release/11-18/config_rb_client.html) (klientske konfiguraci)  
chef-client ... klient se pripoji k Chef serveru a pokusi se vykonat runbook ([mozne problemy](https://docs.chef.io/errors.html#forbidden)  

chef-client ... registruje node na serveru, pouzije konfiguraci z konfiguracniho souboru client.rb  
chef-client -S https://chefserver:443 -K /etc/chef/chef-validator.pam ... chef-client prijima i argumenty v prikazove radce  
/etc/chef/*.pam, ~/.chef, c:\chef ... klice pro klienta  

### Databag

Skladiste dat pro jednotlive nody atd., muze obsahovat duverna data jako hesla, promenne atd.

knife vault delete sea power ... smaze databag  

### Chef cookbook

knife cookbook create motd  
vi $COOKBOOKS/motd/recipes/a.rb  
knife cookbook test motd  
knife cookbook upload motd  
knife cookbook list  
knife node run_list add tluatwb1 motd  
chef-client ... aplikuje recept na klientovi  
chef-client --local-mode hello.rb ... aplikuje recept na lokalnim stroji  
chef-client --local-mode --runlist 'recipe[cookbook_httpd::default]' ... aplikuje runbook, ktery obsahuje jen jeden recept "default" z kucharky "cookbook_httpd"  
chef-client -z -o helloworld ... aplikuje cookbook helloworld (~/cookbooks/helloworld/recipes/default.rb)  

#### Supermarket

chef gem install knife-supermarket - nainstaluje knife supermarket na Workstation aby se dalo pracovat se Supermarketem  
chef install knife-supermarket  
[supermarket-ctl reconfigure](https://github.com/chef/omnibus-supermarket/tree/master/cookbooks/omnibus-supermarket) - nastroj na provadeni omnibus balicku  
[supermarket-ctl](https://docs.chef.io/ctl_supermarket.html) - prikaz na ovladani Supermarketu - start, stop sluzeb, konfigurace atd  
[knife.rb](https://docs.chef.io/config_rb_knife.html) - pridej "knife[:supermarket_site] = 'https://your-private-supermarket'" odkaz na vlastni supermarket  
knife ssl fetch https://default-centos-66 - ziska ssl udaje  
knife ssl check https://default-centos-66 - overi je  
knife supermarket share mycookbook "Other" - uploadne kucharku na Supermarket  
[knife supermarket](https://docs.chef.io/plugin_knife_supermarket.html) - interaktovani se supermarketem, download, search, install, list nepotrebuje ucet  
[supermarket.rb](https://docs.chef.io/config_rb_supermarket.html) ... parametry sypermarketu  
supermarket-ctl-reconfigure ... rekonfigurace Supermarketu po zmene udaju  
[RESTful API](https://supermarket.chef.io/api/v1/cookbooks)  
Popis API - [https://docs.chef.io/api_cookbooks_site.html](https://docs.chef.io/api_cookbooks_site.html)  
fieri - dodatecna sluzba Supermarketu na testovani verze kucharek, musi se povolit  

#### role

[Pekny tutorial](http://mycodingtales.com/posts/automation-with-chef-part-4-setting-up-chef-client/) na vytvoreni role  
knife role list ... seznam roli  

#### Kitchen

definice v  .kitchen.yml  
Umoznuje testovani kucharky v mnoha kloudech a virtualizacich  
Nabizi image z <a href=https://github.com/chef/bento|Bento]]  

### [Cena](https://www.chef.io/pricing/), licence

Chef Basics - zadarmo  
[Hosted Chef](https://manage.chef.io/signup) - do 5 zadarmo, vic jak 5 72$ za rok/instance  
[Chef Automate](https://www.chef.io/automate/) - $137/instance/rok - obsahuje Chef Manage (Web Management portal) a jine  

### Chef recepty

#### Promenne

[node['platform'](https://docs.chef.io/attributes.html)] ... Operacni system node, napr. 'windows'  
node['platform_version'], node['ipaddress'], node['macaddress'], ... dalsi promenne  
[node.default['apache']['dir'](https://docs.chef.io/attributes.html)] ... promenna z konfiguracniho souboru (cookbook/attributes)  
node.chef_environment ... prostredi  
node.name

### Tridy

this_node=[Chef::Node](http://www.rubydoc.info/github/opscode/chef/Chef/Node).load(node.name) ... vytvori objekt, do ktrereho se nacte Chef objekt - node  
this_node.run_list &lt;&lt; "role[windows100]" ... nastavi run list  

### resources

[Vytvareni vlastnich LWRP resources](https://docs.chef.io/custom_resources.html)  
[Vytvareni LWRP resources](http://dougireton.com/blog/2012/12/31/creating-an-lwrp/)

```
file '/etc/motd' do
      content 'Welcome to Chef'
end
```

```
file '/tmp/motd' do
  action :delete
end
```

```
package 'httpd'

service 'httpd' do
  action [:enable, :start]
end

template '/var/www/html/index.html' do
  source 'index.html.erb'
end
```
