---
title: Perl - Regularni vyrazy
---

## Akce s regularnimi znakami

$RETEZEC =~ s/TEXT1/TEXT2/; ... zameni prvni vyskyt TEXT1 na radku textem TEXT2  
$RETEZEC =~ s/TEXT1/TEXT2/g; ... zameni kazdy vyskyt TEXT1 na radku textem TEXT2  
$RETEZEC =~ s/TEXT1/TEXT2/gi; ... zameni kazdy vyskyt text1 (nerozlisuje velka/mala pismena) na radku textem TEXT2  
if( m/TEXT/ ) ... Vyhledavani pomoci regularnich znaku  

## Metaznaky

| ...	zacatek retezce  
$ ...	konec retezce  
. ...	any character except newline  
a* ...	vyskyt znaku a 0 krat nebo vicekrat  
+ ...	vyskyt znaku a 1 krat nebo vicekrat  
? ...	match 0 or 1 times; or: shortest match  
a? ...	zero or one as (i.e., optional a)  
repetition? ...	same as repetition but the shortest match is taken  
| ...	alternativa  
( ) ...	grouping; storing  
[ ] ...	mnozina znaku  
[abc] 	libovalny ze znaku: abc  
[0-9] 	Libovlany ze znaky 0 az 9 podle asci tabulky  
[\-]	znak pomlcka  
[\n]	znak novy radek  
[^abc] 	cokoliv, krome znaku abc  
a{3} ... znak a 3x po sobe  
a{2,} ... znak a alespon 2x po sobe  
a{2,3} ... znak a 2x az 3x  
\ ...	quote or special  

## Specialni lomitkove znaky

\t 	tabulator  
\n 	novy radek  
\r 	navrat na zacatek radku (CR)  
\xhh 	znak pode sestnactkoveho kodu hh  
\b 	word boundary  
\B 	not a word boundary  
\w 	slovni znak - ekvivalent [a-zA-Z_]  
\W 	ne slovni znak  
\s 	prazdny znak (mezera, tabulator, novy radek)  
\S 	znak, jez neni prazdny znak  
\d 	ciselny znak - ekvivalent [0-9]  
\D 	Neciselny znak  

### Priklady regularnich znaku

abc 	abc (that exact character sequence, but anywhere in the string)
^abc 	abc at the beginning of the string
abc$ 	abc at the end of the string
a|b 	either of a and b
^abc|abc$ 	the string abc at the beginning or at the end of the string
ab{2,4}c 	an a followed by two, three or four bs followed by a c
ab{2,}c 	an a followed by at least two bs followed by a c
ab*c 	an a followed by any number (zero or more) of bs followed by a c
ab+c 	an a followed by one or more bs followed by a c
ab?c 	an a followed by an optional b followed by a c; that is, either abc or ac
a.c 	an a followed by any single character (not newline) followed by a c
a\.c 	a.c exactly
[abc] 	any one of a, b and c
[Aa]bc 	either of Abc and abc
[abc]+ 	any (nonempty) string of as, bs and cs (such as a, abba, acbabcacaa)
[^abc]+ 	any (nonempty) string which does not contain any of a, b and c (such as defg)
\d\d 	any two decimal digits, such as 42; same as \d{2}
\w+ 	a word: a nonempty sequence of alphanumeric characters and low lines (underscores), such as foo and 12bar8 and foo_1
100\s*mk 	the strings 100 and mk optionally separated by any amount of white space (spaces, tabs, newlines)
abc\b 	abc when followed by a word boundary (e.g. in abc! but not in abcd)
perl\B 	perl when not followed by a word boundary (e.g. in perlert but not in perl stuff)
