# [TCL](http://en.wikipedia.org/wiki/Tcl)/Jacl

### Externi odkazy

[Jacl](http://publib.boulder.ibm.com/infocenter/wsdoc400/v6r0/index.jsp?topic=/com.ibm.websphere.iseries.doc/info/ae/ae/rxml_commandline.html) na IBM  
[dalsi popis Jacl](http://utenti.multimania.it/yanorel6/2/ch55.htm)  

### Promenne

set a 5 ... nastavi promennou a  
set b $a ... nastavi promennou a podle promenne b  

unset a b ... zrusi definici promenne a a b  
info exist a ... vrati 0 pokud promenna neexistuje, jinak 1  
set len [string length RETEZEC] ... priradi promenne len delku retzce RETEZEC  
global len ... nadefinuje promennou $len v procedure z globalniho globalni prostredi - lze k ni pristupovat z procedury  
<b>cisla</b>  
expr $CISLO*4 ... provede vypocet  
expr sqrt(5*$CISLO) ... vypocita odmocninu z 5 x CISLO  
incr a ... zvetsi hodnotu a o 1  
<b>retezce</b>  

append "ahoj" vazeny pane ... prida na konec skupiny pismen = ahojvazenypane  
string length $TEXT ... delka retezce $TEXT  
string index "Ahoj" 2 ... vypise znak o indexu 2 (o)  
string range {Ahoj, jak se mas} 3 6 ... vypise znaky od indexu 3 po index 6  
string compare TEXT1 TEXT2 ... porovna TEXT1 a TEXT2. -1 pokud je TEXT1 lexikograficky mensi, 1 pokud je vetsi  
string match TEXT1 TEXT2 ... 1 pokud se texty shoduji, jinak 0  
string first "jak" "Ahoj jak se mas" ... vrati index 5 prvniho vyskytu podretezce, jinak -1  
string last "jak" "Ahoj jak jak se mas" ... vrati index 9 posledniho vyskytu podretezce, jinak -1  
string tolower AHOJ ... prevede text na mala pismena  

string toupper ahoj ... prevede text na velka pismena  
string wordend {Ahoj, jak se mas} 1 ... vrati index posledniho pismene slova, na ktere ukazuje index 1 (4)  
string wordstart {Ahoj, jak se mas} 1 ... vrati index prvniho pismene slova, na ktere ukazuje index 1 (0)  
string trim {Ahoj, jak se mas} ?Aash? ... oreze text na zacatku a na konci o pismena Aash az po bile znaky  
string trimleft {Ahoj, jak se mas} ?Aash? ... oreze text na zacatku o pismena Aash az po bile znaky  
string trimright {Ahoj, jak se mas} ?Aash? ... oreze text na konci o pismena Aash az po bile znaky  
regexp "jak s" {Ahoj, jak se mas} ... najde regularni vyraz v textu a vypise 1, jinak 0  
<b>seznamy</b> - specialni typy retezcu - prvky oddelene bilym znakem  

var SEZNAM [list a b c d] ... vytvoreni seznamu  
lindex $TEXT 0 ... (List index) ukaze prvek/slovo o indexu 0  
lindex $TEXT end ... ukaze posledni slovo, prvek  
llength $TEXT ... (List length) ukaze pocet slov, prvku  
lrange $SEZNAM 2 4 ... vrati 2 az 4 prvek seznamu  
lappend SEZNAM e f ... prida dalsi prvky do seznamu e a f - a b c d e f  
linsert $SEZNAM 4 x y ... vrati seznam, kde prida mezi 5. a 6. prvek prvky x y  
lreplace $SEZNAM 4 5 v w ... vrati seznam, kde se 5. a 6 prvek nahradi v a w  
lsearch -exact $SEZNAM d ... vrati index prvku, ktery odpovida zadani "d"  

lsearch -regexp $SEZNAM ah ... vrati index prvku, ktery odpovida regularnimu vyrazu "ah"  
lsort -decreasing $SEZNAM ... vrati seznam, ktery je setrizeny od nejvetsiho po nejmensi  
lsort -increasing $SEZNAM ... vrati seznam, ktery je setrizeny od nejmensiho po nejvetsi  
concat $TEXT $SEZNAM ... vrati spojeny seznam TEXT a SEZNAM  
split {ahoj:pane} ?:o? ... rozdeli text na prvky (prvky oddelene prazdnym znakem - mezerou), oddelovaci znaky : a o  
join {ahoj pane tomasi} : ... spoji prvky seznamu znakem : misto mezery = ahoj:pane:tomasi  

<b>pole</b> - je seznam, kde indexy jsou slova  

set POLE1(prvek1) hodnota1 ... definuje pole POLE1 s indexem prvek1  
array get POLE1 ... vypise vsechny prvky pole  
array exists POLE1 ... vrati 1, pokud promenna existuje a je typu pole  
array size POLE1 ... vrati pocet prvku v poli  
array names POLE1 ... vrati nazvy indexu  
array startsearch POLE1 ... zapocne prohledavani indexu pole POLE1, vrati ID prohledavani  
array nextelement POLE1 s-1-POLE1 ... vrati jmeno dalsiho indexu, pokud nejsme jeste na konci prohledavani  
array anymore POLE1 s-1-POLE1 ... vrati 1 pokud lde dal hledat, 0 pokud uz nejsou dalsi indexy  
array donesearch POLE1 ... ukonci prohledavani indexu pole POLE1, zrusi ID prohledavani  

### podminky

if  boolean  then  body1  else  body2 ... podminky  
if ![info exists a] {set a 0} else {incr a} ... podminka - pokud neexistuje promenna, definuje ji a priradi ji cislo nula. Jinak ji zvetsi  
switch  flags  value  {pat1  body1  pat2  body2  ...} ... podminka s vyberem  
switch  -exact  --  $HODNOTA  { 1  { incr(A) } 2	{ incr(A); incr(A) } default  { return A } } ... priklad podminky s vyberem  

### Cykly

foreach HODNOTA SEZNAM commandBody  

foreach num {1 3 5 7 11 13} { puts $num } ... vypise vsechna cisla  
while  booleanExpr  body  
set i 0; while {$i < 5} { puts "i is $i"; incr i} ... priklad  
for initial test final body  
set numbers {1 3 5 7 11 13}; for {set i 0} {$i < [llength $numbers]} {incr i 1} { puts "i is $i" } ... priklad for  

### Zakladni prikazy

source c:/temp/script/SKRIPT.jacl ... spusti externi skript  

eval exec ls -l ... spusti "ls -l" z shellu  
eval exec ls / > /tmp/aaa  
puts stdout {Ahoj - $text} ... vypise na obrazovku 'Ahoj - $text', neprovede se vyhodnoceni  
puts stdout "$text ma [string length $text] znaku" - Vypise obsah promenne text a pocet znaku - vyhodnoti se vyrazy  
gets stdin AAA ... nacte od promenne AAA retezec ze standardniho vstupu  
lindex  $argv  0 ... prvni parametr z volani interpreta/skriptu  
catch {expr 20 / 5} VYSLEDEK ... priradii vysledek do promenne VYSLEDEK. vrati 0  
catch {expr aaa / 5} VYSLEDEK ... priradii chybu do promenne VYSLEDEK, vrati 1  

### Prace se soubory

open /tmp/aaa w ... otevre soubor pro zapis a vrati FileID  
puts FileID aaa ... zapise do souboru FileID  
close FileID ... zavre soubor FileID  
open /tmp/aaa r ... otevre soubor pro cteni a vrati FileID  
gets FileID ... precte radek ze souboru FileID  
close FileID ... zavre soubor FileID  

### Procedury

Definice procedury\\

```
proc podil {x y} {
set vysledek [expr $x/$y]
puts $vysledek
}
```

podil 10 5 ... provede proceduru, preda argumenty 10 a 5  
global len ... nadefinuje promennou $len v procedure z globalniho globalni prostredi - lze k ni pristupovat z procedury  

====Jacl v html====

```
&lt;applet width=300 height=100 code=cornell.applet.Shell.class&gt;
&lt;param NAME="jacl.script VALUE="buttons.tcl"&gt;
&lt;/applet&gt;
```
