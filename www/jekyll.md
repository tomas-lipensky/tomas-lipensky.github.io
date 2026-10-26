---
title: Jekyll
---

Statický generátor HTML stránek z Markdown souborů, napsaný v Ruby. Používá šablonovací jazyk Liquid (bloky jako {{ page.title }} nebo {% if user %})

## _config.xml

theme: minima ... Zobrazovací téma (šablona), v tomto případě minima  
title: nadpis ... aktivní nadpis vedoucí do hlavní strany  
description: moje stránky ... volitelný text ve formě html, který šablona ukazuje

## Témata

### Témata podporované GitHub Pages

[Architect](https://jekyllhub.com/themes/architect/)  
[Cayman](https://jekyllhub.com/themes/cayman/)  
[Dinky](https://jekyllhub.com/themes/dinky/)  
[Hacker](https://jekyllhub.com/themes/hacker/)  
[Leap day](https://pages-themes.github.io/leap-day/)  
[Merlot](https://jekyllhub.com/themes/merlot/)  
[Midnight](https://jekyllhub.com/themes/midnight/)  
[Minima](https://jekyllhub.com/themes/minima/)  
[Minimal](https://jekyllhub.com/themes/minimal/)  
[Modernist](https://orderedlist.com/modernist/)  
[Slate](https://jekyllhub.com/themes/slate/)  
[Tactile](https://jekyllhub.com/themes/tactile/)  
[Time machine](https://pages-themes.github.io/time-machine/)  

## Front Matter v md dokumentech

Je na začátku ohraničený řádky "---", "---". Nepovinné

title: název stránky ... nahrazuje # nadpis první kategorie
layout: default ... výchozí vzhled strany, bývá v tématu v adresáři _layouts