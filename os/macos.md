## MacOS

### GUI

#### Finder

defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES ... nastaví, že Finder ukazuje plnou cestu pro aktuální zobrazení  
Shift-Command-G ... dialog na zadání cesty, kam se přemístit  

### Sluzby

launchctl list ... seznam slizem  
launchctl unload  /System/Library/LaunchDaemons/ssh.plist ... zastaveni/stop slushy  

### Uživatelé

dscl . -list / ... seznam včech spravovaných objektů pomocí dscl  
dscl . -list /Groups ... seznam uživatelských skupin  
dscl . -read /Users/uzivatel ... informace o uživateli uzivatel  
sudo dscl . -passwd /Users/uzivatel heslo ... nastavení hesla  
dscl . -delete /Users/uzivatel ... smaže uživatele  

### Balickovaci system

sudo installer -verbose -pkg aaa.pkg ... nainstaluje balíček  
pkgutil --pkgs ... seznam nainstalovaných balíčku  
pkgutil --pkg-info net.pulsesecure.TnccPlugin.pkg ... informace o balíčku  
pkgutil --only-files --files net.pulsesecure.TnccPlugin.pkg ... seznam nainstalovaných souboru z balíčku  

#### Homebrew

brew install corkscrew       # ==> tunnel SSH through HTTP proxies  
brew install htop            # ==> https://htop.dev  
brew install node            # ==> https://nodejs.org  
brew install tree            # ==> http://mama.indstate.edu/users/ice/tree  
brew install vim             # ==> https://www.vim.orgtunnel SSH through HTTP proxies  
brew install -vd Azure/kubelogin/kubelogin   ### nainstaluje kubelogin, -v verbose, -d debug  
brew install %%--%%cask balícek ... nejaké balíčky jsou typu cask - instalace balíčku  
brew uninstall cask -balíček ... odinstalace cask balíčku  
brew upgrade %%--cask --greedy --all%% ... upgrade a přeinstalování všech cask balíčků  
brew %%--repository%% ... ukáže adresář Brew  
brew doctor ... hledá provlémy v Brew  

#### Macports

port ... management [balíčků](https://ports.macports.org/search)  
sudo port -v selfupdate  
sudo port install nodejs10 ... instalace node  
port installed ... seznam nainstalovaných balíčků  

#### pkgsrc

### Sit/network

[https://github.com/xjasonlyu/tun2socks/wiki/Examples](https://github.com/xjasonlyu/tun2socks/wiki/Examples) ... Socks5 nastavení  
**stove karty**  
ifconfig ... seznam síťových zařízení a ip adres  
ifconfig lo0 10.0.0.1 alias ... pride dalsi alias (ip adresu)  
scutil --proxy ... ukáže nastavení proxy  

**Routing**  
netstat -rn #... zobrazi routovaci tabulku  
route delete default  
route add default 192.168.0.1  
route change default -interface $INTF  
route change 192.168.0.0/16 -interface $INTF  
route -n add -net 192.168.2.0/24 192.168.1.1  
networksetup -listallnetworkservices #... nastaveni site, stere pretrva restart  
networksetup -listnetworkserviceorder #.. jine vylistovani  
networksetup -setadditionalroutes networkservice [dest1 mask1 gate1] [dest2 mask2 gate2] ... [destN maskN gateN]]  

**firewall - pf packet filtering**  
`pfctl -d` ... zakáže packet filtering (firewall)  
`pfctl -e` ... opvolí firewall  
`pfctl -F all` ... Flush - smaže všechna pravidla (rules, nat, queue, info)  
`pfctl -z` ... smaže statistiky  
`pfctl -s all` ... ukáže všechna pravidla  
`pfctl -v -s rules` ... ukáže pravidla RULES i se statistikama  
`pfctl -vvsTables` ... seznam tabulek  
%%echo "rdr pass on lo0 inet proto tcp from any to 10.0.0.1 port 80 -> 127.0.0.1 port 3000" | sudo pfctl -ef -%%  
`pfctl -v -n -f /etc/pf.conf` ... otestovani sitovych pravidel  
`pfctl -v /etc/pf.conf` ... nacteni sitovych pravidel  
`pfctl -q` .. tichy mod  

**name resolution**  
discoveryutil udnsflushcaches  
dscacheutil -flushcache  

**Síťové profily**
networksetup -listlocations ... seznam profilů, tzv. lokací  
networksetup -getcurrentlocation ... ukáže aktuálmí profil  
networksetup -switchtolocation aaa ... přepne na profil aaa  

##### Microsoft Defender

mdatp  

##### zsh

for i in ${(f)services}; do echo a:$i; done ... rozloží mnoho řádkový text na pole jednořádkových a projede smyčkou for  

##### other

csrutil status ... system integrity protection status  

xattr -dr com.apple.quarantine /usr/local/bin/saml2aws ... povolí spouštění binárky  
### správa zařízení a disků

system_profiler SPUSBDataType ... ukáže připojená USB zařízení  
system_profiler SPPCIDataType ... sezam PCI zařízení  
system_profiler -detailLevel mini ... informace o systému - hardware, software, network  
diskutil list ... seznam disků  
diskutil listFilesystems ... seznam file systémů  
ioreg -p IOUSB ... seznam USB  

### Aplikace

#### Java Virtual Machine

/usr/libexec/java_home ... ukáže cestu k výchozí javě  
export JAVA_HOME=$(/usr/libexec/java_home -v 21) ... nastaví výchozí javu na verzi 21
