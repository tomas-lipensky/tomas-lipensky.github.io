---
title: Vagrant
---

Abstrakcni vrstva pro virtualizacni reseni. Vagrant zajistuje jednotne
ovladani mnoha virtualizacnich technologii - libvirt, virtualbox,
vmware, kvn atd.

## prikazy

vagrant init custom ... ziniciuje vagrant v aktualnim adresari - vytvori json soubor s parametrama  

====Nastaveni VM aby podporovala Vagrant====

```
adduser vagrant
echo 'vagrant ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/vagrant
mkdir -p /home/vagrant/.ssh
chmod 0700 /home/vagrant/.ssh
curl https://raw.github.com/mitchellh/vagrant/master/keys/vagrant.pub > /home/vagrant/.ssh/authorized_keys
chmod 0600 /home/vagrant/.ssh/authorized_keys
chown -R vagrant /home/vagrant/.ssh
sed -e 's/^Defaults\(.*\)requiretty\(.*\)/#Defaults\1requiretty\2/' -i /etc/sudoers
sed -e 's/^Defaults\(.*\)visiblepw\(.*\)/#Defaults\1visiblepw\2/' -i /etc/sudoers
```

## logy, debugging, ...

export VAGRANT_LOG=debug ... zapne debug vypis Vagrantu  

====Instalace====

```
curl https://releases.hashicorp.com/vagrant/1.9.1/vagrant_1.9.1_x86_64.rpm
rpm -i vagrant*rpm
yum install libvirt-devel
vagrant plugin install vagrant-libvirt --plugin-version 0.0.35
```

====Priprava lib-virt boxu====

```
mkdir /vagrant
cd /vagrant

echo '{

  "provider"     : "libvirt",
  "format"       : "qcow2",
  "virtual_size" : 40
}' > metadata.json

echo 'Vagrant.configure("2") do |config| 
  config.vm.provider :libvirt do |libvirt|

    libvirt.driver = "kvm"
    libvirt.host = 'localhost'
    libvirt.uri = 'qemu:///system'
  end
  config.vm.define "new" do |custombox|
    custombox.vm.box = "custombox"
    custombox.vm.provider :libvirt do |test|
    test.memory = 1024
    test.cpus = 1
  end
end' > Vagrantfile
qemu-img convert -f raw -O qcow2  /var/lib/libvirt/images/test.img  box.img
tar cvzf custom_box.box ./metadata.json ./Vagrantfile ./box.img
vagrant box add --name custom custom_box.box
```

## Pripojeni na VM

wget https://raw.githubusercontent.com/hashicorp/vagrant/master/keys/vagrant ## Stahne privatni Vagrant klic  
chmod 600 vagrant # ... nastavi dobra prava (necitelne pro ostatni)  
ssh -p 2222 -i vagrant vagrant@127.0.0.1
