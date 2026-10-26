---
title: Helm
---

## Bloky/Akce

### komentáře

```helm
{{ */ komentář /* }}
```

### define/include

definice funkce

```helm
{{- define "TL.vypisObraz" -}}
velikost: .Values.obraz.velikost
{{- end -}}
obraz: {{ include "TL.vypisObraz" $ }}
```

### if

```helm
{{ if eq .Values.hodnota "ahoj"}}
  # Něco
{{ else if eq .Values.hodnota "cau" }}
  # Něco
{{ else }}
  # Jinak
{{ end }}
```

### with

změní rozsah operátoru .; tzn. blok

```helm
{{ with .Values.doma }}
  vKuchyni: {{.vkuchyni}}
{{end}}
```

tedy v bloku .vkuchyni je jako bez bloku .Values.doma.vkuchyni

### range

for-each blok

```helm
barvy: |-
    {{- range .Values.barvy }}
    - {{ . | title | quote }}
    {{- end }}
```

## Operátory

`velikost: ![ required "Je potřeba zadat velikost" .Values]( required "Je potřeba zadat velikost" .Values.velikost )` ... validace, zda proměnná je nadefinovaná

```helm
{{- if not (has .Values.lidi "Tom") }}
{{- fail "proměnná lidi musí obsahovat Toma" }}
{{- end }}
```

 ... vyskočení z běhu se zprávou, určená např. k validaci proměnných  

### proměnné

$promenna := "aaa" ... nastavení proměnné  
.Value.aaa.bbb ... reference na proměnnou z values aaa.bbb  
index "aaa" "bbb.ccc" ... reference na proměnnou, když obsahuje "divné" znaky, jako tečky, pomlčky atd.  

### seznamy - list

splitList "/" $.Values.image.name ... rozseká řetězec na seznam, oddělovač "/"  
last ... vrátí poslední prvek pole/seznamu  
first ... vrátí první prvek pole/seznamu  
list $ .  

### logické

contains "rn" "Brno" ... true, když řetězec obsahuje podřetězec rn  
hasPrefix "Brn" .Value.mesto ... true, když řetězec obsahuje prefix Brn  
hasSuffin "no" "Brno" ... true, když řetězec onsahuje koncovku no  
and () () ... logický a operátor  
or () () ... logické nebo  
not () ... negace  

### řetězce

cat "ahoj" "muj" "kamaráde" ... spojí texty do jednoho řetězce, tedy "ahoj muj kamarade"  
indent 2 ... udsadí text 2 mezerama  
nindent 4 ... udělá nový řádek a odsazení 4 mezery  
randAlphaNum uses 0-9a-zA-Z
randAlpha uses a-zA-Z
randNumeric uses 0-9
randAscii uses all printable ASCII characters
replace " " "-" ... nahradí řetězec řetězcem, např "jsi nej kamarád" přepíše na "jsi-nej-kamarad"  
quote ... vloží text do dvojitých uvozovek  
squote ... vloží text do jednoduchých uvozovek
