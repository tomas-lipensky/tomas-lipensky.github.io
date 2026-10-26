---
title: Perl
---

## Externi odkazy

[Systemove promenne](perl-promenne.html)  
[1radkovi perlici](http://www.catonmat.net/download/perl1line.txt)  
[Programujeme v PERLu - I](http://www.abclinuxu.cz/clanky/programovani/programujeme-v-perlu-i)  
[Programujeme v PERLu - II](http://www.abclinuxu.cz/clanky/programovani/programujeme-v-perlu-ii) na ABCLinuxu  
[PAR](http://search.cpan.org/~rschupp/PAR/lib/PAR/Tutorial.pod) - Perl Archive - tvoreni spustitelnych binarek na Windows a Linux  
[perl.org](http://www.perl.org/)  
[perl.com](http://www.perl.com/)  
[http://www.perlhowto.com/](http://www.perlhowto.com/)  
[ - CPAN: Comprehensive Perl Archive Network ](http://www.cpan.org/)  
[http://perldoc.perl.org/](http://perldoc.perl.org/)  
[Kniha Modern Perl](http://www.root.cz/knihy/modern-perl/)  
[Perl introduction](http://www.well.ox.ac.uk/~johnb/comp/perl/intro.htm)  
[Obsahly serial na linuxsoft.cz](http://www.linuxsoft.cz/article.php?id_article=1867)  
[Perl Best Practice](http://buhoz.net/public/books/lenguajes/perl/Perl.Best.Practices.Jul.2009.pdf)  
[Perl for Sysadmins](http://docstore.mik.ua/orelly/perl/sysadmin/)  

## Binarky perlu

perl -e 'print scalar localtime(1234567890)"\n"' ... prevede cas v sekundach do citelne podoby  
perl -e 'print crypt("mypassword","Bz");' ... Zahashuje "mypassword" pro uziti v /etc/shadow  
perl -pi -e 's/\r\n/\n/g' input.file ... prevede dosovy txt do unixoveho  
perl -e '$now=time;$then=$now-(24*60*60*60);while(&lt;&gt;){split /\s+/;(@_[7]>=$then)&& print;}'  
perl -e "print join(\"\n\", @INC);" ... ukaze cesty ke knihovnam  
pp -o skript.exe skript.pl ... vytvoreni binarky (vyzaduje balicek PAR::Packer) - balik s knihovnama, perl.exe atd. se rozbali do tempu a pak spusti  

perldoc -v '$"' ... napoveda o promenne $"  
perldoc -f printf ... napoveda o prikazu printf  
perldoc -q read ... najde "read" v FAQ perlu  
perldoc Data::Dumper ... napoveda k modulu  
perldoc -l Data::Dumper ... ukaze soubor modulu  
perldoc -m Data::Dumper ... ukaze obsah modulu  
[perl2exe](http://www.indigostar.com/perl2exe.php) ... Nastroj na kompilaci balicku a knihoven do spustitelneho souboru  
cpan -i Nagios::NRPE::Packet ... stahne a nainstaluje modul Nagios::NRPE::Packet  
PERL_MM_USE_DEFAULT=1 perl -fi PAR::Packer ... stahne a nainstaluje modul PAR::Archive bez ptani na zavislosti  
PERL_MM_USE_DEFAULT=1 perl -MCPAN -e 'install PAR::Packer' ... jina alternativa instalace CPAN modulu bez ptani  

## One liners - jednoradkace

cat last-1.xml | perl -MHTML::Entities -lne 'print decode_entities($_)' ... dekoduje HTML kodovani (apersand kodovani &apm;xxx;)

echo "12/11/2016 00:53:24"|perl -MTime::Local -lne'my ($a,$b,$c,$d,$e,$f)=split(/[\s\/:]+/, $_);my $time = timelocal($f,$e,$d,$a,$b-1,$c); print "$time";'

## Promenne

$A=1;  

$B="15kg" * "2ks"; ... vynasobi 15*2  
$C=&lt;&lt;END;  
a  
b  
END\\ ... multiradek  
$_ ... posledni vysledek, ci obsah promenne, se kterou se pracovalo  
@POLE=("a","b","c"); ... definice pole
@CISLA=(1 .. 10); ... pole cisel 1 az 10  

@ARGV ... promenne z radku  
$POLE[0],$POLE[-1]; ... prvni prvek pole (a), posledni prvek pole (c)  
@POLE2D=([1,2,3],[3,4,5],[7,8,9]); ... 2 dim pole  
print $POLE2D[1][1]; ... vypise 2. prvek 2. pole, stejne jako $POLE2D[1]->[1]  
$refNA2Dpole=[ ["a","b","c"],["d","e","f"] ] ... Reference na 2d pole  
$refNA2Dpole->[0][0] ... vrati a a je to stejne jako $refNA2Dpole->[0]->[0]  
%HASH=('A',"prvekA",'B',"prvekB"); ... definice hashe - pole, kde indexy maji nazvy  
%HASH=('A'=>"prvekA",'B'=>"prvekB");
$HASH{'A'}; ... prvek A z hashe HASH (prvekA), stejne jako $HASH->{'A'}  
defined($PROMENNA) ... vrati 1/0 jestli je promenna definovana/je typu undef  

\@POLE ... vrati adresu pameti, na ktere se nachazi pole  
\@POLE->[0] ... prvni prvek pole  

## Operatory

Numericke:  
$i=1; ... prirazeni;
$i++; ... $i=$i+1;  
$i--; ... $i=$i-1;  
$i+=10; ... $i=$i+10;  

$i-=10; ... $i=$i-10;  
$i=$i**3; ... $i=$i*$i*$i;  

Numericke (porovnani)  

&lt;, &gt; - mensí nez, vetsi nez  
<=, >= - mensi rovno, vetsi rovno  
==, != - rovno, nerovno  

Retezce (porovnání)  

= ... prirazeni hodnoty  
.= ... pridani hodnoty na konec retezce  
lt, gt - delsi nez, kratsí nez  
le, ge - delsi nebo shodné, kratsí nebo shodné  
eq, ne - shodné, neshodné  
$I=~/aaa/; vraci 0, pokud nenajde aaa v $I  
$I=~/aaa/gsi; vraci cele cislo rovnajici se poctu vyskytu znaku v retezci - jednom radku - ignoruji se velikosti pismen  

retezce:  

. - slozeni retezcu  
x - opakovani retezcu;  
= ... prirazeni  
$S =~ m/^-/ ... otestuje [regularni vyraz](http://perldoc.perl.org/perlre.html) na retezci $S  
$S=~s /a/b/s; ... nahradi v retezci $S a za b, $S bere jako jeden radek (s) pokud nic nenahradi, vraci 0  
$S=~s /a/b/im; ... nahradi vsechny a a A za v (i - ignoruje velikost), bere retezec jako vice radku (m)  
$S=~tr/seznam vyrazu/nahrazovane vyrazy/cd - zamenuje seznam vyrazu za seznam vyrau - d -k kdyz nenajde ekvivalent, vymaze vyraz  
$date =~ m/(..)\/(..)\/(....)/; $newdate = "$3,$2,$1"; ... ulozeni casti regularniho vyrazu do promenne  
$multiline_string=~ /(zacatek bloku.*?)konec bloku/s; ... viceradkovy retezec s ohranicenim  

& - bitove AND  
| - bitove OR  
&& - logicke AND  
| | - logicke OR  
|  --- |

(-D file > 30) ... vrati zda je soubor starsi 30 dni  
([-f file](http://www.cs.cf.ac.uk/Dave/PERL/node69.html) ... vrati zda je cesta soubor  

## Cykly, podminky, vlastni funkce a knihovny

for ($i=1;$i<=10;$i++) { print "$i \n"; }  

for (@seznam) { prikazy }  
for (keys %nejaky_hash) { zpracuj_aktualni_klic }  
foreach (@seznam) { print $_; } ... pro kazdy prvek z pole se provede vypis honoty  
foreach $I (%HASH) { print $I; } ... pro kazdy prvek z hashe se provede vypis honoty  
print "AHOJ" while ($AHOJ -eq "ahoj"); ... Provadi se prikaz, dokud plati podminka  
$i=-1; while ($i!=0) { $i=&lt;STDIN&gt;; } ... kdyz se $i ruzni od jenda, cti z klavesnice (standartniho vstupu) (provadi se cyklus, dokud plati podminka)  
$i=-1; until ($i==0) { $i=&lt;STDIN&gt;; } ... cti z klavesnice, dokud $i nebude rovno 0.(provadi se cyklus, pokud neplati podminka)  

print "Ahoj" if ($AHOJ==1); ... provede prikaz print, pokud je spnena podminka  
if ($i<10) { print "$i je mensí nez deset"; }  
 elsif ($i==10) { print "$i je rovno deseti"; }  
 else { print "$i je vetsí nez deset"; }  
if (-e FILE) ... jestli existuje soubor  
perldoc -f "-f" ... vsechny souborove operatory  
printf ("%s\n", (1>0) ? ("Je hezky") : ("Prsi") ); ... jiny typ podminky  
(1 &lt; 0) || print ("chyba") ... jiny typ podminky  
(0 &lt; 1) || print ("to sedi") ... jiny typ podminky  

next; ... skoci na konec podminky while, until, for  
last; ... posledni prikaz v cyklu - okamzite ukonci cyklus  
continue; ... rozdeli cyklus na casti, ktere se zvlast vykonaji pri redo a next  

redo; ... znovu zacne provadet aktualni cyklus (bez overeni podminky)  
last; ... Ukonci cyklus  
sub FUNKCE [(prototyp)] { print @_; $_; } ... definice vlastni funkce (podmodulu) FUNKCE - argumenty funkce jsou $_, funkce se pak vyvola : &amp;FUNKCE(1,2,3); Vrati seznam parametru  
&amp;FUNKCE (a, b, c) ...  volani funkce  
return [hodnota]; ... vrati hodnotu  
use jméno_modulu [[verze]seznam] ... pouziti moduku, knihovny  

## Prace s poli

grep { $_ > 4 } (1 2 3 4 5 6 7 8) ... vrati pole obsahujici cisla vetsi jak 4 (podpole puvodniho)  

@POLE=qw(1 2 3) ... do pole priradi prvky '1' '2' '3' mezera oddelujici slova je jednodussi zpusob, nez davani prvku do uvozovek  
@nadruhoy = **map** {$_ * $_} @cisla; ... kazde cislo v poli da nadruhou a vytvori druhe pole
my %zaplatil = **map** {$_ => 1} @lide; ... vytvori asociativni pole z normalniho pole, kazdy prvek z pole bude klic s hodnotou 1
print **map** { $_ =~ /a/ ? ($_) : () } (ahoj, Ahoj, AHOJ); ... vypise z pole vsechny slova, co maji v sobe male a
push(@POLE,'novy prvek') ... prida na konec pole prvek "novy provek"  
pop(@POLE) ... vrati posledni prvek z pole a smaze ho z pole  
scalar @POLE; - vrati pocet prvku pole POLE  
shift(@POLE) ... vrati prvni prvek z pole a vyjme jej z pole  
unshift(@POLE,"a") ... vlozi prvek "a" na prvni misto pole  
splice (1,2,3,4,5) , 2, 2, (7,8,9) ... za 2 prvkem smaze 2 prvky z pole a nahradi je 3 prvky na (1,2,7,8,9,5)  
@POLE2=[sort](http://perldoc.perl.org/functions/sort.html) (@POLE); ... setridit pole @POLE a priradi ho do pole @POLE2  
@POLE2=sort { $a <=> $b } 50 .. 0; ... numericke trideni  
@POLE2=sort { lc($b) cmp lc($b) } @POLE; ... setridi reverzne abecedne pole  
@POLE2=sort funkce keys %HASH ... setridi hodnoty hashe podle funkce funkce  
@INDEXY=sort { $POLE[$a] cmp $POLE[$b] } 0 .. ((scalar @POLE)-1); ... vrati indexy setrideneho pole alfanumericky  

## Prace s hashi (asociativnimi poli)

delete $HASH{'A'}; ... smaze prvek A hashe HASH  
exists $HASH{'A'}; ... zkontroluje, jestli se klic A nachází v hashi HASH  

keys %HASH; ... vrati seznam indexu seznamoveho hashe HOST, u skalarniho hashe pocet prvku  
values %HASH; ... vrati seznam vsech hodnot hashe HASH  
each(%HASH); ... vrati dvojici dalsiho zaznamu z hashe ($KLIC,$ZAZNAM)  

## Prace s retezci

chomp $I ... zmeni retezec $I - smaze novy radek na konci retezce, vrati pocet zmen  
chomp @I ... smaze konce radku v seznamu, vrati pocet zmen  
chop $i ... odzstani posledni znak v retezci, vrati pocet zmen  

chop @i ... odzstani posledni znak v kazdem prvku pole, vrati pocet zmen  
crypt("mypassword","Bz"); ... zahashuje text mypassword pomoci zakladu Bz  
lc $A; ... vraci vyraz s malymi písmeny  
lcfirst $A; ... vrací výraz, s prvnim malym pismenem  
length "afsdfasdf"; ... delka výrazu v bajtech.  
uc($A); ... vraci vyraz s velkymi pismeny  
ucfirst("fasdf"); ... vraci vyraz, s prvnim velkym pismenem  
$a=$b.$c ... spoji retezce $b a $c  
print "x" x 50, "\n"; zopakuje retezec "x" 50-krat a udela novy radek  

ord $A ... napise ASCI kod prvniho pismene retezce  
chr $cislo ... vypise znak, jehoz ASCI kod je cislo  
index(text,hledany_retezec); napise index, jakym pismenem zacina hledany_retezec v zadanem textu. -1 = nenasel  
index(text,hledany_retezec,pocatek_hledani); napise index, jakym pismenem zacina hledany_retezec v zadanem textu, zacina hledat na zanku pocatek_hledani  
rindex(text,hledany_retezec); napise index, jakym pismenem zacina hledany_retezec v zadanem textu. Hleada od prava, cili posledni vyskyt  
rindex(text,hledany_retezec,pocatek_hledani); napise index, jakym pismenem zacina hledany_retezec v zadanem textu, zacina hledat na zanku pocatek_hledani. Hleada od prava, cili posledni vyskyt  
split [vzorek[,výraz[,limit]]]; - rozd&#283;lí výraz podle zadaného vzorku, pokud je zadán limit, d&#283;lí ho na na tento maximální po&#269;et polí  

@kluci = split(/:/, "Honza:Petr:David"); ... Rozdeli retezec a jednotlive polozky da do pole @kluci  
substr(text,index_pocatku) ... vypise cast textu text od pismene s indexem index_pocatku. Pokud je index_pocatku zaporny, bere se pocet znaku od konce textu  
substr(text,index_pocatku,delka) ... vypise cast textu text od pismene s indexem index_pocatku o delce delka znaku. Pokud je index_pocatku zaporny, bere se pocet znaku od konce textu. Pokud je delka zaporna, bere se delka do konce textu, a neukaze se poslednich delka znaku  

## Prace s cisly:

abs výraz; - vrací absolutní hodnotu výrazu  
atan2 y,x; - vrací arctangens y/x v rozsahu od -pi do pi  
cos výraz; - vrací kosinus výrazu (zadávaného v radiánech)  

exp výraz; - vrací e umocn&#283;né na výraz  
int výraz; - vrací celo&#269;íselnou &#269;ást výrazu  
log výraz; - vrací p&#345;irozený logaritmus (základ = e) výrazu  
rand [výraz]; - vrací náhodné desetinné &#269;íslo z intervalu <0;výraz), pokud není výraz zadán, nahradí ho 1  
sin výraz; - vrací kosinus výrazu (zadávaného v radiánech)  
sqrt výraz; - vrací druhou odmocninu výrazu  

srand výraz; - nastavuje výchozí hodnotu pro rand  
chr výraz; - vrací znak o ASCII hodnot&#283; výrazu  
hex výraz; - p&#345;evádí hexadecimální výraz na desítkovou hodnotu  

## Cas:

time; ... vrací UNIXový &#269;as, po&#269;et sekund od 1.1.1970 8:8  

@timeData = localtime(time); ... Vrati pole (minuta hodina den mesic rok-1900 den_v_tydnu den_v_roce)  
gmtime výraz; - konvertuje unixový &#269;as na "lidský"; ve skalární souvislosti vrací &#269;as v plném tvaru (den v týdnu, m&#283;síc, den v m&#283;síci, &#269;as, rok), v seznamovém kontextu vrací tyto hodnoty rozlozené (vte&#345;ina, minuta, hodina, den, msíc, rok, den v týdnu, den v roce, letní &#269;as), m&#283;síce za&#269;ínají 0 - leden a dny v týdnu 0 - ned&#283;le  

## vstup/vystup

print "Ahoj\n"; ... tisk do vychoziho vstupu  
print STDOUT "Jak se mas\n","Dobre",$OTAZNIK; ... tisk do vystupu STDOUT  
[printf](http://perldoc.perl.org/functions/sprintf.html) ("Dobry%4s, jak %s mas? Jsou %x hodiny a %f minut.\n","den","se",4,0.33); ... formatovany tisk  
print "1 + 2 = ", 1+2, ", promenna A = \"", $A, "\n";  

open SOUBOR,"soubor.fil"; ... otevre soubor soubor.fil pro cteni  
open SOUBOR,"&gt;soubor.fil"; ... otevre soubor soubor.fil pro zapis, neexistuje-li, vytvori jej  
open SOUBOR,"&gt;&gt;soubor.fil"; ... otevre soubor soubor.fil pro pridavani na konec  

open SOUBOR,"+&lt;soubor.fil"; ... otevre soubor soubor.fil pro cteni i zapis  
open SOUBOR,"+&gt;soubor.fil"; ... bymaze obsah stareho souboru soubor.fil a otevre jej pro cteni i zapis, nebo jej vytvori  

$VSTUP=&lt;&gt;; nebo $VSTUP=&lt;STDIN&gt;; ... nacteni jednoho radku ze standartniho vstupu (klavesnice) do promenne $VSTUP  
$VSTUP=&lt;SOUBOR&gt; ... nacte promennou - jeden radek ze souboru
$VSTUP=readline(*SOUBOR); ... jina moznost nacteni radku ze vstupu  
@file=&lt;SOUBOR&gt;; ... nacte cely soubor  
print $f`ile; ... vypise cely soubor  
print SOUBOR "asfda" ... zapise do souboru  
eof(&lt;SOUBOR&gt;) ... test, zda je uz konec souboru  
[($dev,$ino,$mode,$nlink,$uid,$gid,$rdev,$size,,$atime,$mtime,$ctime,$blksize,$blocks)= stat(file)](http://stackoverflow.com/questions/509576/how-do-i-get-a-files-last-modified-time-in-perl) ... vrati pole s informacemi o souboru (inode, cas modifikace, velikost...)  

close SOUBER; ... zavre soubor  
Jiny zpusob nacteni vstupu z prikazu:

```
open(PS,"ps -e -o pid,stime,args |") || [[https://www.cs.cf.ac.uk/Dave/PERL/node111.html|die]] "Chyba: $!\n"; 
while ( &lt;PS&gt; ) { print $_ } 
```

Zpusob, jak do prikazu presmerovat vstup:

```
open(MAIL, "| /bin/mailx -s test user\@localhost ") || die "Chyba: $!\n";
print MAIL "Ahoj";
```

## Soubory/adresare

[chmod](http://perldoc.perl.org/functions/chmod.html) ... zmena prav k souboru  
[IO::Uncompress::Unzip](http://stackoverflow.com/questions/16288977/perl-reading-zip-files-with-iouncompressanyuncompress) ... unzip  
[-x -e -d -f](http://perldoc.perl.org/functions/-X.html) ... zjisti zda soubor je spustitelny, existuje, je to adresar, soubor atd.  

## Ostatni

$ENV{'PATH'} ... hodnota promenne PATH z shellu  
$ARGV[0] ... prvni hodnota argumentu z volani funkce  
system("ls -l /"); = system("ls","-l","/"); ... spusti prikaz ls v operacnim systemu, vrati return code do promenne $?  
$VYSTUP=`command arg1 arg2`; ... jiny zpusob spusteni prikazu, vystup vrati do promenne $VYSTUP  
@VYSTUP=system("ls -l / 2> &amp;1"); ... spusti prikaz, vystup i chyby se ulozi do pole  
open(PS,"ps -ef |"); while ( &lt;PS&gt; ) { } ... spusti program, vystup jde do perloveho skriptu  
exec("cp", "*", "/"); spusti program prikaz "cp * /" a ukonci program (pokud program existuje)  
sleep 60; ... pocka 60 sekund  

## Moduly

use lib 'directory'; ... prida cestu do @INC, kde hleda knihovny  
PERL5LIB=$PERL5LIB:. ... prida cestu do @INC, kde perl hleda knihovny  
[Filesys::Diskspace](http://search.cpan.org/~ftassin/Filesys-DiskSpace-0.05/lib/Filesys/DiskSpace.pm) a [pouziti](http://www.cyberciti.biz/tips/howto-write-perl-script-to-monitor-disk-space.html)  
[IO::Socket](io-socket.html) ... modul pro TCP/IP komunikaci  

[Parallel::ForkManager](parallel-forkmanager.html) ... paralelni zpracovani  
[Term::ANSIColor](term-ansicolor.html) ... barevny vystup na konzolu  
[Proc-ProcessTable](http://search.cpan.org/~durist/Proc-ProcessTable/) ... prace s procesama pod Unixy - je potreba kompilace systemove knihovny  
[Sys-Filesystem](http://search.cpan.org/~rehsack/Sys-Filesystem/) ... Prohlizeni parametru filesystemu  
[Sys-Df](http://search.cpan.org/~iguthrie/Filesys-Df/) ... Pristup ke statistikam filesystemu - kapacita, vyuziti atd. - je potreba kompilace systemove knihovny  
[WWW:Mechanize FAQ](http://search.cpan.org/dist/WWW-Mechanize/lib/WWW/Mechanize/FAQ.pod) ... nastroj na ziskavani WWW obsahu, prace s formulari atd.. [jednoduchy priklad na zobrazovani nazvu poli z formularu](http://stackoverflow.com/questions/16701287/perl-mechanize-print-html-form-names)  
[WWW:Mechanize](http://search.cpan.org/~ether/WWW-Mechanize-1.73/lib/WWW/Mechanize.pm) a [priklady pro zacatecniky](http://stackoverflow.com/questions/4241129/tiny-runable-wwwmechanize-examples-for-the-beginner)  
[Excel::Writer::XLSX](http://perlmaven.com/create-an-excel-file-with-perl)  
[DBD::WMI](http://search.cpan.org/dist/DBD-WMI/lib/DBD/WMI.pm) - Pristupovani k Windows objektum pomoci Windows Query Language.  
[Pod](http://perldoc.perl.org/perlpod.html) - Perl Old Documentation, [POD in 5 minutes](http://www.perlmonks.org/?node_id=252477)  
[Smart::Comments](http://search.cpan.org/~neilb/Smart-Comments-1.06/lib/Smart/Comments.pm) ... chytre komentare pro debugovani, zobrazi treba promenne, progress bar atd.  
[HTML::Entities](https://metacpan.org/pod/HTML::Entities) ... prace s html kodovanim a dekodovani (&eacute; napr.)  
Win32::Console::ANSI ... umozni pouzivani Term:ANSIColor na Windows  
[Win32::OLE](http://search.cpan.org/~jdb/Win32-OLE-0.1709/lib/Win32/OLE.pm) ... Umoznuje pod Windows pouzivat OLE (Object Linking and Embedding)  
use feature qw(switch) ... umozni uziti funkce: given ($A) { when(1) {} default {} } - nahrazka neexistujici podminky case
