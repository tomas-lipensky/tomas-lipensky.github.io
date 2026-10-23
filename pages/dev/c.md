### C#

apt install dotnet-runtime-3.1  
apt install dotnet-sdk-3.1  
dotnet new console ... vytvory Hello world program  
[dotnet new classlib](https://docs.microsoft.com/cs-cz/dotnet/core/tutorials/library-with-visual-studio-code) -n "MyTestNuGetLibrary" ... vytvori prazdnou knihovnu  
dotnet build ... zkompiluje projekt definovany v csproj\
dotnet pack --interactive ... Vytvori NuGet balicek, interactive je pro nahrani do Artefakt repozitare pro autorizaci  

### Kompilace

##### Kompilace s pouzitim staticke knihovny

gcc -c knih1.c; gcc -c knih2.c ... kompilace knih1 a knih2. Vytvori se objektove soubory knih1.o a knih2.o ve formatu ELF  
ar rcs libkinh.a knih1.o knih2.o ... zabali staticke knihovny (objektove soubory) do archivu knihoven  
export LIBRARY_PATH=~/lib;$LIBRARY_PATH ... nastavi cesty k objektum, ktere se hledaji behem kompilace  
export CPATH=~/include;$CPATH ... nastavy cesty k hlavickovym souborum, ktere se hledaji behem kompilace  
export C_INCLUDE_PATH=~/include;$C_INCLUDE_PATH ... jako CPATH  
export CPLUS_INCLUDE_PATH=~/include;$C_INCLUDE_PATH ... jako CPATH, ale pro C++  
#include "knih" ... deklarace knihovny libknih.a v kodu aplikace app.c  
gcc -o app app.c -lknih ... kompilace aplikace app.c, vystupni soubor app, prilinkuje se knihovna libknih (dynamicke knihovny maji prednost)  
gcc -o app app.c -L~/lib -I~/include -lknih ... kompilace, kde zadavam cesty k objektum (pokud neni zadana cesta v LIBRARY_PATH) a k hlavickam (pokud neni zadana v CPATH)  

##### Kompilace s pouzitim dynamicke knihovny

gcc -fPIC -g -Wall -c knih3.c ... kompilace knihovny do objektu (knih3.o), s dynamickym adresovanim pameti (fPIC - Position Independent Code), ukaze Warningy (Wall) a debugovani informace (g)  
gcc -shared -W1,-soname,libknih.so.1 -o libknih.so.1.0.1 knih3.o knih4.o ... vytvori dybamickou knihovnu (Shared Objects), se SOName libknih.so.1, obsahujici objekty knih3.o a knih4.o  
gcc -o app app.c -l knih ... kompilace aplikace app s prilinkovanim dynamicke knihovny  
gcc -o app app.c ./libknih.so.1 ... kompilace aplikace app s prilinkovanim dynamicke knihovny, cesta ke knihovne zadana z prikazu  

prace s knihovnama na Unixu/Linuxu, viz. [Unixovy prikazy - knihovny](../os/unix-commands.html).

##### Kompilace na AIXu

Kompilace C programu na AIXu neni primocara v tom, ze AIX se standartne nedodava s C prekladacem. Existuji 2 moznosti:

* [gcc](http://www.bullfreeware.com/downloaded_50.php) ... GNU prekladac s tim, ze je problem s linkovanim s knihovnama dodavanyma s AIXem zkompilovych pod original prekladacem. Ale na male projekty to lze pouzit
* zakoupit vyvojove prostredi obsahujici original cc_r
* stahnou evaluation verzi vyvojoveho prostredi [XL C/C++](https://www14.software.ibm.com/webapp/iwm/web/reg/download.do?source=swg-xlcaix101&S_PKG=aix&lang=en_US&cp=UTF-8) nebo Visualage C, jejiz soucasti je i balicek s cc_r, viz [info](http://www.ibm.com/developerworks/forums/thread.jspa?threadID=166589)

#### Programovaci jazyk C

Odkaz na ucebni texty [Ing. Jana Kucery](http://www.fi.muni.cz/usr/jkucera) (FI) na C a C++  

##### Navrh algoritmu

<!--blud1.c+blud1.h+bl.tbl
blud3.c+dynamic.h+bl.tbl
blud4.c - Bludiste4+bl.tbl
blud5.c+dynamic.h+bl.tbl
cest.c+dynamic.h+bl.tbl
djikstr.c - Djikstruv algoritmus
fronta.c+fronta.h
fronta1.c+fronta1.h
fronta2.c+fronta2.h
fronta3.c+fronta3.h
hloubka.c+hloubka.h+zasobnik.c
jakob.c+jakob.h
jakoba.c+jakob.h+fronta.h
pole.c+inout.h - Pole1 program vytvati frontu cisel chovajici se jak pole
sirka.c+fronta.h - Sirka - Prohledavani bludiste do sirky
slova1a.c+slova1.h - Slova1 program pocita cetnost zadanych slov, pouziva jednosmernou frontu
slova1.c+dyn1.h - Slova1 program pocita cetnost zadanych slov, pouziva jednosmernou frontu
slova2.c+dyn2.h - Slova2 program pocita cetnost zadanych slov, pouziva obousmernou frontu
sort.c+sort.h - Setridi cisla
zasobnik.c+zasobnik.h-->

[popis souboru](naval/popis.txt)  
[blud1.c](naval/blud1.c)+[bl.tbl](c/naval/bl.tbl) - Bludiste1 - program po zadani bludiste najde cestu ven  
[blud3.c](naval/blud3.c) - Bludiste3 - Dijsk. algoritmus na zjisteni nejkratsi cesty z mistnosti  
[blud4.c](naval/blud4.c) - Warshaluv algoritmus na zjisteni cesty ven z bludiste  
[blud5.c](naval/blud5.c) - Bludiste4 - Floyduv algoritmus na zjisteni cesty ven z bludiste  
[cest.c](naval/cest.c) - Cestujici - Heuristicke vyreseni problemu obchodniho cestujiciho  
[dyn1.h](naval/cyn1.h), [dyn2.h](naval/dyn2.h)  
[dynamic.h](naval/dynamic.h)  
[fronta.c](naval/fronta.c)+[fronta.h](naval/fronta.h) - Fronta - program na vkladani cisel do fronty  
[fronta1.c](naval/fronta1.c)+[fronta1.h](naval/fronta1.h) - Fronta - program na vkladani cisel do fronty  
[fronta2.c](naval/fronta2.c)+[fronta2.h](naval/fronta2.h) - Fronta2 - program vytvari jednosmernou frontu cisel  
[fronta3.c](naval/fronta3.c)+[fronta3.h](naval/fronta3.h) - Fronta3 - program vytvari obousmernou frontu cisel  
[hloubka.c](naval/hloubka.c), [inout.h](naval/inout.h) - Hloubka - Prohledavani bludiste do hloubky''
[jakob.c](naval/jakob.c)+[jakob.h](naval/jakob.h) - Jakob program resi jakobuv problem, jak se rozpocitati, aby Jakob zbyl jako posledni  
[jakoba.c](naval/jakoba.c), [pole1.c](naval/pole1.c) - Jakob program resi jakobuv problem, jak se rozpocitati, aby Jakob zbyl jako posledni  
[sirka.c](naval/sirka.c), [slova1.c](naval/slova1.c)+[slova1.h](naval/slova1.h), [slova2.c](naval/slova2.c)  
[slova2a.c](naval/slova2a.c), [sort.c](naval/sort.c)+[sort.h](naval/sort.h)  
[zasobnik.c](naval/zasobnik.c)+[zasobnik.h](naval/zasobnik.h) - Zasobnik - program na vkladani cisel do zasobniku  

##### Uvod do jazyka C

[cisla.c](cvic3/cisla.c),
[znaky.c](cvic3/znaky.c),
[polygon.c](cvic4/polygon.c),
[primky.c](cvic5/primky.c),
[prevod.c](cvic6/prevod.c),
[jakyden.c](cvic7/jakyden.c),
[vek.c](cvic8/vek.c),
[sifra.c](cvic9/sifra.c),
[vzdalenosti.c](cvic10/vzdalenosti.c),
[osmerka.c](cvic11/osmerka.c)

[Moznost si zaprogramovat zajimavou ulohu](http://3537.cz/) a ziskat tricko, nebo i praci
