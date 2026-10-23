# Integrity

<a name="boot|]]
### Integrity boot

<h6>Boot proces na Integrity</h6>
<li>POST ... Power-On Self Test - Test ulozeny v BootROM</li>
<li>PAL ... Processor Abstraction Layer</li>
<li>SAL ... System Abstraction Layer</li>
<li>EFI boot manager/shell ... Spoustec firmware ukozeny v BootROM, ktery nacita informace o cestach k diskum z NVRAM  
<li>EFI oddil ... Spoustec systemu, ulozeny v EFI systemovem oddilu - bootovaci oblasti bootovaciho disku. Ten nacte soubor auto, ktery ukazuje na defaultni jadro a defaultni parametry</li>
<li>/stand/vmunix ... jadro</li>
<li>init ... init proces s nadefinovanymi init levely a odpovidajicimi procesy</li>

<h6>Struktura boot disku na Integrity - struktura na vsech Xeon serverech stejna</h6>
<li>MBR ... Master Boot Sector</li>
<li>GPT Partition Table ... tabulka Globaly Unique IDentifier - GUID - ukazaele na vsechny EFI oddily</li>
<li>System Partition ... 1. EFI oddil, obsahuje nahravac kernelu a OS auto soubor: \efi\hpux\hpux.efi, \efi\hpux\auto, \efi\hp\tools\network\ping.efi, ...</li>
<li>OS Partition ... 2. EFI oddil, absahuje LVM, nebo FS. LVM obsahuje PVRA, VGRA, BDRA, BBRA</li>
<li>Service partition ... 3. oddil - HPSV - HP Service partition, FAT32 oddil, obsahujici diagnosticke a jine nastroje</li>
<li>GPT Partition Table ... </li>

<h6>[Manualni boot proces](http://www.intel/com/software/products/college/efishell/images/efi_shell_cmnd_1_1.pdf) - preruseni EFI stiskem klavesy Esc</h6>
[Seznam prikazu v EFI shellu](http://docstore.mik.ua/manuals/hp-ux/en/5991-1247B/ch04s13.html#aes-npar-287a)  
help ... napoveda  
devices ... vylistuje vsechny bootovaci zarizeni  
acpiconfig ... ukaze ACPI konfiguraci  
bcfg ... nastaveni bootovaciho menu  
map ... ukaze vsachna bootovaci zarizeni  
fs2: ... vyber zarizeni fs, EFI oddoil 2, a vstup do nej  
hpux ... odstartuje hpux.efi startovaci manazer  
info ... ukaze informace o systemu  
lanaddress ... Ukaze IP  
lanboot ... nastartuje system ze site z Ignite serveru  
exit ... navrat do EFI boot manazeru  
reset ... restartuje server  

<h6>ISL/IPL</h6>
showautofile ... ukaze obsah souboru auto (\efi\hpux\auto)  
setauto "boot vmunix" ... nastaveni \efi\hpux\auto  
boot vmunix ... nastartuje jadro, jak je nadefinovano v auto  
boot vmunix -is ... nastartuje do single-user modu  
boot vmunix -lq ... nastartuje bez LVM quora  
boot vmunix -lm ... nastartuje do LVM udrboveho modu  
boot vmunix -lm ... nastartuje do ladiciho udrzboveho modu  
boot vmunix.prev nproc=6000 ... nastartuje jadro v /stand/vmunix.prev s parametrem nproc=6000  
ll ... vylistuje seznam souboru v adresari /stand  
help -d ... napoveda  
exit ... navrat do EFI menu  
reset ... reboot nParu
