# index

I have decided to keep this section in English as I can see overlapping of the topics over the borders. It makes the information more useful.

## Secure workstation

### 31.05.2023

There is used to be lot of sensitive data stored on the computers (laptops, desktop, servers). It may consist pictures, texts, code, data, but one very sensitive type of data is identity (access to multiple cloud services), history, filled forms, passwords, sessions. To obtain the sensitive data, it is enough to have read access over the files, so for example root/admin access to the computer. How can it happen?
1. steal device - boot from custom boot image as superadmin and access data
2. steal disk - put into own device with superuser and access data
3. logging to the system as a different user - when data is not protected by user account (access rights, ownership)
4. stealing the superuser, or target account
5. some system vulnerability - stealing in the memory, on the way (network) etc.

For system vulnerability, it is important to have system well maintained and configured (limited functionality just to necessary options, password policies etc.)

Stealing account threatens by leaking the password, session, key etc. It is ususally the human error and we must trust the persons they protect their data.

Access configuration on the server - it is partially in the scope of administrator and the user. Always think about access rights of the files and their location on the server (for example not keep it on unprotected places like temporary directories, unprotected removable devices etc.

Steal device and steal disk - for both cases the data encryption is very important to avoid leak of sensitive data. Very important is to have encrypted user profile. In some systems it requires encrypted operating system disk. Here we need to be careful. The encrypted key can be a file on the computer and it can be stolen. Or the encryption key can be a chip on the mainboard and bios can be unprotected and allow insert another boot media or be reset to factory configuration. This is not case of manually entered key (passphrase). But it should be long and hard enough, because the compute force allows to get it bruteforce in shorten time nowadays. When the computer shared by multiple people, all need to know the passphrase and this is not comfortable.

Another alternative is  to have encrypted just disk (filesystem, logical volume), which contains home data. But this requires oftentime to enter the passphrase during boot time, or have extra account, where we unlock the disk.

Best thing is bind the account password with disk encryption password and enter is just once during login. There is quite new tool on linux - systemd-homed, which is a service maintaining such functionality and making security and login comfort on very nice level.

## =Huion 420 tablet

### 22.06.2020

I received an idea to test a pen together with the computer. Huion 420 was looking as a great option for
the start. For first I wanted an ekonomic model for the play, for second I got an recomendation from a
person, who let an online course I had attended and for the last, I have seen a really nice video on
Youtube of a cartoon designer, who evaluated it as valuable stuff. I have seen that it supports Linux,
so the decission was done.
After a little struggle with installation on Ubuntu, I finally realized, that the pen requires AAA batery and
that is only problem blocking the usage ! OK, than, and what was the procedure to make it working?
Inspired by [http://www.magicbluesmoke.org/getting-a-huion-hs610-working-in-linux/](http://www.magicbluesmoke.org/getting-a-huion-hs610-working-in-linux/) and [https://codeyarns.github.io/tech/2015-05-11-how-to-use-huion-420-with-ubuntu.html](https://codeyarns.github.io/tech/2015-05-11-how-to-use-huion-420-with-ubuntu.html), really easy:

su -
  mkdir ~/github.com
  cd ~/github.com
  git clone https://github.com/DIGImend/digimend-kernel-drivers
  cd digimend-kernel-drivers
  dpkg-buildpackage -b -uc  ## to find the missing packages, I need to install, to succeed with make
  make
  make install
  ## replug the device and ensure you have a good AAA batery in a pen
  apt install xournal ## to have a nice note pad for drawing
  apt install gimp ## ti have a good graphical editor

To list information about the device or configure:

lsusb
  xsetwacom --list devices
  xsetwacom --set "Wacom BambooFun 4x5 Pen stylus" PressureCurve 0 20 80 100

and enjoy!

## Onedrive synchronization issue on Linux

### 17.06.2020

Cloud drive is a good way to have backup of your files and have your files synchronized and on single place and in single state on all your devizeces. Microsoft provides the Windows and Mac synchronization tool, but for Linux, there are few projects, who tries keep the same tool working despite the updated of API and other configuration on MS side. I was so happy with the [opensource implementation](https://www.maketecheasier.com/sync-onedrive-linux/) of this, until I moved to a different profile (with loosing config files of the previous profile) and the new attempt to set the synchronization failed. Apparently API was changed, or just something didn't work. I don't feel strong to update the code, or I don't have enough time to do it, but I succeeded to make work arround and set the synchronization. Here is the error obtained:

''
OneDrive HTTP Server Response: 400
* Connection #0 to host login.microsoftonline.com left intact
OneDrive returned a 'HTTP 400 - Bad Request' - gracefully handling error
onedrive.OneDriveException@src/onedrive.d(874): HTTP request returned status code 400 (Bad Request)
{
    "correlation_id": "ddb3d30a-6b81-4c1c-a135-f2d1a3e3ada4",
    "error": "invalid_grant",
    "error_codes": [
        9002313
    ],
    "error_description": "AADSTS9002313: Invalid request. Request is malformed or invalid.\r\nTrace ID: 4ed5f10e-1d1f-416a-bd1a-d4053ebf7101\r\nCorrelation ID: ddb3d30a-6b81-4c1c-a135-f2d1a3e3ada4\r\nTimestamp: 2020-06-17 07:10:33Z",
    "error_uri": "https:\/\/login.microsoftonline.com\/error?code=9002313",
    "timestamp": "2020-06-17 07:10:33Z",
    "trace_id": "4ed5f10e-1d1f-416a-bd1a-d4053ebf7101"
}
----------------
??:? [0x55da54c769d9]
??:? [0x55da54c75cb5]
??:? [0x55da54c76b65]
??:? [0x55da54c74f58]
??:? [0x55da54c748c5]
??:? [0x55da54c827a8]
??:? void rt.dmain2._d_run_main2(char[][], ulong, extern (C) int function(char[][])*).runAll() [0x7f269aaf49db]
??:? _d_run_main2 [0x7f269aaf47ee]
??:? _d_run_main [0x7f269aaf465d]
??:? __libc_start_main [0x7f269a6e00b2]
??:? [0x55da54c4d5ed]
''

The recipe how to overcome the error is:
1) You are asked to authenticate the client in a browser, by going into the URL:
https:*login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=22c49a0d-d21c-4792-aed1-8f163c982546&scope=Files.ReadWrite%20Files.ReadWrite.all%20Sites.ReadWrite.All%20offline_access&response_type=code&redirect_uri=https:*login.microsoftonline.com/common/oauth2/nativeclient

2) you authenticate and autorize the client

3) you obtain an URL

4) you set the URL into the variable URL, for example :

```
URL='https://login.microsoftonline.com/common/oauth2/nativeclient?code=DUMMY_CODE&session_state=DUMMY_STATE'
```

5) you run these commands:

```
CODE=$(echo $URL  | sed -e 's/.*code=//' -e 's/&.*//')
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "client_id=22c49a0d-d21c-4792-aed1-8f163c982546&code=$CODE&grant_type=authorization_code&redirect_uri=https://login.microsoftonline.com/common/oauth2/nativeclient" https://login.microsoftonline.com/common/oauth2/v2.0/token | jq .refresh_token |  sed -e 's/"//g' > ~/.config/onedrive/refresh_token
```

so in other words, you obtain the refresh token manually and store it into the config file.

## Zamyšlení nad zabezpečením domácí sítě a ochranou děti

### 04.05.2020

Jak nastavit domácí prostředí elektronických zařízení tak, aby poskytovalo bezpečí a zároveň vše, co od ní očekáváme? Zábavu, vzdělání, spojení s přáteli, rodinou, se všemi co potřebujeme, zdroj inspirace, zpráv atd? Předně je asi důležité si uvědomit, která nebezpečenství na nás mohou číhat, se kterými se dá bojovat a jak moc obtížné je vyrušit které z nich. Asi bych to rozdělil na nebezpečí, které se skládá z
* nebezpečného obsahu (hlásání a šíření násilí, pohrdání jinými lidmi, sexuálně nevhodný obsah, vyzývání k nebezpečnému chování, nemorálních, čí podvodných stránek, které chtějí vylákat peníze, či jinak zneužít návštěvníky atd.) na celých webech, nebo jen na určitých stránkách, článcích
* ochrana dětí před zveřejňováním citlivých a osobních údajů o sobě či jiných osobách
* ochrana dětí před cílenou komunikaci vůči nim, ať již s cílem dítě zneužít (například ke svému finančnímu prospěchu), či mu ublížit (například ponížit, vyděsit atd.)
* Ochrana před nezákným chováním (stahování, či šíření obsahu proti zákonu, či souhlasu majitele obsahu, či poškozujícího někoho)
* ochrana před závislostí a utápěním času v jednostranné aktivitě
Existují již produkty, které nás mají chránit a které se zaměřují na jedno či více nebezpečí. Jedním aspektem, nad kterým je dobré se zamyslet se, na která zařízení je mohu dostat, která zařízení mohu jimi zabezpečit, která nebezpečí budou pokrývat, co znamená jejich údržba a jak to bude omezovat ostatní členy domácnosti, či funkčnost jiných služeb. Například pokud zabezpečím dítěti jedno zařízeni, třeba telefon, ale neomezím jiné zařízení, například počítač, tak se opatření nestává účinné. Dále, pokud zabezpečím počítač a omezuje to práci jiného člena, tak se takové opatření nejspíše brzy zruší.

**Rozdělení ochrany pro různé členy domácnosti:** Je jedno z předních očekávání, že budeme chtít regulovat zabezpečení dle osob domácnosti. 4-leté dítě bude potřebovat jiné zabezpečení, než 12-leté dítě a jiné než dospělý. Proto bude nejdůležitější rozdělit přístupy na jednotlivá zařízení, tedy zařízení chránit účty. To nás samozřejmě chrání před únikem a zneužitím informací v případě ztráty, či krádeže zařízení, nebo v případě náhodného zvědavého zkoumání zařízením někým jiným. Doporučil bych hlavně rozšířit porozumění všech členu o důležitosti a důvodu ochrany a o nakládání s účty (nepůjčovat přístupy, nesdílet hesla, jen například rodičům, nepoužívat slabá hesla, uvědomit si, že jednání je vystopovatelné). Pokud se některá zařízení nedají rozdělit na účty, je dané zařízení sdílené a je třeba si to uvědomit.

**Ochrana před nebezpečným obsahem - celé weby:** Toto je jednodušší téma, celé weby. Víme, že některé weby se zaměřují na obsah, ze kterého máme obavy, které mají svým charakterem obsah nevhodný. Ochrana před takovým obsahem je jistě jednodušší a dá se zabezpečit vícero způsoby: jmenným překladem - služba převádějící jména webů na číselné adresy a blokováním přístupu (datového toku) na tyto weby. Pokud všechny zařízení používají pouze domácí síť, lze to nastavit centrálně, tedy na domácím routeru, pokud ne, musí se to nastavit na všech zařízeních, které mají přístup do veřejné sítě, například na mobilní síť. Služba na blokování nevhodného obsahu na úrovni jmenného překladu je například **[OpenDNS](https://www.opendns.com/setupguide/#familyshield)**, která zadarmo přináší prví znesnadnění přístupu na tyto nevhodné weby. Samozřejmě ne vše je ohodnoceno jako nevhodný web a každý může přispět ke změně nastavení, ale to znamená kontrolovat, k jakým webům děti přistupují, ale to už je jiná kapitola. Horší je to s blokováním fyzického přístupu přímo na servery. Servery často hostují více webů, tedy pokud zná člověk přímo IP adresu nebezpečného webu, tak pomocí firewallu lze zakázat přístup na tuto adresu, avšak zakážeme i ostatní weby tím serverem hostované, tedy nelze doporučit blokování konkrétních poskytovatelů blokováním síťového toku na jednotlivé servery, lze doporučit proxy službu a blokovat veškerý tok, který přes ni nejde.

**Ochrana před nebezpečným obsahem - jednotlivé stránky** - Považuji toto téma o rozšíření předchozího odstavce o větší ochranu. Předchozí ochrana je totiž na síťové vrstvě, konkrétně na principu, že nevhodné jména serverů se přeloží na IP adresu poskytovatele bezpečí a upozorní na fakt, že se jedná o nebezpečný web. Síťová vrstva nevidí totiž do obsahu aplikačního dotazu na zobrazení konkrétní stránky. Pokud chceme do ní vidět, je třeba povolit pouze proxy službu, přes kterou půjdou všechny dotazy a na ní stanovit pravidla, například blokovat vše, co má v adrese řetězec, který se považuje za nebezpečný, například 'ublizit'. Proxy serveru, popřípadě proxy serverů s důrazem na nevhodný obsah je více, např. **squid, SquidGuard, PfSense, DansGuardian atd.** Seznamy pravidel (zakázaných slov, řetězců) se budou lišit, budou pokrývat různé jazyky a budou na straně dotazů, ne odpovědí stránek. Složitější nástroje na ochranu zde mohou přinést právě velkou hodnotu a blokovat více inteligentně, popřípadě i využívat odpovědi stránek k blokaci, či učení. Nemálo důležitý prvek je i fakt, že proxy server přináší i možnost ukládání historie, proto je možné předchozí obsah procházet a pozměnit pravidla, či provést domluvu, či osvětu.

To by pro dnešek mohlo stačit.

## Code Retreat

### 09.12.2019

Very interesting experience was the presence on Code retreat workshop. The objective was to have several (5) iterations over the same topic: [https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life). The common rule was work 45 in pair (random, each time different pair) on implementation of 0-player game, the the rule was to work in the mode for Test Driven Development (first unit tests, than the cone). We could choose any programming language, we had to delete the code after each iteration and we had 15 minutes after each iteration for retrospective. First iteration was just simple "do it" task, second with the limitation that each function must have just 3 lines and no if statements, next iteration without letter 3, +, u, q, h, next iteration one person doing tests, other the alghoritm, but no words, last one was splitted to 5 minutes iteration for one than other person in the pair. If the code not working, than delete the last iteration code. Really fun, really interesting to learn new approaches, how other person works, to learn new people and break the ice. Definetly great to test TDD on the simple task.

## Ubuntu 18.04.2

### 28.3.2019

New release of Ubuntu 18.04 LTS appeared. Most important is hardware support. For instance my laptop started to face network connectivity issue and new firmware downloaded by OS update wasn't supported by kernel. This is solved by 18.04.2 because it comes with up to date kernel.

More info: [https://www.omgubuntu.co.uk/2019/02/ubuntu-18-04-2-lts-released](https://www.omgubuntu.co.uk/2019/02/ubuntu-18-04-2-lts-released)

Update procedure (18.04 to 18.04.2) :  
`sudo apt-get install --install-recommends linux-generic-hwe-18.04 xserver-xorg-hwe-18.04`
