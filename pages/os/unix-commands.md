# UNIX - Prikazy

### Odkazy

[1-liners](https://github.com/pkrumins/bash-one-liners/blob/master/part1.txt) 1. cast jedno radkovych prikazu P.Kurminse  
[1-liners](https://github.com/pkrumins/bash-one-liners/blob/master/part2.txt) 2. cast jedno radkovych prikazu P.Kurminse  
[1-liners](https://github.com/pkrumins/bash-one-liners/blob/master/part4.txt) 3. cast jedno radkovych prikazu P.Kurminse  
[Linuxjournal.com](http://www.linuxjournal.com/)  

### Obrazovka

echo ... napise na obrazovku text  

clear ... vycisti screen  
tty ...  ukaze, ktera konzole je aktivni  
stty ... ukaze a meni parametry terminalu  
[screen](http://www.unixwerk.de/unix/screens.html) ... multitasking terminalu v jednom procesu  

### Procesy

/proc/$pid/fd/* ... seznam otevrenych souboru danym procesem  
at ... jednou spousteny proces  
batch ... spusti se proces, kdyz system neni vytizen  
bg ... rozjeti procesu a prevedeni do pozadu  
crontab ... pravidelne spoustene procesy  
disown -h %1 ... zprosti vlastnictvi k prosesu na pozadi (proces se neukonci odlogovanim)  
exec skript ... narhadi aktoualni behove prostredi (tedy napr. skript, shell atd) spustenim prikazu "skript"  
fg ... navrat preruseneho procesu do popredi  
ipcs ... (interprocess comunication status) ukazuje meziprocesorovou komunikaci  
ipcrm ... uvolnovani meziprocesorove sdilene pameti?  
jobs ... seznam prerusenych procesu  
kill ... zabiti procesu  
kill -HUP 393442 ... restartuje proces, pokud to umi, napr. sshd  
kill -STOP 1234 ... pauzne proces  
kill -CONT 1234 ... znovu ozivi proces  
lsof -nP ... seznam otevrenych souboru roznyma procesama  
nice ... meni prioritu spoustenych procesu  
nohup ... spusteni procesu na pozadi a ten neni dite shellu  
ps ... seznam procesu  
ps -e f ... podrobny stromovy seznam procesu  
ps xvvv ... podrobny popis parametru u procesu (mnoztvi pameni, jez zabira atd.)  
ldd ... seznam knihoven, jez uziva dany proces  
ldconfig ... v danem adresari nainstaluje novou knihovnu (nejcasteji /usr/lib)  
LD_LIBRARY_PATH ... promenna prostredi, kde jsou cesy ke knihovnam  
LIBPATH=/opt/freeware/lib/:/opt/IBM/ldap/V6.3/lib:/usr/lib ... cesty ke knihovnam, nejlepe danou promennou exportovat (export)  
strace mail ... spusti mail a zobrazuje kod  
strace -p 123 ... zobrazuje kod procesu s PID 123  
wait 1234 ... pocka az proces 1234 posle Return Code  
proces & ... spusti proces na pozadi  
proces |& ... spusti proces na pozadi, vstupy a vystupy jdou do procesu (napriklad ksh |&)  
echo $$, $! ... napise PID aktualniho procesu a posledniho procesu na pozadi  
echo $- ... prepinace aktivniho shellu  
$PPID ... PID rodicovskeho procesu  

### Knihovny

Objekty (soubory s priponou .o) jsou zkompilovane kody - knihovny, ktere lze linkovat ke spustitelnym souborum. Josu ve formatu ELF (Executable and Linkef Format).
Ke kompilaci a liknovani je treba tez hlavickovy soubor s priponou .h.
Knihovny lze zabalit do archivu knihoven (program ar, koncovka .a), jsou to staticke knihovny - prilinkuji se v dobe kompilace do kodu spustitelneho programu.
Shared object libraries (koncovka .so) jsou dynamicke knihovny, zkompilovane parametram fPIC (Position Indepencent Code), ktere se linkuji k programum dynamicky az behem zavadeni, ci behu.  

ar -t -v /usr/lib/x86_64-redhat-linux5E/lib64/libanl.a ... ukaze obsah archivu statickych knihoven (seznam ktere knihovny obsahuje archiv .a)  
export LIBPATH=/opt/freeware/lib/:/opt/IBM/ldap/V6.3/lib:/usr/lib ... konfigurace cest k dynamickym knihovnam  
export LD_LIBRARY_PATH=/opt/freeware/lib/:/opt/IBM/ldap/V6.3/lib:/usr/lib ... konfigurace cest k dynamickym knihovnam  
export LD_RUN_PATH=/opt/freeware/lib/:/opt/IBM/ldap/V6.3/lib:/usr/lib ... konfigurace cest k dynamickym knihovnam  
ldd /usr/bash ... vypise, ktere dynamicke knihovny pouziva dany binarni spustitelny soubor  
ld -G *.o -o libfoo.so  ... linkuje knihvny (objekty) do libfoo.so  
ldconfig -p ... vylistuje knihovny a lokace, ktere se mohou pouzivat  
/etc/ld.so.conf ... konfigurace cest k dynamickym knihovnam  
nm /lib/ld-2.12.so ... vypise staticke funkce a objekty ze zadane knihovny  
nm --dynamic ... vylistuje dynamicke objekty (funkce, konstanty)  
objdump -a /usr/lib/libcupscgi.so.1 ... vylistuje z jakych knihoven se sklada archiv, ci knihovna  
objdump -x /usr/lib/libcupscgi.so.1 ... vylistuje hlavicky a zavislosti na jine dynamicke knihovny  
readelf -s /usr/lib/libcupscgi.so.1 ... vylistuje funkce a objekty z knihovny (jako nm -D)  

### Uzivatele

newgrp ... zmeni aktualni skupinu uzivatele  
finger ... info o uzivateli  
id (uzivatel)... zobrazi info o (aktualnim) uzivatel  
last ... vypis poslednich loginu uzivatelu (/var/adm/wtmp)  
lastb ... vypis poslednich spatnych prihlaseni (/var/log/btmp)  
logname ... vypise id prihlaseneho uzivatele  
passwd ... zmena hesla  
su ... (switch user) smeni uzivatele  
sudo ... pod jinym uzivatelem provede prikaz  
/etc/sudoers ... konfigurace  
visudo ... editace /etc/sudoers  
w ... seznam zrovna prihlasenych uzivatelu  
who ... seznam zrovna prihlasenych uzivatelu  
whoami ... login aktualniho uzivatele  

### Cas

date ... zobrazeni, zmena datumu  
cal ... zobrazeni kalendare  

### Disky, filesystemy

pwd ... aktualni adresar  
df ... disk free - ukaze volne misto na primountovanych discich  
du -smx .[!.]* ... disk usage - ukaze kolik zabira ktery soubor v aktualnim adresari na disku, vcetne skrytych  
fsck ... (File system check) Kontrola a oprava struktury disku  
sync ... synchronizuje disk  
mt ... (magnetic tape) ovlada magnetickou pasku
swpon -a ... aktivuje definovane swapdisky  

### Soubory, adresare

cat ... vypise obsah souboru  
cd ... (change directory) zmena adresare  
chmod ... zmena prav souboru  
chown ... (change owner) zmena vlastnika souboru  
chgrp ... (change group) zmeni skupinu uzivatele  
chroot /home/aaa ... zmeni v prostredi korenovy adresar. / bude v /home/aaa  
cksum soubor ... spocita CRC souboru soubor  
cmp ... napise prvni rozdilny bit 2 zadanych souboru  
cp ... (copy) kopiruje soubor do jineho adresare  
[cpio](http://www.mppmu.mpg.de/Introduction/general/subsubsection2.5.8.2.2.html) ... copy to i/o devices  
cpio -idmv &lt; soubor.cpio ... rozbali soubory z cpio archivu  
cpio -itv &lt; soubor.cpio ... vylistuje archiv soubor.cpio  
cpio -ov &lt; filenames &gt; /dev/rfd0 ... zkopiruje soubory na disketu  
find . -print | cpio -ov > aaa.cpio ... zkopiruje vsechny soubory v adresari i  podadresarich  
dd conv=noerror,sync if=/dev/fd0 of=(filename) ... nacte disketu do souboru, ignoruje chyby disku  
diff ... (differences) najde rozdily v zadanych souborech  
dump ... zalohovani souboru a FS  
file ... rozpoznani zadaneho souboru  
[find](http://www.softpanorama.org/Tools/Find/find_mini_tutorial.shtml) /home/user -name aaa.txt ... program pro vyhladavani souboru na disku podle ruznych parametru  
find / \( -user RO45853 -o \( -perm -0040 -o -perm -0020 -o -perm -0010 \) \( -group IBMAdmin -o -group bin -o -group sys \) \) -type d -ls ... slozitejsi podminka pro find  
gzip ... de/komprese do souboru gz  
install -m 755 soubor /kam ... zkopiruje soubor do lokace kam a priradi mu pristupova prava  
ls ... (list) vypis seznamu souboru v danem adresari  
ln ... (link) vytvori zastupce k souboru  
mkdir ... (make directory) vytvori adresar  
more ... vypise obsah souboru s cekanim po strance  
mv ... (move) presune soubor do jineho adresare  
ncheck ... ukaze jmeno souboru podle idonde  
rm ... (remove) vymaze soubor  
pax ... alternativa pro cpio a tar  
rmdir ... (remove directory) smaze adresar  
stat file.txt ... informace o souboru - velikost, inode, pristupy atd.  
[tar](http://www.computerhope.com/unix/utar.htm) ... (tape archiver) ulozeni souboru do jednoho souboru  
tar cvf - abc | gzip > abc.tar.gz ... baleni a komprimovani jednim prikazem  
touch ... vytvoreni prazdneho souboru, zmena casu prirazenych k souboru  
umask 077 ... nastavi defaultni prava pro nove soubory (vypne vsechny defaultni prepinace pro skupinu a ostatni)  
wc ... (word count) spocite pocet bytu, slov a radku  
which x y ... ktery soubor se spusti zadanim prikazu x a y  
whereis x y ... kde se nachazi spustitelny soubor x a y  
whence x y... kde se nachazi, vcetne aliasu spustitelny soubor x a y  
zcat (compress, uncompress) ... cteni zkompresovaneho .Z, .gz souboru, komprese, dekomprese  
zip ... komprese, dekomprese do .zip  

### Komunikace

mail ... cteni posty  
mail a@b.c ... napise mail na adresu a@b.c (konec ctrl-d)  
talk ... chat s jinym prihlasenym uzivatelem  
wall ... napise zpravu vsem prihlasenym uzivatelum (konec ctrl-d)  
echo Hello > /dev/pts/0 ... posle Hello na konzoli pts/0 (ukaze se v danem terminalu na obrazovce)  
write ... posle radky textu prihlasenemu uzivateli (konce ctrl-d)  

wget http://www.seznam.cz ... stahne html stranku do soubrou  
[curl](http://curl.haxx.se/docs/manual.html) -u user:passwd ftp:%%//%%machine.domain:port/full/path/to/file ... stahne soubor s ftp serveru  
curl -u username: %%--key ~/.ssh/id_dsa --pubkey ~/.ssh/id_dsa.pub scp://%%shell.example.com/~/personal.txt ... stahne soubor pres ssh  
curl %%--ftp-ssl ftp://%%files.are.secure.com/secrets.txt ... stahovani pres sftp  
curl -u user:passwd -x my-proxy:888 http:%%//%%www.get.this/ ... stahovani pres proxy  
curl -o aaa.html http:%%//%%mypage.org/bbb.html ... ukozi stranku do souboru aaa.html
curl -O http:%%//%%www.seznam.cz ... stahne stranku do souboru  
curl -T - http:%%//%%www.upload.com/myfile ... nahraje standartni vstup na stranku (Musti tam byt "PUT" znacka)  
curl %%-d "name=Rafael%20Sagula&phone=3320780"  http://%%www.where.com/guest.cgi Posle metodou POST data  
curl -X POST -H "Content-Type: application/json" -d {name=a; password=b} ... posilani JSONu  
curl %%-F "file=@cooltext.txt" -F "yourname=Daniel" -F "filedescription=Cool text file with cool text inside" http://www.post.com/postit.cgi%% ... odesle soubor a vyplni pole na strance  
curl -A 'Mozilla/3.0 (Win95; I)' http:%%//%%www.nationsbank.com/ ... tvari se jako mozilla  
curl %%--verbose --header 'Host: www.example.com' 'http://10.1.1.36:8000/the_url_to_test'%% … Pouziti virtualni domeny na IP adrese  
curl %%-w "$i: %{time_total} %{http_code} %{size_download} %{url_effective}\n" -o "/dev/null" -s http://address.cz/test.html%% ... vypis custom informaci k requestu (cas odezvy, http kod, velikost) - dobre pro performance testy  

### vstup/vystup

[awk](awk.html) ... programovatelny editor textu z stdin do stdout  
du -smx .[!.]* | awk '{if( $1 > 10){print $2}} ... pokud prvni slovo je > 10, vypis drue slovo  
du -h . |awk '{if(index($1,"G") > 0){print $0}}' ... vypise radky, kde prvni promenna s pismenem G je vetsi nez nula  
cat rc.tcpip | awk '{if ($2 ~ /xntpd/) sub(/^#/,"",$1)}1' > rc.tcpip ... odkomentuje # xntmp  
{ rm rc.tcpip && awk '{if ($2 ~ /xntpd/) sub(/^#/,"",$1)}1' > rc.tcpip; } < rc.tcpip ... to same  
cut ... z kazdeho radku ukaze pouze urcite sloupce  
cut -c 1-8 aaa.txt   ... napise prvnich 8 znaku z radku
cut -d ' ' -f 1,2,5  ... Vypise 1., 2. a 5. pole odeelene mezerou
egrep ... (enhanced grep) umi funkci OG  
fgrep ... (fast grep) rychlejsi grep - vyhledava jen slova  
[grep](http://www.techonthenet.com/unix/basic/grep.php) ... filtruje ze vstupu radky, ktere obsahuji nejaky text zadany [regularnimy](http://www.robelle.com/smugbook/regexpr.html) [vyrazy](http://www.panix.com/~elflord/unix/grep.html)  
head ... prvnich 10 (nekolik) radku z vstupu  
printf ... tisk formatovanych textu  
LEN=20 ; printf -v char  "%${LEN}s" ""; echo ${char%%//%% /-} ... napise 20x pomlcku  
printf "%5sahoj" ... 20xmezera + ahoj  
rew ... vypise pozpatku, co se do nej posle  
[sed](http://4bcad.com/doc/notes/sed) ... (stream editor) edituje tok textu  
sed -e 'rozsah1PRIKAZ1;rozsah2PRIKAZ2' ... provede posloupnost prikazu na posloupnosti rozsahu  
sed -ne '/TOM!/s/kde je TOM? /;1,5p' ... na radcich, kde neni retezec TOM, napis na zacatek "kde je TOM", vytiskni jen prvich 5 radku  
sed 's:$:\r:' -i soubor ... prevede unixovy soubor na dosovy  
sed 's/\s\{2,\}/ /g;s/^ %%//%%g;' -i soubor ... Provede 2 substituce - smaze vicenasobne bile znaky a mezery na zacatku radku  
sed '/^$/d' ... smaze prazdne radky  
sed -i '/Windows/d' /tmp/data.txt ... Smaze radky se slovem Windows primo v souboru data.txt  
sed '/WORD1/,/WORD2/d' ... smaze vsechny radky mezi slovem WORD1 a WORD2 vcetne techto 2 radku  
sed -n 22p ... vypise 22. radek  
sed '1iaaa' soubor ... vlozi radek pred prvni radek a napise text aaa  
sed '/^{/,/^}/!d' ... vytiskne vse mezi prvni slozenou a posledni slozenou zavorkou (pred a po smaze) - Vyselektuje JSON  
sort ... tridi radky ve vypisu  
sort -k 3 ... pridi podle tretiho slova  
sort -t : -k 2 -n ... numericky tridi podle druheho slova oddeleneho znakem :  
string /etc/fstab ... ukaze soubor /etc/fstab, netisknutelne znaky neukaze  
tail (-f) ... poslednich 10 (+- nekolik) radku z vstupu (pernamentne)  
tee ... sandartni vstup vstup posle na st. vystup i do souboru  
tr ... prevede/smaze nektere znaky  
tr '[A-Z]' '[a-z]' ... prevede velka pismena na mala  
tr ";" "\n" ... zameni strednik za novy radek  
tr -d '\r' &gt; input.file &lt; output.file ... prevede dosovy textovy soubor na unixovy  
uniq ... maze duplicitni radky  
wc ... pocita radky, slova
ls >/tmp/ls 2> &1 ... vystup, i vystup chyb jde do /tmp/ls  
script -c bash vystup.txt ... presmeruje veskery vystup i do souboru. -t jsou casove znamky  

### shell

alias l='ls -l' ... prezdivka l je misto ls -l  
echo $$ $_ $(date + &quot;%m&quot;)... napise PID procesu, posledni prikaz(vystup) a minutu  
echo %%$[^1]

[^1]: 10+10%% ... soucet 10+10  
echo ${AAA} ... vypise promennou AAA  
M=aa;aa=5;eval echo \${$M} ... vyhodnoceni promenne odkazujici na promennou  
typeset l AAA ... zmeni pismena v promenne AAA na mala  
echo ${#AAA} ... vypise delku promenne AAA  
echo $0 $# $* ... napise jmeno aplikace, pocet parametru, vsechny parametry  
echo $? $! $1 ... napise posledni exit hodnotu, pid posledni bg aplikace, prvni argument  
(sleep 6000) & sleep 2 ; kill $! ... timeout pro prikaz - ukonci prikaz po 2 sekundach, pokud se nedokonci  
echo [${num:5:7}](http://www.softpanorama.org/Scripting/Shellorama/Reference/string_operations_in_shell.shtml) ... vypise 5 az 7 znak z promenne $num  
${probenna/CO/ZACO} ... zameni prvni retezec CO za ZACO  
${probenna%%//%%CO/ZACO} .. zameni vsechny retezce CO za ZACO  
B=1;A=B;C=${!A} ... neprimy odkaz. Udela jakoby C=$($A) (to same co eval C=\$$A)  
aaa="ahoj"; echo $aaa; echo ${aaa} ... prirazeni a vypis promenne  
pole[0]="cau"; echo ${pole[0]} ... definovani prvku pole, vypis  
set A X 1 2 3 d e f ... nadefinuje pole X skladajici se z prvku 1 2 3 d e f  
set +A X a b c ... prepise prvni 3 prvky pole X na a b c  
unset X ... zrusi pole  
typeset X[0]="1" X[1]="2" X[2]="a" ... dalsi definice pole X  
typeset -u X ... prevede vsechny prvky z pole X do velkych pismen  
typeset -L2 X ... vsechny prvky orizne na 2 znaky  
typeset -A Y[A]=a Y[B]=b ... definice asociativniho pole  
echo "${pole[*]), ${#arrname[*]}" ... vypise vsechny prvky pole a jejich pocet, kornshel dovoluje max.4096 prvku  
${array}, $array ... prvek 0 z pole array  
${array[n]} ... prvek n z pole array  
${array[n+2]} ... prvek n+2 z pole  
${array[$i]} ... prvek $i z pole  
${array[*]}, ${array[@]} ... Vsechny prvky z pole  
${#array[*]}, ${#array[@]} ... Pocet prvku v poli  
${#array[n] ... Delka prvku n z pole array  
${!array[*]}, ${!array[@]} ... vsechny indexy inicializovanych prvku pole  
${!array[*]:n:x} ... x prvku pole pocinaje prvkem n  
${!array[@]:n} ... Vsechny prvky z pole zacinaje prvkem n  
echo ${aaa:-"ahoj"} ... vypise promennou aaa pokud existuje, pokud ne tak "ahoj"  
echo ${aaa:+"ahoj"} ... vypise "ahoj", pokud promenna aaa existuje  
echo ${aaa:?"aaa not defined"} ... vypise ahoj, nebo vyskoci s hlaskou "aaa not defined"  
echo ${aaa:="ahoj"} ... vypise aaa, pokud existuje. Pokud ne, tak se aaa priradi ahoj a pak se vypise  
echo ${aaa:%.*} ... v promenne smaze nejmensi mozny vyskyt regularniho vyrazu .* od konce  
echo ${aaa:<nowiki>%%</nowiki>.*} ... v promenne smaze nejvetsi mozny vyskyt regularniho vyrazu .* od konce  
echo ${aaa:#.*} ... v promenne smaze nejmensi mozny vyskyt regularniho vyrazu .* od zacatku  
echo ${aaa:##.*} ... v promenne smaze nejmensi mozny vyskyt regularniho vyrazu .* od kacatku  
IFS=":"; for i in "a:b:c"; do echo $i; done ... nastavi oddelovac :  
${variable%%//%%pattern1/pattern2} ... Nahradi vsechny vyskyty vyrazu pattern1 za pattern2 v promenne  
${variable/pattern1/pattern2} ... Nahrani prvni vyskyt vyrazu pattern1 za pattern2 v promenne  
${variable/#pattern1/pattern2} ... Nahradi prvni vyskyt  vyrazu pattern1 za pattern2 v promenne, jestlize promenna zacina vyrazem pattern1  
${variable/%pattern1/pattern2} ...  Nahradi posledni vyskyt  vyrazu pattern1 za pattern2 v promenne, jestlize promenna konci vyrazem pattern1  
${variable:start} ... Vrati promennou zacinajicim na pozici start az do konce promenne  
${variable:start:length} ... Vypise z promenne lenght znaku zacinajicich na pozici start  
env ... zobrazi promenne prostredi  
envsubst <vstup.txt >vystup.txt ... vysubstituuje text $X a ${X} za hodnoty systémových proměnných  
export AAA ... promennou AAA vyexportuje pro potomky  
exit 0 ... ukonci skript/shell s return codem 0  
fc ... (fix command) prace s historii shellu  
fc -c ... r ... posledni prikaz  
fc -l 1 ... seznam vsech prikazu od prvinho  
help ... hapoveda k vestavenym prikazum  
history ... vypis cele historie prikazu  
let "SOUCET = $AAA + 1" ... Pricte k promenne AAA 1 a priradi vysledek promenne SOUCET  
logout ... odhlaseni z shellu  
pwd ... vypise aktualni adresar  
read ... precte vstup ze standartniho vstupu  
while read line; do echo $line; done &lt; a.txt ... cte soubor radek po radce  
while read line; do echo $line; done &lt; &lt;(ls) ... cte vystup z prikazu radek po radku (bash)  
return 1 ... ukonci funkci a vrati RC=1  
shift ... presune $n na $n-1  
set -o ... zobrazi mod editace prikazove radky  
set ... vypise promenne  
shopt ... zobrazuje nastaveni shelu  
sleep 2 ... shell pocka 2 sekundy  
test $a -eq 100 ... porovnavani a testovani promennych a souboru - vrat 0 pokud promenna a je rovan 100  
[ $test = a@(123 ]( $test = a@(123 ) ... zavorky misto test  
[  $date =~ ^[0-9]{8}$ ](  $date =~ ^[0-9]{8}$ ) ... regularni byrazy  
timeout 60s wait 3000 ... timeout pro prikazy - ukonci po 60 sekundach pokud prikaz neskonci  
type sh ... napise, jako jako co shell interpretuje sh  
ulimit ... nastaveni a zobrazeni omezeni shellu  
unalias ... zrusi prezdivku  
unset ... zrusi promennou  
[promenne prostredi shellu](http://www.kingcomputerservices.com/unix_101/understanding_unix_shells_and_environment_variables_part_2.htm)  
xargs prg ... Precte radky z stdin preda je jako argumenty programu prg  
ls | xargs -t -I {} mv {} {}.old ... priklad :-)  
[set -o emacs](http://www.unixwerk.de/unix/ksh_emacs.html) ... prepne ksh do emacs ovladani  

### programovani (podminky)

cd a &amp;&amp; echo jsem v a ... pokud se povede cd a, pak udelej druhy prikaz  
cd a || echo nejsem v a ... pokud se nepovede cd a, pak udelej druhy prikaz  
[test](http://wiki.bash-hackers.org/commands/classictest) ... otestovani podminky  
if x then y else z fi ... pokud x, potom y, jinak z  
read x ... nacte z klavesnice radek a priradi jej promenne x  
for x in y do z done ... promenne x prirad postupne prvky z y a vzdy proved z  
while x; do y done ... dokud je pravda x pak delej y  
until [ podminka ]( podminka ); do prikaz; done ... delej, dokud nenastane podminka  
exit n ... ukonci davku a vrati vystupni kod n  
shift ... posune argumenty doleva  
prikaz1 && prikaz2 ... pokud se provede prikaz1, pak vykonej prikaz2 a vrat nula, pokud vystup obou je 0  
prikaz1 || prikaz2 ... pokud se provede prikaz1, pak vykonej prikaz2 a vrat nula, pokud vystup aspon jednoho je 0  
continue ... skoc na konec cyklu  
break ... ukonci cyklus  
function aaa { } ... definovani funkce  
aaa () {} ... definovani funkce  

##### Parametry skriptu

getopts ":s:a:" PARAMETR ... vrati parametr, se kterym byl volan prikaz (-XXX), kde povolene parametry jsou a a s\\

```
while getopts ":s:ab" PARAMETR; do
    case $PARAMETR in
        a|b    ) echo parametr a nebo b;;
        s    ) echo parametr s ma argument $OPTARG;;
        *    ) echo "Neco jineho"
    esac
done
shift $(($OPTIND - 1)) # pote prvni parametr skriptu bude prvni text bez minuska
```

$@ parametry v uvozovkach, oddelene mezerou  
$* parametry oddelene mezerou  
$# pocet parametru  
$0, $1, ... nulty, prvni parametr  

### samorozbalovaci skripty

clanek [Bash Self-Extracting Script](http://www.linuxjournal.com/node/1005818) na Linuxjournal  
[Jak rozbalit soubor ze samorozbalovaciho skriptu](http://stackoverflow.com/questions/20758981/self-extracting-script-in-sh-shell)  

### kodovani, kryptovani, komprese

echo -n 'Ahoj' | base64 ... enkryptuje text do base64  
echo -n c2NvdHRsaW51eC5jb20gcm9ja3MK | base64 -d ... dekryptuje base64 text  
compress ... komprese a rozbaleni .Z souboru  
gzip ... komprese a rozbaleni .gz souboru  
gpg ... gpg kryptovani  
openssl  

### ostatni

basename /a/b/c ... vrati jmeno souboru, tedy c  
expr 1 + 2 ... vypocita 1 + 1  
[^2]

[^2]:  1 + 2  ... to same  
let 1 + $cislo ... to same
bc ... kalkulacka  
$result=$(print "n=1;for(i=1;i<8;i++)n=i*n;n"|bc) ... vypocita 8 faktorial  
man  
info  
telinit n ... prepne runlevel na cislo n  
telinit -q ... ukonci init, napr. pro odzkouseni syntaxe  
shutdown ... vypnuti, restartovani, upozorneni na vypnuti  
uptime ... Ukaze, jak dlouhu system bezi od minuleho vypnuti/restartu  
who -r ... ukaze momentalni runlevel  
hostname ... jmeno pocitace  
hostname aaa ... zmeni jmeno pocitace na aaa  
host aaa ... prevede aaa na numerickou adresu a opacne  
nolookup www.seznam.cz  
dig www.seznam.cz  
lpc ... Check and control the printer  
lpq ... ukaze obsah tiskove fronty  
lprm ... maze z tiskove frony  
logger -ip auth.notice -t sshd "Alois se pripojil a provadi $SSH_ORIGINAL_COMMAND" ... zapise "Alois se pripojil a provadi prikaz" do logu udalosti ve /var/log/*  
rup ... ukaze, jak dlouho bezi pocitace na siti  
uname ... informace o systemu a jadru  
cat /etc/issue ... informace o OS  
watch -n 60 ls ... spusti ls kazdych 60 sekund  

ftpwho ... kdo je pripojeny na ftp  

### Konverze

catdoc ... prevod MS Word .doc do txt a tex  

### sitove nastroje

[nc](http://www.g-loaded.eu/2006/11/06/netcat-a-couple-of-useful-examples/) ... netcat  
nc -vz  -w3 -n 129.39.133.239 9497 ... otestuje, zda je na adrese 129.39.133.239 otevreny port 9495, timeou 3 sec  
nc -l 3333 ... posloucha na portu 3333  
nc 1.2.3.4 3333 ... posila na port 3333  

##### Transfering files

cat backup.iso | nc -l 3333  
nc 192.168.0.1 3333 > backup.iso  

##### Transfering - pkazuje progress

cat backup.iso | pv -b | nc -l 3333  
nc 192.168.0.1 3333 | pv -b > backup.iso  

##### Zalohovani

dd if=/dev/hdb5 | gzip -9 | nc -l 3333  
nc 192.168.0.1 3333 | pv -b > myhdb5partition.img.gz  
tar -czf - /etc/ | nc -l 3333  
nc 192.168.0.1 3333 | pv -b > mybackup.tar.gz  

##### Bezpecnost

cat backup.iso | nc -l 3333  
ssh -f -L 23333:127.0.0.1:3333 me@192.168.0.1 sleep 10;  
nc 127.0.0.1 23333 | pv -b > backup.iso  

nc abc.cz 22 #... jako telnet  
nc -z 192.168.0.1 80-90 #... Port scanner  
nc -l -p 12345 -e /bin/bash  #... Presmerovani shellu na port  
nc -l -p 12345 | nc tomas.lipensky.cz 80 | nc -l 123456  #... nc jako proxy - port worwarder  
nc -X 4 -x 129.39.133.102:1080 192.168.13.44 22 #... Otevre tunel pres proxy  

ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_muj ... vyganeruje RSA klic pro SSH  
ssh-keygen -lf ~/.ssh/id_muj.pub ... ukaze fingerprint klice - ukazuje se pri veborse loging v auth.log  
ssh-keygen -R SERVERNAME ... smaže s known_hosts  
ssh-agent bash ... spust bash s ssh-agentem, ktery umi nahrat do pameti hesla ke klicum  
ssh-add ~/.ssh/id_muj ... po zadani hesla umozni pouzivat certifikat bez hesla  
ssh-add -l ... vylistuje klice v pameti  
ssh-add -L ... ukaze verejny klic ke klicum v pameti  
[Nastaveni sftp a logovani sftp udalosti](http://www.the-art-of-web.com/system/sftp-logging-chroot/)  
[/etc/sshd/sshd_config](http://linux.die.net/man/5/sshd_config) ... nastaveni ssh daemona, uzitecne prikazy = LogLevel, ForceCommand, Match User aaa pravidla,  
~/.ssh/authorized_keys ... nastaveni klicu, pred klicem muze byt omezeni, jako treba command="/bin/ls", from="192.*.*.*", environment="REMOTEUSER=jrhacker" ...  
ssh serverA "bash -s" &lt; ./skript.sh ... spusti lokalni skript na vzdalenem pocitaci  
ssh -X server ... povoli X11 forwarding, nastavi DISPALY a xauth. X11Forwarding musi byt povoleno v /etc/ssh/sshd_config. Pri sudo se musi pouzit xauth  
xauth add $(xauth -f ~USER/.Xauthority list|tail -1) ... nastavi xauth pro forwardovani X11 packetu  
autossh -X -L 5432:remote_DB_server:5432 -R 873:local_RSYNC_server:873 user@remote_ssh_server ... jako ssh -L -R (socks proxy), ale obnovuje tunel po skončení sezení
