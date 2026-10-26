---
title: Virtualizace - Virtualni pocitace
---

## KVM

Linux reseni - interni odkaz [lin-vpars.html](lin-vpars.html)

## libvirt

Linux reseni - interni odkaz [lin-vpars.html](lin-vpars.html)

#### XEN

Linux reseni - interni odkaz [lin-vpars.html](lin-vpars.html)

## [VirtualBox](http://www.virtualbox.org/)

Linux prikazy na internim odkazu [lin-vpars.html](lin-vpars.html)

## [VMWare](http://www.vmware.com/cz/)

Linux prikazy na internim odkazu [lin-vpars.html](lin-vpars.html) a [esx.html](esx.html)

## Docker

## Eucalyptus - cloud solution from Ubuntu

sudo euca_conf --no-rsync --discover-nodes ... zapne node controler  
cd ~/.euca; sudo euca_conf --get-credentials mycreds.zip; unzip mycredents.zip ... ziska kredence od node controleru  
euca-describe-availability-zones verbose ... ukaze virtualni pocitace a jejich stav  
euca-add-keypair mykey > ~/.euca/mykey.priv ... generovani SSH paru klicu  
euca-authorize default -P tcp -p 22 -s 0.0.0./0 ... povoli ssh tok ze vsech mist  
euca-run-instances emi-A1 -k mykey -t c1.medium ... spusti image  
wait -n5 euca-describe-instances ... kontroluje stav instance, aby jsme vedeli, kdy nastartovala  

## [Vagrant](https://en.wikipedia.org/wiki/Vagrant_%28software%29)

Virtualizacni konfigurator nad jednotlivymi virtualizacnimi resenimi.

# Virtualni masiny (pocitace) - VM

VM s Internet Expolorer - https://dev.modern.ie/tools/vms/linux/t
