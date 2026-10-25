# LINUX - X Windows

### Externi odkazy

[Popis xserver architektury](http://en.wikipedia.org/wiki/X_Window_System_protocols_and_architecture)  
[SysAdminGuide](https://wiki.gnome.org/SysAdminGuide) na wiki.gnome.org - navod na spravu GNOME  
[SysAdminGuideUpdate](https://wiki.gnome.org/SysAdminGuideUpdate) na wiki.gnome.org  

### X Windows

[startx, xinit](http://xwinman.org/basics.php)
startx -- :1 ... spusteni druheho Xwindows  
startx -- :2 ... spusteni tretiho Xwindows  
gimp --display :2 ... spusteni gimpu ve tretim Xwindows  
/etc/X11/xdm/Xsession ... globalni nastaveni manazeru oken  
~/.xinitrc ... uzivatelske nastaveni manazeru oken (spusteni manazeru: exec WM)  
xinit /usr/bin/ck-launch-session startlxde ... spusteni okenniho manazeru LXDE z prikazove radky s [ConsoleKit](http://www.freedesktop.org/wiki/Software/ConsoleKit) (s podporou HAL)  

##### Konfigurace, testy konfiguracni soubory

Xorg -configure ... nacte vsechny ovladace, detekuje hardware a zapise to do xorg.conf  
xorgcfg -textmode ... nastaveni X-ek v textovem rezimu  
xorgconfig, x86config ... nastaveni X-ek  
X -probeonly ... spusti X-ka jen pro otestovani nastaveni  
ddcprobe ... kontrola, zda kudzu spravne detekoval vlastnosti monitoru a karty  
xev ... otestovani a vypsani udalosti (X event) - vstupnich zarizeni, zobrazi cislo zmacknute klavesy atd.  
[~/.Xdefaults](https://wiki.archlinux.org/index.php/Xdefaults) ... nastaveni pro jednotlive aplikace  
~/.xinitrc ... nastaveni spousteni xek  
[~/.dmrc](etc-dmrc) ... nastaveni defaultniho spravce oken, jazyka, klavesnice  
[/etc/X11/xorg.conf](etc-xorg-conf) ... nastaveni hardwaru (graficke karty, monitoru, klavenice, mysi) pro Xka  
synclient [TouchpadOff](http://www.x.org/archive/X11R7.5/doc/man/man4/synaptics.4.html)=1 ... zakaze pouzivani touchpadu za chodu prepinac TouchpadOff v xorg.conf) a jine nastaveni touchpadu od Synapticsu  
xinput --disable 15 ... zakaze power tlacitko  
xinput set-prop 12 'Device Enabled' 0 ... zakaze vstupni zarizeni cislo 12  
xinput --list ... seznam vsech [xinput](http://en.wikipedia.org/wiki/DirectInput) zarizeni  
xinput set-button-map $(xinput --list | grep TouchPad | cut -c55-56) 1 2 3 5 4 7 6 ... zmeni smer skrolovani u TouchPad zarizeni  
xrandr --current ... aktualni konfigurace monitoru  
xrandr --output VGA --mode 1024x768 ... nastavi mod pro monitor VGA  
xrandr --output LVDS-0 --rotate left ... otoci monito LVDS-0 doleva  
xrandr --output VGA --right-of LVDS ... nastavi, z monitor VGA bude napravo od LVDS  
xrandr --output LVDS-0 --set BACKLIGHT 15 ... nastavi podsviceni monitoru  
xrandr --prop ... ukaze nastaveni monitoru  

### Spravci prihlaseni, spousteni X-ek

system-switch-displaymanager ... vyber spravce prihlaseni  
/etc/X11/prefdm ... konfiguracni soubor pro start spravce prihlaseni  

##### [GDM](http://library.gnome.org/admin/gdm/stable/) - Gnome Desktop Manager

[/etc/gdm/custom.conf](http://library.gnome.org/admin/gdm/stable/configuration.html.en)  
/usr/share/xsessions/*.desktop  ... definice spravcu oken  

##### [KDM](http://muzso.hu/2007/05/05/kdm-greeter-customized-session-list-and-default-session)  

##### XDM

/etc/X11/xdm/Xsession ... vychozi konfigurace spoustece manazeru oken  
~/.xsession ... uzivatelska konfigurace spoustece manazeru oken  

##### CDM

~/.Xdefaults : *wmStartupCommand: /usr/X11R6/bin/fvwm ... Vybere manazer oken pro uzivatele
~/.Xdefaults : *waitWmTimeout: 2

##### LXDM

## Okenni manazery (Window managers)

* [GNOME (gnome-session)](#gnome)
* KDE (startkde)
* XFCE4 (startxfce4)
* Blackbox (blackbox)
* FVWM (fvwm, fvwm2)
* Window Maker (wmaker)
* IceWM (icewm)
* [LXDE](#lxde)
* [Cinnamon](#connamon)

### GNOME

[GNOME](http://library.gnome.org) ... stranky projektu

[Spousteni gnome](http://www.yolinux.com/TUTORIALS/GNOME.html)  
gconftool-2 --dump / |grep "<key>" | cut -d'>' -f2 | cut -d'<' -f1 | less ... vypis vsech klicu nastaveni gnome  
gconftool-2 --dump / > gnome.xml ... vypis aktualniho nastaveni gnome  
gconftool-2 --direct --config-source xml:readwrite:/etc/gconf/gconf.xml.defaults --type bool --set /schemas/apps/gnome-session/options/logout_prompt false ... nastaveni defaultni hodnoty - nepta se pri odhlasovani  
gconftool-2 --direct --config-source xml:readwrite:/etc/gconf/gconf.xml.mandatory --type string --set /system/http_proxy/host wwwproxy.xyz.com ... nastavi proxy, ktarou uzivatel nemuze zmenit  
gconftool-2 --direct --config-source xml:readwrite:/etc/gconf/gconf.xml.defaults --type int --set /apps/metacity/general/num_workspaces integer ... nastavi pocet ploch  
gconftool-2 --direct --config-source xml:readwrite:/etc/gconf/gconf.xml.mandatory --type string --set /apps/metacity/global_keybindings/panel_run_dialog '<Alt>F3' ... nastaveni klavesovych zkratek  
gconftool-2 --direct --config-source user-configuration-source --recursive-unset ... reset uzivatelskych hodnot na defaultni  
gsettings set org.gnome.shell.extensions.dash-to-dock show-show-apps-button false ... vypne Activites menu v Gnome2 horni liste  
gsettings set org.gnome.settings-daemon.plugins.media-keys screenshot '[]' ... odregistruje PrtScreen tlacitko od screenshotu  
/usr/lib/bonobo/servers/*.servers ... aplety  
/usr/share/themes/*/index.theme
~/.local/share/mime:/usr/local/share/mime:/usr/share/mime ... definice provazanosti koncovek souboru a protokolu s programy (MIME)  
update-mime-database ~/.local/share/mime ... update provedenych zmen  
gnomevfs-info soubor ... vypise informace o souboru a detekovany MIME typ  
gnome-session ... manazer seance - iniciuje gnome  
gnome-shell --version ... verze gnomu  
gnome-settings-daemon ... konfiguruje vzhled a parametry gnome  
gnome-panel ... panely  
Metacity ... window manager  
pkg-config --variable=privlibexecdir gnome-screensaver ... zjisti, kde sidli gnome-screensaver  
pkg-config --variable=themesdir gnome-screensaver ... zjisti, kde jsou ulozene sporice obrazovky  
Brasero + gstreamer-plugins-ugly ... vypaluje i MP3 na CP  

Shell extensions:
journalctl /usr/bin/gnome-shell ... logy shell rozsireni  
alt-F2 -> lg ... Looking glass  
[sound-output-device-chooser](https://extensions.gnome.org/extension/906/sound-output-device-chooser/)  
Clipboard Indicator  
Desktop Icons  
Draw On You Screen  
PulseAudio Loopback Device  
Remove App Menu  
Suspend  
system-monitor  
Ubuntu Dock  
Ubuntu AppIndicators  

### LXDE

pouziva Freedesktop.org standarty, konfigurace lze delat i pomovi xdg-utils  
[Spusteni LXDE](https://wiki.archlinux.org/index.php/LXDE_%28%C4%8Cesky%29) po startu  
[FAQ](http://wiki.lxde.org/en/LXDE:Questions) k LXDE - konfigurace ldxe.rc.xml atd  
[~/.config/openbox/lxde-rc.xml](http://en.gentoo-wiki.com/wiki/Openbox#Create_custom_keyboard_shortcuts) - popis konfiguracniho souboru  
gpicview ... prohlizec obrazku  
lxapperance ... nastaveni vzhledu LXDE  
lxlauncher ... otevre na plose interaktivni spoustec aplikace (neco jako menu)  
lxmusic ... prehravac hudby  
lxpanel ... manazer panelu a menu, je standartne spousten pri startu lxde  
lxpanelctl config ... konfigurace panelu  
lxrandr ... meni rozliseni obrazovky a dalsich monitoru, ukazuje jednotliva rozliseni - soucasti LXDE  
lxsession ... manazer sezeni - spousti autostart procesy, nastaveni plochy atd.  
lxsession-edit ... povoleni/zakazani programu v autostartu  
lxshortcut -o a.desktop ... Vytvori spoustec a.desktop  
lxshortcut -i pidgin.desktop -o a.desktop ... ze spoustece pidgin.desktop udela spoustec a.desktop  
lxtask ... okno seznamu aplikaci, cpu vyuziti, pamet atd. - neco jako top  
lxterminal ... terminal  
openbox --reconfigure ... nacte okofigurace lxde-rc.xml a zmeni parametry beziciho Openboxu  
pcmanfm ... filemanager  
startlxde ... spousteni LXDE, tento proces spusti dalsi pricesy jako lxsession atd  
su - -c nm-applet ... applet NetworkManager (v liste)  
xarchiver ... spravce archivu  
~/.config/lx* ... osobni nastaveni  
/usr/share/lx*/profile/ ... glogalni nastaveni  
xrandr --output VGA1 --left-of LVDS1 ... nastavi, ze druhy monitor bude nalevo od prvniho (mozno pouzit left-of, above, bellow)  
xrandr --output LVDS1 --mode 1440x900 ... zmeni rozliseni obrazovky  
xrandr --output VGA1 --same-as LVDS1 ... nastavi, ze oba monitory ukazuji totez  
xrandr --output VGA1 -off ... vypne zobrazovani na VGA1  

### Cinnamon

cinnamon --replace ... restart Cinnamonu  
cinnamon-settings panel ... konfiguracni panel  
cinnamon-settings applets  
cinnamon-settings extensions  
gsettings set org.cinnamon.desktop.wm.preferences num-workspaces 4 ... pocet pracovnich ploch  
gsettings set org.nemo.desktop show-desktop-icons false ... schovani ikon z plochy  
gsettings set org.cinnamon.desktop.wm.preferences resize-with-right-button true ... zmena velikosti okna pravym tlacitkem  
dconf dump /org/cinnamon/desktop/keybindings/ &gt; keybindings-backup.dconf ... export klavesovych zkratek  
dconf load /org/cinnamon/desktop/keybindings/ &lt; keybindings-backup.dconf ... import klavesovych zkratek  
gsettings set org.gnome.gnome-screenshot auto-save-directory %%file:///home/USER/some_path%% ... skreenshot  
/etc/xdg/autostart/nm-applet.desktop ... globalni profil appletu  
~/.config/autostart/nm-applet.desktop ... lokalni profil appletu  

====Nastaveni klavesnice====

```
[[http://wiki.eeeuser.com/howto:moveshiftkey|xmodmap]] ... zmena klavesnicove mapy a tlacitek mysi pod X
xmodmap -e "remove shift = Shift_L" ... zrusi funkci leveho shiftu
xmodmap -e "add shift = Shift_L" ... zapne funkci leveho shiftu
xmodmap -e "keycode 111 = Down" ... tlacitko nahoru bude delat akci "dolu"
xmodmap -e "remove lock = Caps_Lock" ... vypne funkci CapsLock
setxkbmap cz ... nastavi ceskou klavesnici pod X (resp. us anglickou, ...)
```

### Nastaveni plochy, setreni energie atd.

xsetroot ... meni nastaveni prvniho (root) okna  
xsetroot -solid navy ... nastavi barvu pozadi  
xset +-Dpms .. zapne setreni energie dpms pro Xka  
xset dpms force standby .. stanby mod ihned  
xset dpms force off .. ihned vypnejavascript:document.forms['EditForm'].screen.value=3;document.forms['EditForm'].submit();  
xset s -activate ... aktivuje setric  
xscreensaver -no-splash & ... zapne demona, ktery automaticky zapne setric obrazovky  
xscreensaver-command -activate ... aktivuje sporic v xscreensaved demonovi  
xdg-screensaver lock ... aktivuje sporic + zamkne obrazovku na heslo  
gnome-screensaver-command -l ... zamkne obrazovku v Gnome  

====Sdileni a pripojeni k X-windows====

```
xhost - bart ... zakaze prihlasovani do x z barta
xhost + 1.2.3.4 ... povoli sdileni techto Xek z adresy 1.2.3.4
xhost - uplne zakaze sdileni techto Xek
xauth list ... ukaze seznam certifikatu Magix-cookie
/etc/X11/xdm/kdmrc -> "-listen tcp" + otevrit posty 6000-6010 na FireWallu
```

##### vnc server

service vncserver start/stop/status  
/etc/sysconfig/vncservers  
$HOME/.vnc/xstartup  
vncserver  
vncpasswd  

##### vnc klient

vncviewer host:screen  
vncviewer -via user@host localhost:1 ... pres ssh  

#### NX

[NX](http://en.wikipedia.org/wiki/NX_technology) ... vylepseni X-server komunikace pres sit (SSH komunikace atd)  

##### Preposilani X packetu pres ssh

ssh -X aaa ... povoleni preposilani X paketu pri spojeni na server aaa  
ssh -Y aaa ... povoleni preposilani overenych X paketu pri spojeni na server aaa  
ssh -R 6000:localhost:6000 aaa ... spojeni na server aaa a vytvoreni tunelu pro port 6000 (porty pro prenos X paketu 6000-6009)  
export DISPLAY="localhost:0.0" ... nastaveni, ze X pakety pujdou portem 6000 (:1.0 pro 6001, ...)  
xauth list  

#### Ostatni prikazy

rexec ... tcp/ip prikaz posilajici prikaz vzdalenemu systemu k provedeni
import -window root obrazek.png ... screenshot  
xclock -d -update 1 -geometry +819+710 & ... hodiny  
startx -- :1 ... pusti dalsi x server (muze bezet na kazde konzole) s default windows manazerem  
xinit ... pusti x server bez windows manazera  
Shift-PgUp/PgDown  

### Menu, MIME typy a vychozi aplikace podle Freedesktop.org standartu

~/.config/ ... osobni nastaveni, soubory danne standartem [freedesktop.org](http://www.freedesktop.org/wiki/)  
[xdg-*](http://portland.freedesktop.org/xdg-utils-1.0/) ... utility z xdg-utils pro konfiguraci [freedesktop.org](http://en.wikipedia.org/wiki/Freedesktop.org) veci  
[xdg-mime](http://portland.freedesktop.org/xdg-utils-1.0/xdg-mime.html) ... prace s MIME, instalace novych, asociace aplikaci  
xdg-mime query filetype /tmp/obr.jpg ... zjisti, jaky mime typ odpovida tomuto souboru  
xdg-mime query default image/png ... zjisti, jaka aplikace otevre tento MIME  
xdg-mime default totem.desktop video/mp4 ... nastavi vychozi aplikaci pro MIME video/mp4  
alacarte - editor menu  
/etc/xdf/menus/*.menu ... definice slozek v nabidce hlavniho menu  
/usr/share/applications/*.desktop ... definice polozek v menu  
/usr/share/applications/defaults.list ... definice vychozich aplikaci pro jednotlive MIME typy  
/usr/share/applications/mimeinfo.cache ... vsechny registrovane aplikace pro jednotlive MIME typy  
/usr/share/mime/globs ... globalni nastaveni koncovek souboru a jejich MIME typu  
/usr/share/desktop-directories/*.directory ... definice nazvu slozek a ikon v hlavnim menu  
$HOME/.local/share/mime/globs ... definice koncovek souboru a nazvy MIME typu  
$HOME/.local/share/applications/mimeapps.list ... lokalni nastaveni pro uzivatele  
$HOME/.local/share/applications/defaults.list ... lokalni nastaveni pro uzivatele  

### Fonty

X Core fonts .. prvni, nevyhlazene fonty, jsou v xorg.conf, nacita je Xfs  
Xft .. definuje se v etc/fonts, ~/fonts/, pro GTK, Qt  
fonts.dir, fonts.scale .. seznam fontu v adresari, seznam skalovatelnych fontu .  
. vygeeneruje se mkfontdir, mkfontscale. Nejdrive spustit mkfontscale. Pak lze pridat do xorg.cfo, nebo xfs  
cp *.ttf cd /usr/X11R6/lib/X11/fonts/TTF  
ttmkfdir > fonts.scale  
mkfontdir  
xfontsel ... prehled x fontu vcetne jejich ukazky  
/etc/fonts/fonts.conf ... konfigurace fontu  
[fontconfig](http://freedesktop.org/software/fontconfig) ... nastroj na konfiguraci fontu  
fc-list ... seznam fontu co jsou k dispozici  
fc-cat ... informace o fontech v cache  
fc-cache /usr/share/X11/fonts/Type1... vytvori cache fontu  
fc-scan /usr/share/X11/fonts/Type1 ... prozkouma adresar a najde fonty  

### Oblibene programy

xnview ... prohlizec obrazku (xorg-x11-fonts-100dpi xorg-x11-fonts-75dpi xorg-x11-fonts-misc xorg-x11-fonts-ISO8859-1-100dpi xorg-x11-fonts-ISO8859-1-75dpi)  
recordmydesktop --on-the-fly-encoding --fps 6 --buffer-size 5000 -o a.ogv ... nahravani plochy i se zvukem  
cheese ... nahravani z kamery  

### ovladani oken, clipboardu atd.

xwininfo ... napise informace o oknu, ktere se vybere (rozmery, id, poloha, ...)  
xwininfo -root -children -int ... seznam vsech oken, id (jako integer), rozmery, poloha  
xwininfo -name "Queue Checker" ... id okna s timto popisem  
xprop -id 0x6e00faa ... napise informace o okne id 0x6e00faa = PID, atd  
xprop -id $(xprop -root 32x '\t$0' _NET_ACTIVE_WINDOW | cut -f 2) _NET_WM_NAME ... napise jmeno aktivniho okna\\s

xdotool getactivewindow ... ikaze id aktiviniho okna  
xdotool getwindowpid 212132 ... ukaze cislo pidu, co vlastni to okno  
xdotool getwindowgeometry 3124213 ... ukaze geometrii okna id 3124213  
xdotool search -name "Queue checker" ... ukaze id okna se jmenem queue checker  
xdotool search --pid 1234 ... ukaze id oken ktere vlasni proces 1234  
xdotool getmouselocation --shell ... ukaze lokaci mysi  
xdotool windowkill 12233 ... zabije okno id 12233  
xdotool click 1 ... klikne tlacitkem 1 (levym)  
xdotool mousemove 70 100 ... presune mys na pozici  
import a.png ... (ImageMagick) screenshot  
xclip -selection c -o ... vypise clipboard (ctrl-v)  
xclip -o ... vypise co je oznaceno  
echo test | selection c ... vlozi do schranky (ctrl-c)  
xsel ... vypise co je oznaceno kurzorem (jako xclip -o)  
qdbus org.gnome.ScreenSaver /ScreenSaver org.gnome.ScreenSaver.GetActive ... napise, zda je gnome screensaver aktivni  
qdbus org.kde.screensaver /ScreenSaver org.freedesktop.ScreenSaver.GetActive ... napise zda je kde screensaver aktivni  

##### xorg-x11-apps

[xwd](https://en.wikipedia.org/wiki/Xwd) ... screen saver, uklada do formatu xwd (X Window Dump)  
sleep 3 ; xwd -root | xwdtopnm | pnmtopng > Screenshot.png ... za 3 sekundy sejme celou obrazovku  
convert xwdss.xwd xwdss.png ... (ImageMagick) prevod xwd do png  
xwud ... prohlizeni xwd souboru. Dalsi programy co to podporuji jsou gimp, xnview, xv, ImageMagick, Netpbm, ...  
/usr/bin/identify a.png (ImageMagick) identifikuje soubor, ukaze rozmery atd  
/usr/bin/display a.png (ImageMagick) zobrazi obrazek, umoznuje editaci (crop, zvyraznovai)  
gnome-screenshot ... screenshot od gnona  

##### xautmatization

visgrep ... vizualni grep, najde obrazek na plose a zada jeho polohu  
patextract ... vyextraktuje cas png obrazku, lze pak pouzit visgrepem  
xte ... strojove ovladani mysi, klavesnice, klipbordu  

### Programy a uzitecne nastroje

/usr/bin/flameshot gui ... Flameshot - sejme cast obrazovky, umi do snimku kreslit
