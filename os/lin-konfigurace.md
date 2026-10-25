# lin-konfigurace

### Ubuntu

[Ubuntu](Ubuntu) - apt remove example-content #… odebere zbytecny balik - pisnicka a video

LVM sifrovane na urovni PV nebo [LV](https://petrnosek.cz/lvm-a-sifrovani-dat-na-hdd-pomoci-dm-crypt-luks/)? LV, protoze si muzeme vybrat, jake LV nesifrovat a ktere sifrovat. Lepe se prenasi mezi PV, bezpecnejsi, chranene proti prenosu na nechranene PV  

root LV - sifrovat ci nesifrovat? Sifrovat = chrani proti nabootovani z docasneho media a podstrceni uzivatele se sudo pravy, ktery pri behu rozsifrovaneho disku pristoupi na pocitac i proti jinym zmenam konfigurace  
### Pravidelne cisteni Snap balicku

snap list | grep disabled  
snap remove &&--revision=45 nazev_balicku  

### update balicku

Update muze zpusobit nefunkcnost, lepe provadet update kontrolovanou cestou (1x tydne/14 dni/mesic/pri problemech)  

### bezpecnost

### Historie, autid
