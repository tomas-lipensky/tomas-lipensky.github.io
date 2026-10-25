# PA-RISC

### PA-RISC boot

**Boot proces na PA-RISC**
    
- POST ... Power-On Self Test - Test ulozeny v BootROM
- PDC ... Processor Dependent Code - Test ulozeny v BootROM
- IODC ... I/O Dependent Code - Test ulozeny v BootROM
- PDC/BCD ... Boot Console Header - Spoustec firmware ukozeny v BootROM, ktery nacita informace o cestach k diskum z NVRAM
- ISL/IPL ... Initial System/Program Loader - Spoustec systemu, ulozeny v LIF (Logical Interchange Format) oblasti bootovaciho disku. Ten nacte soubor AUTO, ktery ukazuje na defaultni jadro a defaultni parametry
- /stand/vmunix ... jadro
- init ... init proces s nadefinovanymi init levely a odpovidajicimi procesy

**Struktura boot disku na PA-RISC**

- LIF Header
- PVRA ... Physical Volume Reserved Area - Informace o PV
- BDRA ... Boot Data Reserved Area - Ukazatele na /stand, swap a /
- LIF Area ... Obsahuje obsahuje ISP/IPL, AUTO a jine nastroje potrebne na lokalizaci jadra a jeho spusteni
- VGRA ... Volume Group Reserved Area - informace o strukture VG
- LVs ... Logicke oddily
- volne misto
- BBRA ... Bad Blocks Reserved Area - misto na ukadani dat misto poskozenych sektoru na disku

Boot disky bez LVM maji misto VGRA, LVs a volneho mista heden HSF oddil a na konci disku misto pro swap  

**Manualni boot proces - preruseni BCH stiskem klavesy Esc**
help ... napoveda  
in all ... ukaze informace o systemu  
search ... vylistuje vsechny bootovaci zarizeni  
search ipl ... vylistuje vsechny bootovaci zarizeni obsahujici IPL  
path ... ukaze, ktere cesty jsou nastavene jako pri, haa, alt  
path pri x/x.x.x ... nastavi cestu x/x.x.x jako primarni (1.) cestu v NVRAM  
path haa x/x.x.x ... nastavi cestu x/x.x.x jako HA alternativni (2.) cestu v NVRAM  
path alt x/x.x.x ... nastavi cestu x/x.x.x jako alternativni (3.) cestu v NVRAM  
boot pri ... nastartuje system z disku v primarni ceste  
boot haa ... nastartuje system z disku v HA alternativni ceste  
boot alt ... nastartuje system z disku v alternativni ceste  
boot x/x.x.x ... nastartuje system z disku v zadane ceste  
boot lan.x.x.x.x install ... nastartuje system ze site z Ignite serveru na IP adrese x.x.x.x  
auto ... ukaze parametry autobootu  
info ... ukaze informace o serveru?  
lan_addr ... Ukaze IP  
date ... datum a cas  
reset ... restartuje server  

**ISL/IPL**
hpux ... nastartuje jadro, jak je nadefinovano v HP-UX  
hpux ls ... vylistuje seznam souboru v adresari /stand  
hpux show autofile ... ukaze obsah souboru AUTO  
hpux -is ... nastartuje do single-user modu  
hpux -lq ... nastartuje bez LVM quora  
hpux -lm ... nastartuje do LVM udrboveho modu  
hpux /stand/vmunix.prev nproc=6000 ... nastartuje jadro v /stand/vmunix.prev s parametrem nproc=6000
