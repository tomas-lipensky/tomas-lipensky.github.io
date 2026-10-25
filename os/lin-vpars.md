# LINUX - Virtualni pocitace

* Pro virtualizaci W2012, W10, W8 je potreba zapnout ochranu pameti v biosu, jinak se OS nespusti.
* Pri konverzi obrazu z VMWare do KVM se smeni SATA radic na IDE. [Je treba radic zmenit](https://rbgeek.wordpress.com/2013/08/13/converting-a-vmware-workstation-virtual-machine-to-kvm/), jinak nenastartuje system, hlavne Windows

### KVM

##### KVM - Kernel Based Virtual Machine

balicky: kvm virt-manager libvirt libvirt-python python-virtinst  

[KVM home page](http://www.linux-kvm.org/page/Main_Page)  
[How to create KVM machine on F14](http://www.howtoforge.com/virtualization-with-kvm-on-a-fedora-14-server)  
lsmod kvm  
modprobe kvm  
modprobe kvm-intel  
kvm-img create fedora15.img 15G ... vytvori image soubor  
kvm -hda ubuntu.qcow -vga std ... spusti VM  
kvm -m 768 -boot d -cdrom ~/iso/Fedora-15-x86_64-DVD.iso -hda fedora15.img & ... namountuje  CD/DVD z iso souboru  
ibm-virt-viewer -a -c qemu:///system KVM_Windows_7-KVM ... spusti prohlizec konzole (i grafice) virtualniho stroje  
virt-manager ... manazer virtualnich stroju  
/usr/libexec/qemu-kvm -name KVM_Windows_7-KVM -S -M rhel6.3.0 -cpu SandyBridge,+erms,+smep,+fsgsbase,+rdrand,+f16c,+osxsave,+pcid,+pdcm,+xtpr,+tm2,+est,+smx,+vmx,+ds_cpl,+monitor,+dtes64,+pbe,+tm,+ht,+ss,+acpi,+ds,+vme,-nx -enable-kvm -m 2528 -smp 2,sockets=2,cores=1,threads=1 -uuid bfe1da6a-0f39-4045-a7a8-4fc57791a907 -smbios type=0,vendor=LENOVO,version=G1ET41WW (1.16 ),date=05/25/2012,release=1.16 -smbios type=1,manufacturer=LENOVO,product=2350B58,version=ThinkPad T430,serial=PB19T9T,sku=LENOVO_MT_2350,family=ThinkPad T430 -nodefconfig -nodefaults -chardev socket,id=charmonitor,path=/var/lib/libvirt/qemu/KVM_Windows_7-KVM.monitor,server,nowait -mon chardev=charmonitor,id=monitor,mode=control -rtc base=localtime -no-shutdown -device ich9-usb-ehci1,id=usb,bus=pci.0,addr=0x8.0x7 -device ich9-usb-uhci1,masterbus=usb.0,firstport=0,bus=pci.0,multifunction=on,addr=0x8 -device ich9-usb-uhci2,masterbus=usb.0,firstport=2,bus=pci.0,addr=0x8.0x1 -device ich9-usb-uhci3,masterbus=usb.0,firstport=4,bus=pci.0,addr=0x8.0x2 -device virtio-serial-pci,id=virtio-serial0,bus=pci.0,addr=0x5 -drive file=/var/lib/libvirt/images/KVM_Windows_7-KVM.qcow2,if=none,id=drive-virtio-disk0,format=qcow2,cache=writeback -device virtio-blk-pci,scsi=off,bus=pci.0,addr=0x6,drive=drive-virtio-disk0,id=virtio-disk0,bootindex=1 -drive if=none,media=cdrom,id=drive-ide0-1-0,readonly=on,format=qcow2 -device ide-drive,bus=ide.1,unit=0,drive=drive-ide0-1-0,id=ide0-1-0 -netdev tap,fd=22,id=hostnet0,vhost=on,vhostfd=23 -device virtio-net-pci,netdev=hostnet0,id=net0,mac=52:54:00:1a:93:59,bus=pci.0,addr=0x3 -chardev pty,id=charserial0 -device isa-serial,chardev=charserial0,id=serial0 -chardev pty,id=charchannel0 -device virtserialport,bus=virtio-serial0.0,nr=1,chardev=charchannel0,id=channel0,name=arbitrary.virtio.serial.port.name -chardev spicevmc,id=charchannel1,name=vdagent -device virtserialport,bus=virtio-serial0.0,nr=2,chardev=charchannel1,id=channel1,name=com.redhat.spice.0 -device usb-tablet,id=input0 -spice port=5900,addr=127.0.0.1,disable-ticketing,seamless-migration=on -vga qxl -global qxl-vga.ram_size=67108864 -global qxl-vga.vram_size=67108864 -device intel-hda,id=sound0,bus=pci.0,addr=0x4 -device hda-duplex,id=sound0-codec0,bus=sound0.0,cad=0 -chardev spicevmc,id=charredir0,name=usbredir -device usb-redir,chardev=charredir0,id=redir0,bus=usb.0,port=3 -chardev spicevmc,id=charredir1,name=usbredir -device usb-redir,chardev=charredir1,id=redir1,bus=usb.0,port=4 -chardev spicevmc,id=charredir2,name=usbredir -device usb-redir,chardev=charredir2,id=redir2,bus=usb.0,port=5 -chardev spicevmc,id=charredir3,name=usbredir -device usb-redir,chardev=charredir3,id=redir3,bus=usb.0,port=6 -device virtio-balloon-pci,id=balloon0,bus=pci.0,addr=0x7
 ... spusteni VM s parametry  
guestmount -c qemu:///system -d Virtual_Client_for_Linux_Windows_7-KVM -m /dev/sda2 --rw /tmp/mount/ ... namountovani disku z virtualni masiny na hostitelskou  
guestmount -a /var/lib/libvirt/images/xenserver.qcow2 -m /dev/sda1 /mnt ... namountuje qcaw2 image  
mount -o loop rawimage.img /mnt/tmp ... namountuje raw image  
kpartx -l /var/lib/libvirt/images/guest1.img ... vylistuje partitions na obrazu  
kpartx -a /var/lib/libvirt/images/guest1.img ... vytvori loopback zarizeni v /dev/mapper k partition na obrazu  
mount -o loop /dev/mapperloop0p1 /mnt/tmp ... namountuje partition  
vgscan ... nadetekuje nove PV a VG  
vgchange -ay VolGroup00 .. aktivuje VG  
kpartx -d /var/lib/libvirt/images/guest1.img ... zrusi maping loop zarizeni k obrazu  
virsh -c qemu:///system list --all ... vylistuje vsechny virtualni masiny  
qemu-img convert winxp.vmdk -O qcow2 /var/lib/libvirt/images/winxpvm.img ... prekonvertuje vmdk diskovy kontejner na qcow2 format  
qemu-img convert -f raw disk.raw -O qcow2 disk.qcow2 ... prevede raw format na qcow2  
ls -l /etc/libvirt/qemu/  
virt-install -n MDMCSedu --os-type=Linux --ram=2048 --vcpus=2 --import --disk path=/var/lib/libvirt/images/CentOS-7-edu.img,bus=virtio --network bridge:virbr0 --force
0  
virsh console myRHELVM1 ... pripoji se na konzoli  
virsh dominfo myRHELVM1 ... informace o VM  
virt-top ... informace o systemovych prostredcich co berou VM  
virsh start MDMCS ... spusti VM MDMCS  
virsh shutdown MDMCS ... posle signal k zastaveni VM  
virsh destroy VM ... okamzite vypne VM  

### LXC - Linux Container

lxc-create -n web1 -t Ubuntu  
lxc-start -n web1 -d  
lxc-attach -n web1  
lxc-ls --fancy ... seznam kontejnerů  
### libvirt

Je potreba podpora virtualizace v jadru, viz sekce KVM a XEN

service libvirtd start/stop/status ... Virtualizacni sluzba  
pygrub /dev/VolGroup00/wspd ... bootloader pro virtualni masiny  
virsh shutdown MACHINE ... vypne virtualni stroj MACHINE  
virsh start MACHINE ... zapne virt. stroj machine  
virt-install -n VirtFed11 -r 512 -f /dev/vgTL/LV.virtFed12 -l http://mirror.karneval.cz/pub/fedora/releases/11/Fedora/i386/os -w network:default ...  
 vytvori virtualni stroj, 512 MB ram, disk - LV.virtFed12, instalace z dane adresy  
virt-manager ... graficke sprava, ovladani a vytvareni virtualnich stroju  
virt-view MACHINE ... otevre okno s pohledem na obrazovku virtualniho stroje MACHINE  
virsh -c qemu:///system list ... seznam virtualnich stroju  
virt-install --connect qemu:///system -n vm10 -r 512 --vcpus=2 -f ~/vm10.qcow2 -s 1 -c /mnt/auto/win/Y82583/zip/CentOS-5.5-i386-netinstall.iso --vnc --noautoconsole --os-type linux --os-variant debianlenny --accelerate --hvm

##### XEN

balicky: xen, virt-manager, xen-tools  
grep flags /proc/cpuinfo ... test, zda je tam prepinac "pae"  
xm create wspd -n ... vytvori virtualni masinu ze souboru wspd  
xm create -c MACHINE ... necha vybrat z GRUBu pri startu virt. stroje MACHINE  

### Virtual Box

[VirtualBox](http://www.virtualbox.org/) virtualizacni reseni
##### Instalace

wget http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo ... instalace repo souboru  
yum update ... update kernelu a balicku  
yum install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms ... instalace zavislosti  
yum install VirtualBox-5.0 ... instalace VBoxu  
/etc/init.d/vboxdrv setup ... konfigurace modulu jadra  

##### prikazy, konfigurace

ls ~/VirtualBox\ VMs/ ... misto defaultnich VM obrazu  

VBoxManage clonehd disk.vdi disk.raw --format raw ... naklonuje VBox disk na raw format  
VBoxManage createvm -name Centos-5.5-im5 -register ... Vytvori novy profil virtualni masiny a zapise jej do konfigurace VM  
VBoxManage createvdi -file /vm/HDD-Centos-5.5-im5.vdi -size=8000 -register ... vytvori oddil pro disk o velikosti 8GB a zapise na disk  
VBoxManage internalcommands sethduuid Centos-5.5-im5.vdi ... zmena UUID disku (nelze mit v repozitari disku 2 disky se stejnym UUID)  
VBoxManage modifyvm Centos-5.5-im5 Centos-5.5-im5 -hda HDD-Centos-5.5-im5 ... Prida virtualnimu pocitaci HDD  
VBoxManage modifyvm Centos-5.5-im5 Centos-5.5-im5 -dvd /vm/Centos.iso ... vsune do virtualni mechaniky DVD  
VBoxManage modifyvm Centos-5.5-im5 --memory 512 ... zmena VM - nastaveni pameti na 512MB  
VBoxManage modifyvm Centos-5.5-im5 --acpi off ... vypni ACPI  
VBoxManage modifyvm Centos-5.5-im5 --boot1 dvd ... prvni bootovaci menium DVD  
VBoxManage modifyvm Centos-5.5-im5 --nic1 bridged ... nastaveni 1. sitoky na typ bridged  
VBoxManage modifyvm Centos-5.5-im1 --bridgeadapter1 eth0 ... spoji bridgovany virtualni adapter se sitovou kartou eth0  
VBoxManage modifyvm Centos-5.5-im1 --macaddress2 0800276F3BB1 ... nastavi MAC adresu  
VBoxManage registerimage dvd /vm/Centos.iso ... zaregistruje ISO instalacniho DVDcka  
VBoxManage storagectl Centos-5.5-im5 --name SATA1 --add sata ... Prida sata radic SATA1  
VBoxManage storageattach Centos-5.5-im5 --storagectl SATA1 --port 0 --device 0 --type hdd --medium /mnt/vm/Centos-5.5-im5.vdi ... k radici SATA1 pripoji harddisk  
VBoxManage showvminfo Centos-5.5-im5 ... ukaze nastaveni VM Centos-5.5-im5
VirtualBox ... graficky manazer  
VirtualBox --startvm Centos-5.5-im1 ... spusti obraz, vytvori okno s konzolou  
VBoxHeadless -s Centos-5.5-im1 ... spusti VM, ale nevytvori okno s konzolou  
VBoxTunctl -b -u scottro ... pro uzivatele scottro prida virtualni sitovou kartu toc1 (pro bridge)  

[Migrace existujicich Windows do VirtualBoxu](http://www.virtualbox.org/wiki/Migrate_Windows)  
[Guest addition pack](http://download.virtualbox.org/virtualbox/) ... Zkompiluje se do hostovaneho OS - podpora sdilene schranky, graficke ovladace, sdilene adresare, ...  
mount -t vboxsf share ~/host ... namountovani sdileneho adresare na hostovi  
[Manual pro VirtualBox](http://www.virtualbox.org/manual/)  
xclip ... program na ukladani schranky do souboru a cteni zchranky ze souboru pro nefungujici sdilenou schranku (gclip pro windows)  

### VMware

[VMWare](http://www.vmware.com/cz/) virtualizacni reseni  

vmware-mount - mountovani vmware obrazu - balicek vmware-player, vmware-vix-disklib-distrib  
vmware-mount -p CentOS-5.5-i386-virtual-machine-org.vmdk ... ukaze jednotlive oddily obrazu  
vmware-mount CentOS-5.5-i386-virtual-machine-org.vmdk /mnt/0 ... Namountovani obrazu  
vmware-mount CentOS-5.5-i386-virtual-machine-org.vmdk 5 /mnt/5 ... Namountovani 5 oddilu obrazu  
vmware-vdiskmanager fedora20-multi.vmdk -t 0 fedora20-uni.vmdk ... prevede multi part diskovy kontejner na jeden soubor  
/etc/vmware/vmnet8/nat/nat.conf ... definice sitoveho nastaveni, vcetne port forwardingu  

##### Konverze vmware obrazu do virtualboxu

vmware-vdiskmanager -r CentOS-5.5-i386-virtual-machine-org.vmdk -t 0 flattened.vmdk ... slouceni vicesvazkoveho VMware obrazu do jednosvazkoveho  
qemu-img convert flattened.vmdk -O raw rawfile.bin  
VBoxManage convertdd rawfile.bin CO.vdi  

### Eucalyptus - cloud solution from Ubuntu

sudo euca_conf --no-rsync --discover-nodes ... zapne node controler  
cd ~/.euca; sudo euca_conf --get-credentials mycreds.zip; unzip mycredents.zip ... ziska kredence od node controleru  
euca-describe-availability-zones verbose ... ukaze virtualni pocitace a jejich stav  
euca-add-keypair mykey > ~/.euca/mykey.priv ... generovani SSH paru klicu  
euca-authorize default -P tcp -p 22 -s 0.0.0./0 ... povoli ssh tok ze vsech mist  
euca-run-instances emi-A1 -k mykey -t c1.medium ... spusti image  
wait -n5 euca-describe-instances ... kontroluje stav instance, aby jsme vedeli, kdy nastartovala  

### Odblokovani Windows virtualniho pocitace (zapomenute heslo)

chntpw -l /tmp/mount/Windows/System32/config/SAM ... vylistovani uctu ve Windows  
chntpw /tmp/mount/Windows/System32/config/SAM -u USER ... vymaze heslo u uzivatele  

### WINE

Funkcni instalace .NET do WINE na [winehq.org](https://appdb.winehq.org/objectManager.php?sClass=version&iId=25478) projektu  
[winetricks](http://wiki.winehq.org/winetricks) ... instalace ruznych Windows programu pod WINE  
[instalace .NET](https://appdb.winehq.org/objectManager.php?sClass=version&iId=25478)  
export WINEARCH=win32 ... nastavi Wine na 32-bitovou verzi  
export WINEPREFIX=/home/tomas/.wine-teams/ ... zmena korenoveho adresare pro wine  
wineboot -u ... updatne prefix do aktualni konfigurace wine  
wineboot ... provedeni restartu, zastaveni a jinych operaci WIne prostredi  
winecfg ... graficka konfigurace Wine  
wineconsole ... otevre dosove okno  
wine uninstaller ... odinstalace nainstalovanych programu  
wine aaa.exe ... spusti program aaa.exe ve wine  
playconsole ... graficky interface pro wine  

### Android - Anbox

[Instalace Anboxu](https://docs.anbox.io/userguide/install_kernel_modules.html)
