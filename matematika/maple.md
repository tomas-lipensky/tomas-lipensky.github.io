---
title: matlab
---

### Maple

Volna alternativa k programu Maple je [Octave](http://www.gnu.org/software/octave/), ve kterem vsechny zaklady, o kterych zde pisi, funguji stejne, ci podobne, jako v Matlabu. Kromě těchto stránek najdete jistě celou řadu ostatních stranek, se základy ovládání a používání programu Matlab v českém jazyce. Ale třeba Vám budou právě tyto vyhovovat lépe než ty ostatní, jako třeba mě.

#### Popis kapitoly

Seznam příkazů, které obsahuje. Kliknutím na aktivní popis kapitoly se přemístíte na stránku, která dané téma popisuje.  

#### Základní poznatky

Zadávání skalárů (matic 1x1), vektorů (matic 1xm) a matic:  
x=1  
v=[1,2,3,4]  
A=[1,2;3,4]  

Výpis proměnné a:  
a  

Přiřazení matici (skaláru, vektoru) výsledek funkce:  
a=sin(1)  
[a]=sin(1)  
b=[sin(1),sin(0)]  
[c,d]=[sin(0),sin(-1)]  

#### Základní funkce

**zeros(m,n)** - matice plná nul o rozměrech mxn
**eye(m,n)** - jednotková matice o rozměrech mxn
**rand(m,n)** - matice o rozměrech mxn plná náhodných čísel v intervalu (0,1)  
**randn(m,n)** - matice o rozměrech mxn plná náhodných čísel v intervalu (-6?,6?)
**min([a,b,c])** - minimum z a,b,c
**max([a,b,c])** - maximum z a,b,c
**abs(a)** - absolutni hodnota z a
**disp('ahoj')** - vypíše hlášku "ahoj"

#### Základní operace s maticema

**X+Y** součet matic, souhlasi-li dimenze
**X+a** každé buňce matice X se přičte skalár a
**X-Y** rozdíl matic, souhlasi-li dimenze
**X-a** od každé buňky matice X se odečte skalár a
**X*Y** součin matic, souhlasi-li dimenze
**X*a** každá buňka matice X se vynásobí skalárem a
**X'** matice X se transponuje a komplexně sdruží
**X.'** matice X se transponuje
**X^p** matice X se vynásobí p-krát sama se sebou (mocnina), souhlasi-li dimenze
**X.+Y** součet matic po složkách, souhlasi-li dimenze
**X.-Y** rozdíl matic po složkách, souhlasi-li dimenze
**X.*Y** součin matic po složkách, souhlasi-li dimenze
**X.^p** prvky matice X se vynásobí p-krát samz se sebou (mocnina)
**X>Y** porovnání matic po složkách, souhlasi-li dimenze, vysledek matice plná nul a jednicek. (alternativy <, <=, >=, ==, ~=, &, |)

#### Podmínky

if elseif else end  
for break end
while end

#### Kreslení

plot  

#### Argumenty funkcí

nargin

#### načítání/ukládáni dat z/do souboru