### Odkazy

[https://tldp.org/LDP/Bash-Beginners-Guide/html/](https://tldp.org/LDP/Bash-Beginners-Guide/html/) ... Bash pro zacatecniky  

### Promenne

#### typ znak

`promenna="Ahoj svete"` ... definice promenne  
`: ${aaa?Promenna neni nadefinovana}` ... overi, zda je promenna aaa nadefinovana, jinak vyskoci s RC1 a textem: aa: Promenna neni nadefinovana  
`echo ${ccc:?chyba}` ... neprovede echo, kdyz promenna ccc nexistuje, nebo je nulova, vyskoci s RC 1 a textem ccc: chyba  
`echo ${promenna-"vychozi"}` ... vypise promennou, kdyz je definovana, tak text "vychozi", lze pouzit i prikaz `whoami`, nebo promennou $HOSTNAME.  
`echo ${retezec:-ahoj}` ... vypise promennou retezec, pokud je prazdny, nebo nenadefinovany, jinak vypise "ahoj"  
`echo ${retezec:=ahoj}` ... vypise promennou retezec. Pokud je prazdny, nebo nenadefinovany, nadefinuje ji na ahoj a vypise ahoj  
`echo ${retezec:+cau}` ... vypise cau, pokud je promenna retezec nadefinovana a neprazdna (opak operatoru -)  
`echo ${promenna:3}` ... vypise promennou promenna, vynecha prvni 3 znaky  
`echo ${promenna:3:3}` ... vypise promennou promenna, vynecha prvni 3 znaky, napise jen nasledujici 3 znaky  
`echo ${promenna/svete/chlape}` ... vypise promennou promenna, nahradi vyskyt slova svete za chlape  
`echo ${promenna#A*j}` ... smaze z textu pocatecni nejkratsi mozny pattern ze zacatku textu, vypise jen konec bez patternu  
`echo ${promenna##A*j}` ... smaze z textu pocatecni nejdelsi mozny pattern ze zacatku textu, vypise jen konec  
`echo ${promenna%A*j}` ... smaze z textu koncovy nejkratsi mozny pattern ze zacatku textu, vypise jen zacatek bez patternu  
`echo ${promenna<nowiki>%%</nowiki>A*j}` ... smaze z textu koncovy nejdelsi mozny pattern ze zacatku textu, vypise jen zacatek  
`echo ${promenna/aaa/j}` ... v promenne promenna nahradi jeden vyskyt podretezce aaa za j  
`%%echo ${promenna//aaa/j}%%` ... v promenne promenna nahradi vsechny vyskyty podretezce aaa za j  
`echo ${promenna/#*a/j}` ... v promenne promenna nahradi zacatecni vyskyt podretezce aaa za j, ekvivalent ^*a  
`echo ${promenna/%*a/j}` ... v promenne promenna nahradi koncovy vyskyt podretezce aaa za j, ekvivalent *a$  
`echo ${!a*}` ... vypise vsechny promenne, ktere zacinaji na a  
`echo ${!aaa}` ... kdyz promenna aaa obsahuje nazev jine promenne, tak vypise hodnotu odkazovane jine promenne  
`echo ${#prommena}` ... vypise pocet znaku  
`unset promenna` ... smaze (oddefinuje) promennou  

#### typ pole

declare -p pole
pole=(asi jeden clovek) ... definice pole  
declare -p pole1=(a v c) ... jina definice pole  
echo ${pole[1]} ... vypise druhy clen pole  
declare -p pole ... vypise typ promenne a jeji hodnotu  

#### typ cele cislo

declare -i cislo=10  

#### konstanty

readonly PI=3.14 ... definice konstatny, neda se zmenit  

### specialni zarizeni

cat </dev/tcp/time.nist.gov/13 ... otevre spojeni na server time.nist.gov port 13, vypise cas  

echo "HEAD / HTTP/1.0" >/dev/tcp/tomas.lipensky.cz/80 ... ping na URL  

exec 5<>/dev/tcp/www.net.cn/80  
echo -e "GET / HTTP/1.0\n" >&5  
cat <&5 ... tako telnet
