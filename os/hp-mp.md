# MP - Management Processor

Defaultni uzivatel: Admin/Admin

### zakladni MP&gt; mod

co ... COnsole interface - konzole serveru, nebo nParu  
vtp ... Virtual Front Interface - monitoring stavu systemu  
cm ... Command Menu - prikazova radka MP  
cl ... Console Log viewer - prohlizeni logu konzoli  
sl ... Show event Log viewer - Prohlizeni stavu hardwaru  
fw ... FirmWare update  
he ... HElp - napoveda  
x ... eXit  

### CO - konzole

|B ... navrat do MP menu  
|E cf ... aktivace klavesnice, pokud je vice uzivatelu v konzoli  
vparstatus -w ... cislo aktualniho vParu  
|A ... prepnuti do dalsiho vParu  
/opt/hpvm/bin/hvpmconsole -p myguest ... VM MP - Virtual Machine Management Processor - prepinani mezi VM  

====VFP - predni panel  
|b (nebo q) ... navrat do MP menu  

### CL - Console log

|b (nebo q) ... navrat do MP menu  
? ... napoveda ovladani  

### SL - Show event log

|b (nebo q) ... navrat do MP menu  

### HE - Help

q ... navrat do MP menu  

### CM - Command Menu

|b (nebo ma) ... navrat do MP menu  
sysrev ... ukaze vsechny firmware  
he ... help - napoveda k prikazum  
ls ... lan status - ukaze sitove nastaveni MP  
lc ... lan console - meni sitove nastaveni  
dns ... konfigurace dns nastaveni  
so ... tvorba ssh/ssl klicu a nastaveni uzivatelske bezpecnosti (logout timer, ...)  
sa ... System access - nastavovani pristupu k MP (telnet, https, ...)  
er ... na starsich MP - zapnout/vypnout vzdaleny modem  
el ... na starsich MP - zapnout/vypnout telnet  
ew ... na starsich MP - zapnout/vypnout https  
uc ... user configuration - nastaveni uzivatelu  
who ... ukaze, kdo je zdovna pripojeny do MP  
te ... tell - napsat zpravu vsem pripojenym uzivatelum  
xd ... restart MP (po zmene sitoveho nastaveni)  
dc ... default configuration - tovarni nastaveni  
di ... disconnect - odpoji vsechny uzivatele  
rs ... reset serveru  
tc ... (Transfer of Control) Crash dump + reset  
pe ... power entity - haltovani jednotlivych nParu  
pc ... power control - zapinani/vypinani serveru  
ps ... power status - informace o chodu serveru a nParu
