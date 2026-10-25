# lin-workstation

## Install Ubuntu on encrypted physical volume

lsblk ## list disks  
DEV=/dev/xxx ## select a proper disk device  
sgdisk --print $DEV ## list current partitions  
BOOTPAR=x;PVPAR=z;EFIPAR=u;GRUBFS=v  
sgdisk --new=$BOOTPAR:0:+512M --typecode=$BOOTPAR:8301 --change-name=$BOOTPAR:/boot $DEV ## partition for /boot  
#sgdisk -n $GRUBFS:0:+2M -t $GRUBFS:ef02 -c $GRUBFS:GRUB $DEV  
#sgdisk -n $EFIPAR:0:+128M -t $EFIPAR:ef00 -c $EFIPAR:EFI-SP $DEV  
sgdisk -n $PVPAR:0:0 -t $PVPAR:8301 -c $PVPAR:rootfs  $DEV ## partition for /  
sgdisk -p $DEV  
cryptsetup luksFormat --type=luks1 ${DEV}$BOOTPAR  
cryptsetup luksFormat --type=luks1 ${DEV}$PVPAR  
cryptsetup open ${DEV}$BOOTPAR LUKS_BOOT  
cryptsetup open ${DEV}$PVPAR rootfs_crypt  
mkfs.ext4 -L boot /dev/mapper/LUKS_BOOT  
pvcreate /dev/mapper/rootfs_crypt  
vgcreate ubuntu-vg /dev/mapper/rootfs_crypt  
lvcreate -L 4G -n swap ubuntu-vg  
lvcreate -l 80%FREE -n root ubuntu-vg  
while [ ! -d /target/etc/default/grub.d ]; do sleep 1; done; echo "GRUB_ENABLE_CRYPTODISK=y" > /target/etc/default/grub.d/local.cfg  
INSTALL  
mount /dev/mapper/ubuntu--vg-root /target  
for n in proc sys dev etc/resolv.conf; do mount --rbind /$n /target/$n; done  
chroot /target  
mount -a  
apt install -y cryptsetup-initramfs  
echo "KEYFILE_PATTERN=/etc/luks/*.keyfile" >> /etc/cryptsetup-initramfs/conf-hook  
echo "UMASK=0077" >> /etc/initramfs-tools/initramfs.conf  
mkdir /etc/luks  
dd if=/dev/urandom of=/etc/luks/boot_os.keyfile bs=512 count=1  
chmod 500 /etc/luks  
chmod 400 /etc/luks/boot_os.keyfile  
cryptsetup luksAddKey ${DEV}$BOOTPAR /etc/luks/boot_os.keyfile  
cryptsetup luksAddKey ${DEV}$PVPAR /etc/luks/boot_os.keyfile  
echo "LUKS_BOOT UUID=$(blkid -s UUID -o value ${DEV}$BOOTPAR) /etc/luks/boot_os.keyfile luks,discard" >> /etc/crypttab  
echo "rootfs_crypt UUID=$(blkid -s UUID -o value ${DEV}$PVPAR) /etc/luks/boot_os.keyfile luks,discard" >> /etc/crypttab  
update-initramfs -u -k all  

## Nástroje

`add-apt-repository ppa:unit193/encryption`  
`apt install veracrypt keepassx`  

## Teams for Linux

====MS Code====

```bash
sudo add-apt-repository -y "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EB3E94ADBE1229CF
sudo apt update
sudo apt -y install code
```

====Skype4Business====

```
sudo apt-get install pidgin pidgin-sipe
```

[https://blog.programster.org/ubuntu-16-04-configure-pidgin-for-skype-for-business-lync](https://blog.programster.org/ubuntu-16-04-configure-pidgin-for-skype-for-business-lync)

Conferece attenance: [https://askubuntu.com/questions/296875/lync-attendee-meetings-on-ubuntu](https://askubuntu.com/questions/296875/lync-attendee-meetings-on-ubuntu)

## MS Office 365 Online

#### Chrome:

[https://askubuntu.com/questions/941330/how-can-i-install-office-365-and-avg-without-using-virtual-machine-on-linux-ubun](https://askubuntu.com/questions/941330/how-can-i-install-office-365-and-avg-without-using-virtual-machine-on-linux-ubun)

==Evolution:==

```
sudo apt-get install evolution-ews
```

Configure the online account for "Microsoft Exchange" like described on URL:
[https://www.maketecheasier.com/access-microsoft-exchange-linux/](https://www.maketecheasier.com/access-microsoft-exchange-linux/)

Another usefull resource:
[https://www.eduhk.hk/ocio/content/faq-configure-evolution-access-office-365](https://www.eduhk.hk/ocio/content/faq-configure-evolution-access-office-365)

After implementing the configuration, close Evolution, go to the command line and kill all evolution processes.

## OneNote

[https://pages.corifeus.com/github/onenote](https://pages.corifeus.com/github/onenote)

====Teams====

```bash
cd /opt
git clone https://github.com/IsmaelMartinez/teams-for-linux
cd teams-for-linux
dist/linux-unpacked/teams-for-linux
```

```
wget https://statics.teams.microsoft.com/hashedassets/favicon/prod/favicon-9f45b466.ico -o /opt/teams-for-linux/teams.ico
echo "[Desktop Entry]
Version=1.0
Terminal=false
Type=Application
Name=Teams
Exec=/opt/teams-for-linux/dist/linux-unpacked/teams-for-linux
Icon=/opt/teams-for-linux/teams.ico" > ~/.local/share/applications/teams-for-linux.desktop
```

====PowerShell====

```bash
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install -y powershell
pwsh
```

## AZCLI

[https://docs.microsoft.com/cs-cz/cli/azure/install-azure-cli-apt?view=azure-cli-latest](https://docs.microsoft.com/cs-cz/cli/azure/install-azure-cli-apt?view=azure-cli-latest)

====Winexe====

```bash
wget http://download.opensuse.org/repositories/home:/uibmz:/devel:/experimental/Debian_9.0/amd64/winexe_4.8.0.0-15_amd64.deb
apt install ./winexe_4.8.0.0-15_amd64.deb
mkdir -p /usr/local/samba/var/cache
winexe -U prgorilocal/USER%HESLO //SERVER PRIKAZ
```
