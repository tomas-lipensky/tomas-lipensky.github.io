Bit , vyjadreni , popis

8 , 0x0101 ... break disabled
6 , 0x0040 ... ignoruje data v NV RAM
7 , 0x0080 OEM bit
10 , 0x0400 ... IP broadcast se samyma nulama
5,11,12 , 0x0800-0x1000 ... rychlost konzoly
13 , 0x2000 Nabootuje z ROM, pokud image selze
14 , 0x4000 IP broadcast nema cisla site
15 , 0x8000 Diagnosticke zpravy, ignoruje NVRAM

0-3:
00 ... rommon> prompt, b prikazy (confreg 0x2142, reset)
01 ... nabootuje IOS z ROM
0x...2-F ... router pouzije boot prikazy z NVRAM
