## Weby

[robodoupe.cz](http://robodoupe.cz) ... Web o robotice a elektronice  

### Chytrá domácnost

[https://iot.tuya.com/](https://iot.tuya.com/) ... Tuya  
[https://www.reddit.com/r/smartlife/comments/gj5ixd/smart_life_web_interface/](https://www.reddit.com/r/smartlife/comments/gj5ixd/smart_life_web_interface/) ... Python skript pro Tuyapy  
### Elektro soucastky

[Barevne oznaceni rezistoru (odporu)](http://nearbus.net/wiki/index.php?title=File:Resistor_color_codes.jpg)

##### Ridici jednotky/mikropocitace

Raspberry Pi  
Arduino  
AVR Atmel atmegaXXX  

##### elektro zarizeni

[vlhkostat](http://www.elektrobock.cz/cs/cidlo-vlhkosti/product.html?id=68) na elektrobock.cz  
[EShop snalshop](http://www.snailshop.cz/)  
[ges]()  
[GM electronic](https://www.gme.cz)  

##### I2C

[I2C](http://cs.wikipedia.org/wiki/I%C2%B2C) na cz.wikipedia.org  
[I2C teplotni citlo](http://www.amaterskaelektronika.cz/file/teplota-vlhkost-sht11-assembler) na amaterskaelektronika.cz  

##### 433

[Lekce jak na 433](http://arduino8.webnode.cz/news/lekce-20-arduino-a-vyuziti-433-92-mhz/)  
[nakup 433](http://arduino-shop.cz/arduino/1003-arduino-433mhz-vysilac-prijimac-1427821401.html)
[jiny nakup 433](http://robotstore.cz/obchod/arduino/433mhz-vysilac-a-prijimac-sada-arduino-modulu/)  

##### ATMega:

[gotronik.pl](http://www.gotronik.pl/zestawyuruchomieniowe/mod_avr_atmega16v1.html)

## Raspberry Pi

[Popis extension slotu Raspberry Pi A i B +, GPIO specifikace](http://elinux.org/RPi_Low-level_peripherals)  
[Ovladani GPIO z shellu Linuxu](http://luketopia.net/2013/07/28/raspberry-pi-gpio-via-the-shell/)  
[piGPIO](https://www.npmjs.com/package/pigpio) - Knihovna pro nodeJs na ovladani GPIO  
[Raspbian a Node-Red](https://nodered.org/docs/hardware/raspberrypi) - navod na instsalaci Node-Red na Raspbianu  
[GPIOd](https://www.npmjs.com/package/node-red-node-pi-gpiod) - ovladani GPIO sbernice na Raspberry na [Node-RED](../dev/node-red.html). V pripade "nrgpio python command not working" je problem nejspise s pravy k pinum, zkusit pod rootem.  
[Kodi](https://www.raspberrypi.org/documentation/usage/kodi/) ... multimedialni cetrum pro Raspberry Pi  
[Yatse](https://play.google.com/store/apps/details?id=org.leetzone.android.yatsewidgetfree&hl=en_US) ... Dalkovy ovladac pro Kodi na Androidu  

##### Priklady

[Zapojeni diody na linuxsoft.cz](http://www.linuxsoft.cz/article.php?id_article=1953)  
[Jednoduche zapojeni diody a cidla pohybu](http://www.raspi.cz/2012/06/prvni-experimenty-gpio-svitime-led-diodou-detekujeme-pohyb/)  
[Ovladani GPIO z shellu (Raspbian Wheezy)](https://sites.google.com/site/semilleroadt/raspberry-pi-tutorials/gpio)  
[Zapojeni prepinacu](https://www.linuxexpres.cz/hardware/raspberry-pi-vstup-vystup-gpio)
[Zapojeni Rele](https://www.linuxexpres.cz/hardware/inteligentni-domacnost-s-raspberry-pi-3?highlightWords=Raspberry)  

##### Prikazy Raspbian Wheezy

echo 11 > /sys/class/gpio/export  ... aktivuje GPIO port 11 (vytvori soubor /sys/class/gpio/gpio11)  
echo out > /sys/class/gpio/gpio11/direction ... Aktuvuje na GPIO portu 11 rezim In/Out  
cat /sys/class/gpio/gpio11/value ... ukaze hodnotu GPIO portu  
echo 0 > /sys/class/gpio/gpio11/value ... vypne port 11  
echo 11 > /sys/class/gpio/unexport ... deaktivuje port 11
