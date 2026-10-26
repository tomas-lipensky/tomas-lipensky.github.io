---
title: ansible
---

## Odkazy

[galaxy.ansible.com](https://galaxy.ansible.com/) ... verejna knihovna roli  

## Klient

ansible win -i hosts win_ping  
ansible win -i hosts win_reboot  
ansible win -i hosts wait_for_connection  
ansible localhost -m ping ... otestuje spojeni pro ansible  
ansible localhost -m command -a uptime ... spusti příkaz uptime  
win_regedit  
win_regmerge  

ansible-playbook playbook.yaml --syntax-check
ansible-playbook --connection=local --inventory 127.0.0.1, playbook.yml -e ansible_python_interpreter=/usr/bin/python3 ... spusti playbook lokalne na mistnim pocitaci, nastavi python3 misto python, kdyz jsou nainstalovane oba  
ansible-playbook -i inventory/hosts --limit testserver playbook1.yml ... Spusteni playbooku na omezem seznamu z inventare  
ansible-playbook playbooktags.yml --tags untagged,tag1 ... provede jen neotagované tasky a tasky s tagem tag1  
ansible-playbook playbooktags.yml --skip-tags=install,mydir ... vynechá otagované tásky tagy install, mydir  
ansible-playbook playbooktags.yml --extra-vars action=install ... nadefinuje, nebo přepíše proměnnou/fakt  

## playbooky

### obecná konstrukce běhu - play

name:  
hosts: ... seznam nodů, nebo grup, na které se budou tasky aplikovat  
serial: 1 ... úroveň paralelizace  
ignore_unreachable: true ... přeskočení nedostupných nodů  
vars: ... proměnné  
tasks: ... seznam tasků  
handlers: ... handlery - akce, co se podmíněně spustí při konkrétních změnách v tasku  

### task

#### nepovinné, dpolňující parametry

name: ... jméno tásku  
tag: ... jméno tagu - tagy se označuje, co se provede a co ne  
when: ... podmínka, za jaké se task provede  
register: command_result ... proměnná, do které se uplží výstup tásku  
delegate_to: ... určí se node, na kterém se task provede, například localhost  
vars: ... proměnné pro task  
ignore_errors: true ... task se považuje za úspěšný i když nastanou chyby  
ignore_unreachable: false ... úspěch, i když je node nedostupný  
failed_when: "'FAILED' in command_result.stderr" ... informace, kdy se považuje task jako neúspěšný  
changed_when: "bass_result.rc != 2" ... definuje, kdy se task považuje za změnu konfigurace  

#### typy tasku

debug: ... výpis progměnných  
set_fact: ... nastavení proměnných  
shell: ... provedení akce v shellu  
fail: ... ukončení běhu  
import_tasks: ... načte tasky z jiného souboru  
include_role: ... vloží roli (playbooky definované v extra adresáři, něco jako modul, nebo knihovna)  
uri: ... HTTP/HTTPS volání  
block: ... blok tasků, více v sekci block  
tempfile: ... vytvoří dočasný soubor, sám se smaže po konci  
read_csv: ... načte csv soubor  

#### blok

block: ... vytvoří blok tasku  
always: ... provede se vždy, i když se blok přeruší z důvodu chyby, třeba čištění  
rescue: ... provede se, když je chyba  

handler: ... volání tasku jen když se provede změna  

### vyrazy

promenna.json.tag_list |lower ... (string) vyraz, kde promenna typu json, jeji onjekt tag_list se prevede na male pismen  
selectattr('vg_name', 'equalto', 'vgapplis') ... (list) vybrani podle atributu  
json_query(sum_query) ... (list) - vyraz v jsonu  
list ... (list) - prevede na jednoduchy seznam  
sum ... (cislo) - secte  
first ... (prvek) - prvni polozka seznamu  
length > 0 ... (cislo) velikost seznamu je vetsi nez 0  
is defined ... (boolean) - je definovana  
select('match', '^(eth|wlan)[0-9]+') | list ... vyber ze seznamu  
in LIST ... (boolean) - je prvek obsazen v seznamu?  

====Jinja2 filtry====

```
{{ secrets | to_nice_yaml( width=150, explicit_start=True, explicit_end=True) }}
```
 ... naformatuje datovy objekt do yamlu
