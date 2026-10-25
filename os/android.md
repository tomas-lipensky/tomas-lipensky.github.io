# android

## Externi Odkazy

[www.linuxreaders.com/category/android](http://www.linuxreaders.com/category/android)  

## IDE, utility, Propojeni Android a PC

[Android Studio](https://developer.android.com/studio/index.html)  
[Jak nastavit prostredi pro (na MobileFirst tuturialu)](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/7.1/setting-up-your-development-environment/setting-up-the-android-development-environment/)

## Odkazy na aplikace

[www.freewarelovers.com/android](http://www.freewarelovers.com/android)  
[market.android.com](http://market.android.com/)  

## Google sluzby

https://www.google.com/android/devicemanager ... Device manager najde telefon, zablokuje atd.  
https://www.google.com/landing/now ... chytra upozorneni podle casu, mista atd.  

## Oblibene aplikace

Barnacle Wifi Tether  
Advanced Task Killer  
APG  
DroidWall  
[STDroid](https://w3.tap.ibm.com/tap/app/2126)  
[Android WiFi LEAP Configuration Manager](https://w3.tap.ibm.com/tap/app/1689)  
airdroid ... pripojeni se k androidu z PC + nasledne ovladani  

## Prikazy v terminalu

netcfg ... seznam sitovych karet  

## Pripojeni LG GT540 k pocitaci - Linux

[Navod jak nainstalovat SDK a udelat testovaci aplikaci](http://www.if-not-true-then-false.com/2010/android-sdk-and-eclipse-adt-on-fedora-centos-red-hat-rhel/)  

- Stahnout: [Android SDK](http://developer.android.com/sdk/index.html) + [fastboot](http://developer.htc.com/adp.html)
- Na telefonu:
  - vypnout Nastaveni - SDKarta - "USB Mass Storage"
  - zapnout Nastaveni - Aplikace - Vyvoj - Ladeni USB
- Rozbalit android sdk treba do /usr/local/, spustin /usr/local/android-sdk*/tools/android a nainstalovat Android SDK tool - adb (v $SDK/platform-tools)
- rozbalit fastboot do /usr/local/android-sdk*/tools
- nastavit udev, aby mohli k zarizeni pristupovat i jini uzivatele nez root:

  ```sh
  echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="1004", ATTRS{idProduct}=="618e", MODE="0666"
  SUBSYSTEM=="usb", SYSFS{idVendor}=="1004", MODE="0666"' > /etc/udev/rules.d/51-android.rules
  ```

- pripojit LG pomoci USB
- otestovat pripojeni: lsusb; dmesg | tail -10

### [adb](http://android-dls.com/wiki/index.php?title=ADB) - Android Debug Bridge

adb devices ... seznam pripojenych zarizeni (musi mit zapnuto debug USB na telefonu)  
adb shell ... ziskam interaktivni shell z telefonu  
adb push ... prenese soubor na Android  
adb pull ... prenese soubor z androidu  
adb reboot  
adb shell  
adb [logcat](http://www.androidcentral.com/android-201-10-basic-terminal-commands-you-should-know) ... vypise ruzne logy Adnroidu  

### bosboot

Po nabootovani telefonu do fastbootu, specialniho rezimu, ktery umoznuje napriklad modifikaci bootsekvence, se pracuje v fastbootu pomoci prikazu [fastboot](http://android-jotting.blogspot.com/2010/11/how-to-use-fastboot-on-ubuntu.html). Rezim fastboot je umoznen jen v nekterych romkach  

## Vyvoj aplikaci pro Android v Android SDK

[Hello word.apk](http://blog.firszt.eu/index.php?post/2011/02/09/Hello-World%2C-my-first-android-application-in-3-staeps-%28CLI-only%29)  

## Struktura souboru

/sdcard/Android/data/ ... data aplikaci  
/sdcard/Android/data/com.google.apps.docs>files>pinned_docs_files_do_not_edit ... zrcadlene soubory Google drive  

## Prikazy

[https://github.com/jackpal/Android-Terminal-Emulator/wiki/Android-Shell-Command-Reference](https://github.com/jackpal/Android-Terminal-Emulator/wiki/Android-Shell-Command-Reference)
