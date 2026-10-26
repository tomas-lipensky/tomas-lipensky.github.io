---
title: RUBY
---

## Externi odkazy

[abclinuxu: ruby pro zacatecniky](http://www.abclinuxu.cz/clanky/programovani/ruby-pro-zacatecniky-8-soubory-vyjimky-kontakt-s-os)  

## Promenne

url = node['repo_url'] + "tsm-client/install/" + version ... spojovani retezcu  
localfilepath = "#{Chef::Config['file_cache_path']}/#{filename}" ... tvoreni retezcu  
PROMENNA.to_s ... prevedeni promenne do retezce  
promenna.inspet ... vytvori dump promenne - prevede promennou vcetne cele struktury na text  
promenna.nil? ... true pokud promenna neni definovana nebo je nil  

## Operatory

| |, &amp;&amp; ... logicke operatory nebo a a  
|  --- |
and, or ... operatory na logicky beh programu  

### String

promenna.empty? ... pravda pokud se jedna o prazdny retezec ''  
promenna.strip ... orizne bile znaky na zacatku retezce  

### Array

promenna.empty? ... pravda pokud je to prazdne pole []  

### Hash

promenna.keys ... prevede hash na array klicu  
promenna.values ... prevede hash na array hodnot  
promenna.traverse{ |k, v| [k.downcase, v]} ... prevede hash na hash, kde ztransformuje klic na male pismena  
promenna.key({"klient" => "280"}) ... vrati klic kde hash ma hodnotu klient rovnu 280  
promenna.key?("klic") ... true, pokud klic "klic" existuje  

## cykly, podminky

prikaz if node['platform_family'] == 'rhel' ... podminka  
if node.attribute?('override_domain_name')\\else\\end\\ ... if-else podminka  
unless () {} ... misto if not  
case promenna\\ when 'hodnota'\\else\\end \\ ... case podminka  
node['dhs_ucdagent'].each do |key, value|\\ send(key, value)\\  end\\ .... for each  

## Vstup vystup

puts "OK:  #{checkOriginalInstallationDate}" ... vystup na standartni vystup  
file = [File](http://ruby-doc.org/core-2.3.1/File.html).open("/tmp/some_file", "w") { |file| file.write("your text") }... zapis do souboru i se zavrenim souboru.  
file.close ...  zavreni souvoru

## Testy

::[File](http://ruby-doc.org/core-2.3.1/File.html).exist?('/var/www/html/login.php') ... true pokud soubor existuje, soucast tridy [File](http://ruby-doc.org/core-2.3.1/File.html)  

## blok a vyjimky

begin  
  prikazy  
  raise 'chyba' ... vyvola vyjimku  
rescue Exception => e  
  puts e.message ... zobrazi text vyjimky - chyba  
  puts e.backtrace.join("\n") ... vypise podrobnosti o chybe vcetne radku  
  prikazy  
  retry ... zkusi jeste jednou blok, ktery selhal  
end

## Modudly

require 'chef/win32/version' ... nacteni externiho modulu  

## Ruzne funkce

Time.now.strftime('%Y%m%d%H%M%S%L') ... cas v presnem formatu
