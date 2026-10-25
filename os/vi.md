# vi

[Souhrn ovladani](http://lagmonster.org/docs/vi.html)  

[viemu](http://www.viemu.com/vi-vim-cheat-sheet.gif) ... cheatsheet s ovladanim vi  

## EDITACE

Y, yy, :y, y$ ... aktualni radek do schranky  
y3l ... 3 pismena do schranky
p ... vlozit ze schranky za  
P ... vlozit ze schranky pred  
u ... undo  
ctrl-r ... redo  
D, dd, ... smazat cely radek
d3d ... smazat 3 radky
J ... spoji radek s nasledujicim  
x ... smaze jeden znak dozadu  
X ... smaze 1 znak pred kurzorem (backspace)  

## POHYBY V SOUBORU

ctrl-b ... page back  
ctrl-f ... page forward  
ctrl-e ... obrazovka o radek nahoru  
ctrl-y ... obrazovka o radek dolu  
G ... posledni radka  
gg ... prvni radek  
H ... na zacatek stranky  
M ... na prostredek stranky  
L ... na konec stranky  
(, ) ... veta vzad, veta vpred  
{, } ... odstavec vzad, odstavec vpred  
% ... skoci na pridruzenou zavorku (,),{,},[,]  
|, 0 ... zacatek radku  
$ ... konec radku  
e ... (end of word) konec slova (a-zA-Z)  
E ... (End of Word) konec slova (pred mezeru)  
b ... (beginning of word) zacatek slova (a-zA-Z)  
B ... (Beginning of Word) zacatek slova (za mezeru)  
w ... (word) dalsi slovo (a-zA-Z)  
W ... (Word) dalsi slovo v sirsim smyslu (oddelene mezerou)  
f: ... posun na radce na dalsi vyskyt znaku :  
F: ... posun na radce na predchozi vyskyt znaku :  
h,j,k,l ... znak: vlevo, dolu, nahoru, vpravo  
ma ... (marker) oznaceni znaku oznacovacem a  
'a ... skoci na prvni slovo za oznacovacem a  
`a ... skoci na znak oznaceny oznacovacem a  

## HLEDANI, NAHRAZOVANI

/asdf ... najde dalsi vyskyt asdf  
?asdf ... najde predchozi vyskyt asdf  
n ... najde dalsi vyskyt naposledy hledaneho retezce  
N ... najde predchozi vyskyt naposledy hledaneho retezce  
:sROZSAH/CO/CIM/PARAMETRY ... nahrazeni textu CO textem CIM v rozsahu ROZSAH  
ROSZAH ... "1,3" - prvni az treti radek, ".,$" - aktualni radek az posledni radek, "%" - cely dokument  
CO  
CIM ... "&" -  text, ktery vyhovuje podmince  
PARAMETRY ... "g" - vsechny vyskyty na radku, "c" - potvrzeni kazde zmeny, "i" - ignoruje velikost pismen  

## Nastaveni

:set number/nonumber ... zobrazuji se cisla radku na levo od radku  

## PRIKLADY

Smazani vsech radku, na kterych je vyraz "abc":

```
:g/abc/ d
```

Mezi malym pismenem a velkym udela novy radek:

```
:1,$s/([a-z]\)\([A-Z]\)/\1\r\2/g
```

Substutuce

```
:.,$s/a\{2,}/b/gi ... nahradi libovolny pocet A,a vetsi nez 2 pismenem b
:%s/[^a]/a/g nahradi libovolny znak krome a na a
:%s/\(\w\+\)\(\s\)\(\w\+\)/\u\3\2\l\1\\r/ ... prehodi 1. a 2. slovo, prvni zacne velkym pismenem, druhe malym, pote rozdeli radek
:%s/a*1/&2/ ... za libovolny pocet a-cek nasledovanym cislem 1 se prida znak 2

 .	any character except new line 	  	 
\s	whitespace character 	
\S	non-whitespace character
\d	digit 	
\D	non-digit
\x	hex digit 	
\X	non-hex digit
\o	octal digit 	
\O	non-octal digit
\h	head of word character (a,b,c...z,A,B,C...Z and _) 	
\H	non-head of word character
\p	printable character 	
\P	like \p, but excluding digits
\w	word character 	
\W	non-word character
\a	alphabetic character 	
\A	non-alphabetic character
\l	lowercase character 	
\L	non-lowercase character
\u	uppercase character 	
\U	non-uppercase character 
```

===Počeštění===

```

```

[Programovani ve VI na ROOTovi](http://www.root.cz/clanky/editor-vim-a-programovani/)
