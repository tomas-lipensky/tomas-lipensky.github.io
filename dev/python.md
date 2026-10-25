# Python / Jython

Jython je iplementace Pythonu cela napsana v Jave.

### Externi odkazy

[U&#269;íme se programovat v jazyce Python](http://howto.py.cz/index.htm)  
[Python a Qt 1 (Uvod)](http://www.abclinuxu.cz/clanky/programovani/python-a-pyqt-1-uvod) na ABCLinuxu  
[Python a PyQt - 2 (podmínky, cykly, tla&#269;ítka)](http://www.abclinuxu.cz/clanky/programovani/python-a-pyqt-2-podminky-cykly-tlacitka) na ABCLinuxu  

[Python a Qt 3](http://www.abclinuxu.cz/clanky/programovani/python-a-pyqt-3) na ABCLinuxu  
[Standardni knihovna pro Python](http://www.abclinuxu.cz/serialy/standardni-knihovna-pro-python) - Odkazy na nasledujici dily serialu  
[1 - builtins 1](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-1-builtins-1)  
[2 - builtins 1](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-2-builtins-2)  
[3 - builtins 1](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-3-builtins-3)  
[4 - builtins 1](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-4-builtins-4)  
[5 - retezce 1](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-5-retezce-1)  

[6 - retezce 2](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-6-retezce-2)  
[7 - retezce 3](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-7-retezce-3)  
[8 - Regularni vyrazy](http://www.abclinuxu.cz/clanky/programovani/standardni-knihovna-pro-python-8-regularni-vyrazy-1)  
[py.cz](http://py.cz/) - &#268;eský informa&#269;ní rozcestník  
[Jython na IBM](http://publib.boulder.ibm.com/infocenter/wsdoc400/v6r0/index.jsp?topic=/com.ibm.websphere.iseries.doc/info/ae/ae/rxml_commandline.html)  
[Kniha Ucebnice jazyka Python](http://www.root.cz/knihy/ucebnice-jazyka-python/)  
[Kniha Dive into Pyhton](http://www.root.cz/knihy/dive-into-python/)  

[Kniha Think Pyhton](http://www.root.cz/knihy/think-python/)  
[Kniha Ponorme se do Pyhtonu 3](http://www.root.cz/knihy/ponorme-se-do-pythonu-3/)  
[Prima serial o Pythonu na sallyx.org](http://www.sallyx.org/sally/python/)  

[WebSphere Application Server](../was/was.html) Jython prikazy  
[Quickly](http://wiki.ubuntu.com/quickly) - vyvojovy nastroj na jednoduchou a rychlou tvorbu grafickeho prostredi GTK pro Pyhton  

### Prikazy

python ... spusti interaktivni prekladac  
python -c 'print "Ahoj"' ... spusti prikaz  
python soubor.py ... spustu soubor v pythonu  
pydoc string ... popis knihovny string
pydoc -p 82 ... spusti http server na portu 82 s napovedou k pythonu  
jython ... spusti interaktivni prekladac Jythonu  
echo 'toydi deified idiot' | python -c "print raw_input()[::-1]"

### Virtualni prostredi + instalace doplnku mitmproxy pro VP

sudo yum install python-virtualenv  
virtualenv -p /usr/local/bin/python2.7 ~/Desktop/mitmproxy  
cd ~/Desktop/mitmproxy  
. bin/activate  
python -m venv ADRESAR ... vytvoří virtuální prostředí my_project_env  
source ADRESAR/bin/activate ... aktivuje virtuální prostředí  
pip install mitmproxy ... nainstaluje balíček mitmproxy - buď globálně, nebo do aktivovaného virtuálního prostředí  
python3 -m pip install -r requirements.txt ... instalace z **requirement.txt** souboru  
%%python3.12 -m pip install --user ddgs==1.2%% ... jiný způsob na instalaci balíčku, jen pro daného uživatele  
[pipx](https://github.com/pypa/pipx) install pycowsay ... nainstaluje lokálně pro daný adresář knihovnu (nemusí se používat venv)  
pipx list ... seznam nainstalovaných knihoven  
pipx run skript parametry ... spustí python aplikaci s parametrama a nainstalovanýma knihovnama  
[uv](https://pypi.org/project/uv/) ... jeden nástroj na nahrazení pip, poetry, pyenv, twine, virtualenv  

### Moduly

Moduly se dají stáhnout na [pipy](https://pypi.org/), nebo např. githubu

[boto3](https://pypi.org/project/boto3/) ... AWS SDK  

### Promenne a prace s nimi

isinstance(PROMENNA, str) ... vrati True/False, jestli je PROMENNA typu string. typy promennych: int, long, long, complex,
str, unicode, list, tuple, type(object)  
global x ... definovani globalni promenne (definovana i z funkci atd.  
type(AAA) ... vrati typ promenne AAA, napriklad &lt;type 'int'&gt;  
del a[2:] ... smaze vsechny prvky od druheho prvku seznamu  
del (AAA) ... smaze (oddefinuje) promennou AAA  
_ ... predchozi promenna  
AAA is 1 ... vrati True, pokud AAA je cislo  
AAA is not [] ... vrati true, pokud AAA neni 0 prvkove pole  

#### Retezec

TEXT = "ahoj %20s" % 'Franto' + ' jak se mas' ... definice promenne, doplni se do 20 znaku text (ci promenna) za procentama  
TEXT1,TEXT2="Ahoj, mam %1.2f \"penez\" na %i lizatka" % (1.2,2) ,"Cau %2i lidi" % 2 ... definice 2 retezcu naraz  
TEXT[1] ... druhe pismeno retezce  
TEXT[-1] ... posledni pismeno retezce  
TEXT[1:3] ... druhe az ctvrte pismeno  
TEXT[1:] ... druhe az posledni pismeno  

TEXT[:-2] ... napise cely retezec krome poslednich 2 pismen  
TEXT = """ "Ahoj" rekla.  
"Ahoj" odpovedel """ ... uvnitr trojitych uvozovek (slozenych i jednoduchych, se mohou vyskytovat uvozovky i konce radku  
TEXT=r'ahoj\n' ... \n se neprelozi jako novy radek  
UNICODE=u'ahoj\u0020cau' ... unicode retezec  
TEXT="Ahoj %(jmeno)s, uz jsme %(poradi)i"%zaznam ... vlozi zaznamy ze slovniku (hashe)  
TEXT2 = TEXT + " pane" ... spoji retezce, pokud se jedna o retezce  
TEXT3 = TEXT * 3 ... znasobi (zopakuje) se text 3x za sebou  
TEXT="Jmeno %10s, vek %-5d, vaha %f" % ("Tomas", 30, 75.3) ... formatovani retezce, Tomas na 10 znaku, zarovna z prava, 30 na 5 znaku, zarovna zleva  

TEXT1 > TEXT1 ... vyhodnoceni uzporadani textu  
TEXT1 < TEXT1 ... vyhodnoceni uzporadani textu  
TEXT1 == TEXT2 ... shodnost textu  
'a' not in TEXT ... vyhodnoceni, zda neni pismeno 'a' obsazeno v retezci  
len('ahoj') ... delka retezce  
str(32) ... prevede na retezec  
repr(32) ... prevede na strojovy retezec (zapouzdreny uvozovkama)  
u"á".encode('utf-8') ... prekoduje unicode do utf-8  

TTEXT=str([1, 2, "text"])+TEXT ... prevede seznam na text a slouci jej s promennou TEXT  
string.upper("ahoj") ... prevede na velka pismena AHOJ  
string.capitalize("ahoj") ... prevede na prvni velke pismeno Ahoj  
string.capwords("ahoj pane") ... prvni pismena budou velka: Ahoj Pane  
string.center("Ahoj") ... zarovna text na prostredek radku  
string.rjust("text", 10) ... zarovna text zprava tak aby mel 10 znaku  
string.ljust("text", 10) ... zarovna text zleva tak aby mel 10 znaku  
string.zfill('-2',5) ... doplni cislo nulami na 5 pozic
TEXT.split() ... rozdeli retezec na pole, oddelovac mezera  
TEXT.split("\n") ... rozdeli retezec na pole, oddelovac novy radel  

TEXT.rstrip() ... odstrani windowsowsky "\r"  
TEST.strip() ... oraze prazde znaky ze zacatku i konce textu  
TEXT.find("podtext") ... najde pozici vyskytu retezce podtext v retezci TEXT, jinak -1  
TEXT.startswith("aaa") ... vrati true, pokud retezec TEXT zacina "aaa"  
ord('a') ... napise asci cislo znaku a  
chr(65) ... napise znak o asci 65  
"AHOJ".lower() ... prevede na mala pismena "ahoj"  

#### pole (seznam, array)

a=[1,2,3,'ctyri'] ... definice pole  
a[2:]=[] ... 2. az posledni prvek pole se odstrani  
a[0:5]=1 ... prvnich 5 prvku se nahradi prvkem 1  
a[:0]=2 ... prida 2 na konec seznamu  
a[-1] ... posledni prvek pole  
a[:] ... cely seznam  
"aa" in B ... vrati true, pokud "aa" je prvkem seznamu  
range(65, 71) ... udela pole o cislech 65 - 71  
[filter](http://docs.python.org/library/functions.html#filter)(funkce, pole) ... vystup jsou prvky pole, ktere po dosazeni do funckce vrati True  

map(abs, range(0,5)) ... vrati pole, sestavajici se z navratovych hodnot funkce abs z pole range(0,5)  
reduce(funkce, seznam) ... na dvojici ze seznamu aplikuje funkci. Na vysledek a dalsi prvek aplikuje funkci ..  
[ x*x for x in range(4) ] ... vrati seznam druhych mocnin z cisel 0 .. 4  
[ x*x for x in range(4) if x > 2 ] ... vrati seznam druhych mocnin z cisel 0 .. 4, pokud jsou vetsi nez 2  
1 in a ... vyhodnoti, zda je 1 obsazen v poli a  
b=list("Ahoj") ... prevede retezec na pole  
a+b ... slouci pole a a b  
a.append(6) ... prida 6 na konec pole  
a.count('b') ... spocita pocet vyskytu 'b'  

a.extend([1,2,3,4]) ... (to same jako a[len(a):]=[1,2,3,4]) prida na fkonec pole dalsi prvky  
a.index(3) ... napise, ktery index pole obsahuje cislo 3  
a.index('a') ... napise, ktery index pole obsahuje pismeno a  
a.insert(1, 'b') ... prida na 2. pozici prvek 'b'  
a.pop(2) ... odebere 2. prvek v poli a vrati jej jako vystup. Pokud neni argument, vrati posledni  
a.remove(1) ... odebere ze seznamu prvni vyskyt 1  
a.reverse() ... prehodi poradi prvku pole  
a.sort() ... setridi pole  

#### Slovnik (Asociativni pole, hash)

HASH={} ... definice prazdneho slovniku  
CLOVEK={'jmeno': 'Tomas','vek': 30} ... definice slovniku  
print CLOVEK['jmeno'] ... vypis prvku ze slovniku  
CLOVEK['pohlavi']="muz" ... novy provek  
keys() ... rati vsechny klice slovniku  
has_key(x) ... vrati pravda/nepravda, pokud je x klic slovniku  

#### cislo

CISLO = 7 / 2 ... celociselne deleni  
CISLE = 7 % 2 ... modulo po celociselnem deleni  
CISLO= 3.13%%**%%2 ... 3.13 na druhou  
a += 1 ... stejne jako a = a + 1  
a < b <= 3 ... retezeni podminek  
int(3.14) ... prevede text (cislo) na celociselnou hodnotu  

float(2) ... prevede cislo na realne cislo  
hes(100) ... prevede cislo do 16-kove soustavy  
abs(-5) ... absolutni hodnota  
sqrt(4) ... odmocnina  
pow(2,3) ... (power) 3-ti mocnina ze 2  
max(1,2,3,4,5) ... maximum  
min(1,2,3,4,5) ... minimum  
round(3.1444,2) ... zaokrouhleni na 2 desetinna mista  

#### Logicke promenne

not ( 1 == 1 ) ... negace => false  
1 == 1 ... rovnost = True  
1 > 2 ... vetsi nez = False  
2 < 1 ... mensi nez  
1 != 1 ... nerovno  
2 >= 1 ... vetsi nebo rovno  

2 <= 1 ... mensi nebo rovno  
1 == 2 or 1 < 2 ... nebo  
1 == 2 and 1 < 2 ... a  
bool(1) ... prevede na True  

### Podminky, cykly a funkce try

pass ... prazdne telo pro if/while/for napr. pro testovaci ucely  

break ... skoci na konec smycky (napr. while ci for)  
continue ... skoci na zacatek smycky  

Podminene provedeni prikaz:  
Jednoducha prazdna podminka - splnena vzdy, nic se neprovede:

```
if True:
 pass
```

Dvojita podminka:

```
if (a < 10):
 prikazy
else:
 prikazy
```

trojita podminka:

```
if VYRAZ:
 prikazy
elif VYRAZ2:
 prikazy
else:
 prikazy
```

Cyklus While:

```
while VYRAZ:
    prikazy
```

Cyklus While-else, dokud je splnena pokminka, prikazy1, pote prikazy2:

```
while VYRAZ:
    prikazy1
else:
    prikazy2
```

Cyklus For, priradi postupne do promenne i jednotlive prvky pole:

```
For i in pole:
    prikazy
```

for i in range(5) ... provede kroky pro 1, 2, 3, 4, 5  

Cyklus For-else, priradi postupne do promenne i jednotlive prvky pole a provede s nimi prikazy1, pote prikazy2:

```
For i in pole:
    prikazy1
else:
    prikazy2
```

Try-except - provede prikazy1, pokud se nepovede z jakehokoli duvodu, neukonci program ale provede prikazy2. Nepovinne finally bude provedeno v kazdem pripade. Slouzi napriklad na korektni uzavreni otevrenych veci.

```
try:
    prikazy1
except:
    prikazy2
finally:
    prikazy3
```

except ValueError: ... kdyz je chyba hodnoty  

except NameError: ... kdyz je chyba nazbu promenne  
except ZeroDivisoinError: ... kdyz je deleni nulou  
except (ValueError, IOError): ... kdyz je chyba hodnoty, nebo vstupu  
except (TypeError, RuntimeError): ... kdyz je chybny typ promenne, nebo Runtime chyba  
raise NameError, "Informace k vyjimce" ... vyvolani vyjimky daneho typu  

Vlastni vyjimky:

```
class MyError(Exception):
  def __init__(self), value):
    self.value = value
  def __str__(self):
    return 'self.value'
try:
  raise MyError(2*2)
except MyError, e:
   print "Vyjimka MyError s hodnnotuu: ', e.value
```

### Zakladni prikazy

# komentar ... komentar, bud na samostatnem radku, ci za prikazem  
print "Ahoj \t Nazdar" ... tisk na obrazovku, \t tabulator  
print "Ahoj %-10s, mam %d kluky." % "Ivane", 3 ... formatovani tisku  
print('Poslední pismeno "{}"'.format("pismeno"[-1])) ... formátování, napíše poslení písmenu z textu  
sys.stdout.write("Hello World!\n") ... Dalsi tisk na obrazovku  
type(PROMENNA) ... napise typ promenne  
TEXT=raw_input("Napis neco: ") ... vstup z klavesnice  
TEXT=input("Napis neco: ") ... vstup z klavesnice  
cislo=int(input("Napiš číslo: ")) ... vstup z klávesnice, převede na číslo  
sys.exit (1) ... ukonci program a vrati hodnotu 1  

### Prace se soubory

file2 = open (/home/a/b.txt, 'w') ... otevre soubor pro zapis. Pokud existuje, prepise jej  
file2 = open (/home/a/b.txt, 'a') ... otevre soubor pro zapis. Pokud existuje, zapisuje na konec souboru  
file2.write("Ahoj\nCau") ... zapise do souboru 2 radky: Ahoj a Cau  
file2.close() ... zavre soubor  
file = open (/home/a/a.txt, 'r') ... otevere soubor /home/a/a.txt na cteni  
print file ... napise jmeno souboru a jeho mod otevreni  
text = file.read() ... precte cely soubor  

text = file.read(5) ... precte 5 znaku z radku souboru  
text = file.readline() ... precte radek ze souboru  
text = file.readlines() ... precte vsechny zbyvajici radky  
for i in file: ... precte vsechny radky souboru  
file.tell() ... vrati aktualni pozici v souboru  
file.seek(3) ... bez na 3 znak v soubopru  
file.seek(-3,2) ... bez na 3 znak od koncr souboru (druhy argument 2 - konec souboru, 0 zacateksouboru, 1 aktualni pozice)  
pickle.dump(x,file) ... z balicku pickle - ulozi datovou struktoru do souboru  
pickle.load(file) ... z balicku pickle - nace datove struktory ze souboru  

### Definice funkci a importovani funkci z knihoven

execfile('c:/temp/script/testFunctions.py') ... spusti jiny python script  
import [sys](http://docs.python.org/library/sys.html) ... importute knihovnu sys, ktera umoznuje pristup k nekterym promennym interpretu python  
dir(sys) ... vylistuje funkce, promenne atd. z importovane knihovny sys  
dir(**boiltin**) ... vylistuje vestavenne obekty, bylo li importovano **builtin**  
sys.path.append('/cesta/ke/knihovnam') ... prida cestu k me knihovne  
import [string](http://docs.python.org/library/string.html) ... import funkci z knihovny string - viz sekce o retezcich  

import [os](http://docs.python.org/library/os.html) ... knihovna umoznujici vyuzivat moznosti OS (promenne prostredi atd.)  
import [command](http://docs.python.org/library/commands.html) ... knihovna pro praci s prikazovou radkou  
import [math](http://docs.python.org/library/math.html) ... importovani matematickych funkci a konstant  
import adresar.knihovna ... importuje knihovna.py z podadresare z cesty. Adresar musi obsahovat soubor **init**.py - i prazdny  

from adresar.soubor1 import * .... naimportuje ze souboru soubor1.py vsechny funkce, nemusi se pak spoustet adresar.soubor1.funkce, ale jen funkce  
from adresar import soubor ... funkce se spousti soubor.funkce()  
os.path.isfile("aaa.py") ... vrati true/false, pokud  aaa.py je soubor  
os.environ.get("PATH") ... nacte systemovou promennou PATH  
import [sys](http://docs.python.org/library/sys.html) ... knihovna, umoznujici pristup k nekterym promennym interpretu python  
sys.getdefaultencoding() ... ziska defaultni kodovani znaku  
import java.lang.System as system ... importuje funkce z knihovny java.lang.System a budo se referencovat jako system (napr. system.getProperty() )  

import java.util as util  
import java.io as javaio  
dir(string) ... seznam funkci v knihovne string  
type(string.count) ... napise typ prvku(funkce) count z knihovny string  
print string.find.**doc** ... napise popis funkce find z knihovny string  
print string.find.**name** ... vrati jmeno funkce  
return ... ukonci okamzite funkci  
return 0 ... ukonci funkci a vrati 0;  

definice funkce, nasleduji radky funkce zacinajici min. 1 prazdnym znakem. Prikazy funkce jsou vsechny radky se stejnym odsazenim (doporucuji se min 4 mezery), parametr2 nepovinny:

```
def FUNKCE1 (parametr1, parametr2=0):
    """Dokumentacni retezec"""
    prikazy
```

def FUNKCE2 (*parametry): for a in parametru: print parametry ... definice funkce s variabilnim poctem parametru  
def FUNKCE3 (**aspole): for  i in aspole.keys(): print i, " : ", aspole[i] ... Definice funkce s asociativnim polem  
FUNKCE1(parametr1=1, parametr2=2) ... volani funkce se jmeny parametru  
print FUNKCE1.**doc**
FUNKCE2(1,3,5,6) ... volani funkce  
FUNKCE3(a="pismeno A", b="pismeno B")  
soucet = lambda a,b: a+b ... definice "kratke", nebo tez "lambda" funkce  

### Modul [sys](http://docs.python.org/library/sys.html)

AAA=sys.argv[0] ... prvni argument z volaniprogramu  
len(sys.argv) ... pocet argumentu  
sys.platform ... ukaze OS  
sys.version ... verze OS  
sys.path ... ukaze cesty  

### Modul [os](http://docs.python.org/library/os.html)

os.path.exists("/bbb/aaa") ... vrati true, pokud soubor/adresar existuje  
os.path.isfile('/a.txt') ... vrati true, pokud soubor existuje  
os.environ.get('PATH") ... vrati obsach promenne prostredi  

### Modul java.lang.System - jython

system.getProperty('line.separator') ... ziska hodnotu promenne line.separator  

### Modul java.io - jython

propsfile = java.io.FileInputStream("./properties.conf") ... Udela ukazatel na soubor  

### Modul java.util - jython

props = java.util.Properties() ... definice promenne prop jako javovskeho objektu s nastavenim  
props.load(propsfile) ... nacte soubor s ukazatele a objektu typu A=B jsou jako objekty  
print props.getProperty("A") ... vypise hodnotu A  

### Modul [re](http://docs.python.org/library/re.html)

Prace s regularnimi vyrazy  

### Modul [string](http://docs.python.org/library/string.html)

Prace s retezci  

### knihovna pexpect

ssh = pexpect.spawn ('ssh -i /home/a/key user@server') ... definice prikazu, odesle prikaz, ceka odezvu  
ssh.expect (['Password:','password:']) ... pokud odezva obsahuje password nebo Password
ssh.sendline ('heslo') ... odesle se heslo  
ssh sendline ('uname -n') ... odesle prikaz uname -n  
ssh.interact ... prepne do interaktivniho modu  

### knihovna time

time.sleep(60) ... pocka 60 sekund  

====Grafika====

```
from gasp import *
begin_graphics()
Circle((200, 200), 60) ... Circle instance at (200, 200) with radius 60
Line((100, 400), (580, 200)) ... Line instance from (100, 400) to (590, 250)
Box((400, 350), 120, 100) ... Box instance at (400, 350) with width 120 and height 100
end_graphics()
```

====Tridy====

```
class Pes:
    "Popis tridy vyvolany Dog.__doc__"
    rasa="krizenec"
    def __init__(self, stek):
        self.stek = stek
        return
    
    def stekni(self):
        print self.stek
        return

    def neznamy_clovek(self, pocet_steku):
        for i in range(pocet_steku):
            print self.stek
        return

fido = Pes("Haf haf\n")
fido.stekni()
print fido.rasa
fido.stek="Hau\n"
kolemjdouci=fido.neznamy_clovek
kolemjdouci(5)
```

Dedicnost:

```
class Pes_vyje(Pes):
    def __init__(self,stek, vyti):
        Pes._init__.(self,stek)
        self.vyti=vyti

    def stekni(self):
        Pes.stekni(self)

    def zavyj(self):
        print self.vyti
        return 1
```

isinstance(fido, Pes) ... vrati 1 pokud je fido instanci tridy Pes, 0 kdyz neni  

### Google App Engine

Pro vyvoj Pythonovych aplikaci pro Google App Engine je potreba tvorit skripty v Python 2.5. Idealni je tvorit koncpterm MVC (Model - View - Controler) jak je ukazano nize. View je html vzor, Model je datova struktura, Controler je logika v py.
Aplikace se da otestovat lokalne pomoci python2.5. Pro vyvoj se doporucuje [App Engine SDK](http://code.google.com/appengine/downloads.html) (Eclipse with plugins), ktery umoznuje nahravani aplikaci na Google cloud. Databaze jsou omezene 1000 radky, tak existuje omezeni na pocet shlednuti aplikace za casovou jednotku.

mkdir -p ~/myapp/templates  
vi ~/myapp/[app.yaml](google-myapp/app.yaml)
vi ~/myapp/[myappDB.py](google-myapp/myappDB.py)
vi ~/myapp/[myapp.py](google-myapp/myapp.py)
vi ~/myapp/templates/[index.html](google-myapp/index.html)
vi ~/myapp/templates/[comment.html](google-myapp/comment.html)
vi ~/myapp/templates/[comments.html](google-myapp/comments.html)
