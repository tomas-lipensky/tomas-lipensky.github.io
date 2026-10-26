---
title: JQ
---

## Externi odkazy

[JQ manual](https://stedolan.github.io/jq/manual/#tostring)  

## jq přepínače

1.r ... zobrazí jen hodnotu, nedává do uvozovek  

## jq příkazy

select(.pole == "hodnota") ... selekce, výběr, filtr = zobrazí jen hodnoty splňující podmínku  
map(.hodnota) = .[] | .hodnota ... vnoží se do seznamu  
tonumber  
tostring  
[:4]

## Příklady

cat soubor.json | [jq](https://stedolan.github.io/jq/manual/) -r '.automatic.filesystem | map([.mount, .kb_used, .kb_size] )' | jq -r '.[] | @csv' ... prevede json do csv  
cat soubor.json | jq -r '.rows | map([.name, .chef_environment, .automatic.os, ('`date +%s`' - .automatic.ohai_time | tostring)] | join(", ")) | join("\n")' ... dalsi zpusob prevodu do csv  
echo '[{"a": "b"}, {"a": "c"}]' | jq '.[] | .a' ... vypise "b" a "c"  
echo '[{"a": "b"}, {"a": "c"}]' | jq '.[] | {text: .a}' ... vypise {"text": "b"}, {"text": "c"}  
echo '[{"a": "b"}, {"a": "c"}]' | jq '[.[] | {text: .a}]' ... vypise [{"text": "b"}, {"text": "c"}]  
cat az_vm_list-d_live.json | jq -r '.[] | select(.storageProfile.osDisk.osType == "Windows") | "\(.name)\t' ... vybirani jen urcitych zaznamu, formatovani na vystup  

## Spojovani JSON souboru

jq -s add soubor1.json soubor2.json ... spoji/slouci 2 a vice json souboru. Respektuje strukturu objektu  
jq -s . ... spoji vstupujici objekdy do pole (1. objekt pole = 1. objekt/soubor, 2. objekt pole = 2. objekt/soubor, ...)  
jq '.[]' soubor1.json soubor2.json ... spoji json objekty. [{soubor1.objekt1}], [{soubor1.objekt2}], ... [{soubor2.objekt1}], ...  
jq -s .  soubor1.json soubor2.json ... spoji json objekty. [{soubor1.objekt1}, {soubor1.objekt2}, ...], [{soubor2.objekt1}, ...]({soubor1.objekt1}, {soubor1.objekt2}, ...], [{soubor2.objekt1}, ...)  
jq --slurp "[.[] | .[]" 1.json 2.json ... spoji json objekty. [{soubor1.objekt1}, {soubor1.objekt2}, ... {soubor2.objekt1}, ...]  

## Konverze typu

echo '[{"number": 1, "string": "one"}]' | jq '.[] | .string + ": " + (.number|tostring)' ... prevede objekt .number na text  
echo '[{"number": 1, "string": "one"}]' | jq -r '.[] | [ .string, .number|tostring ] | join(": ")' ... dalsi moznost toho sameho  

## Konverze TXT na JSON

jq '. | split("\n") | map( {value: .} ) | {rules: .} ' -R -s rules.txt ... vytvori json strukturu, kde .rules je pole objektu s klicem "value" a hodnotou daneho radku TXT souboru  
jq '. | split("\n") | map( split("\t") | {value: .[0], tag: .[1]} ) | {rules: .} ' -R -s rules.txt ... z txt kazdy radek rozdeli podle tabulatoru a zapise to json (1. hodnota jde do .rules.value, druha do .rules.key
