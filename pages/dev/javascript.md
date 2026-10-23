# WEB - Javascript

### JS servery

[node.js](https://cs.wikipedia.org/wiki/Node.js) ... javaskriptovy serverovy engine  
node main.js ... spustí js soubor, třeba console.log("ok")  

### npm

balíčkový manažer pro nodejs

[npm](https://npmjs.org/) config list ...  vypis konfigurace  
npm config get registry ... nastavení registrů  
npm login ... připojení k repozitáři  
npm config set registry https://artifactory.vodafone.com/artifactory/api/something/ ... konfigurace repozitáře  
npm login --registry=https://npm.pkg.github.com  
npm whoami ... zobrazí uživatele v repozitáři  
npm whoami --registry=https://npm.pkg.github.com ... v konkrétním repozitáři  
npm install socket.io ... nainstaluje knihovnu  
### yarn

balíčkový manažer pro nodejs nad npm

package.json ... seznam balíčků k instalaci a skriptů  
yarn.lock ... zámek na verze npm balíčků  

[yarn global](https://classic.yarnpkg.com/lang/en/docs/cli/global/) dir ... globální nastavení  
yarn global bin ... kam bude yarn dávat symlinky balíčků  
yarn bin ... lokace bin souboru  
yarn list ... seznam nainstalovaných balíčků  

yarn add react-native-cli ... nainstaluje react-native-cli i se závistlostma  
yarn install --update-checksums ... provede instalaci balíčků i se závistlostma z definičního souboru package.json  
yarn remove react-native-cli ... odinstaluje balíček  
### Nastroje

[Storybook](https://storybook.js.org/) ... nastroj na vyvoj izolovanych komponent stranek pro React, Vue a Angular  
[https://www.jslint.com](https://www.jslint.com) ... linter - kontroluje kód - hledá chyby v syntaxi i čistotě kódu  
[yui compressor](https://refresh-sf.com/yui) ... kompresuje kód aby byl kratší  

### Knihovny

[jQuery](https://en.wikipedia.org/wiki/JQuery) ... Knihovna s funkcema na manipulaci s DOM (Document Object Model), AJAXem, JSONem atd. Napriklad meneni obsahu bloku html kodu atd.  
[TableFilter](http://koalyptus.github.io/TableFilter/examples) ... filtry a efekty k HTML tabulkam  
[rGraph](https://www.rgraph.net/) ... JS generovani grafu z JSON textu  
[chartjs](http://www.chartjs.org) ... dalsi grafy  
[gojs](https://gojs.net/latest/samples/sankey.html) … JS diagramy  

### js priklady

[js projekty cloveka Peteris Krumins](https://github.com/pkrumins)

### AJAX

[Clanek o AJAXu na root.cz](http://www.root.cz/clanky/ajax/)  

### Promenne, funkce na promennych

typeof promenna ... vrátí typ proměnné, třeba "object"  

##### Řetězce

var text='aaa', (int)cislo; ... definice nove proměnných  
text.length ... délka řetězce  
strlen(text) ... funkce délka řetězce  
text.charAt(0) ... první písmeno  
text.search('a') ... najde index prvího výskytu v textu  
[iarseInt](https://developer.mozilla.org/en-US/docs/web/javascript/reference/global_objects/parseint)(test) ... vyparsuje číslo z textu  
text.toUpperCase() ... převede na velká písmena, podobně toLowerCase()  

##### čísla

var cislo=1;  
var soucet=cislo + 10; ... součet  
var modulo=cislo++ % 3; modulo 2/3=2. cislo se zvětší o 1  
cislo.toString();  

##### pole

var pole = new Array(); ... prázdné pole  
var pole = ["hlina", "hnuj", "brazda"]; ... pole řetězců  
pole.[push](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)("pisek") ... přidá další prvek do pole  
pole.splice(1,1) ... odstraní hnuj, vratí hodnotu odstraněných prvků, tedy hnuj  
pole['barva']="cervena"; ... přidá nečíselný index a nadefinuje hodnotu. Prvek je pole.barva  
isArray(pole) ... je pole?  
pole.length ... počet prvků  
var polepoli = [],[](],[); ... multipole řetězců  
pole.join(" "); ... slouci pole do retezce, oddelovac mezernik  

##### objekty

var obj={};  
obj.name='js' ... přidání typu  
var app={version: 1.0, getVersion: function() {return this.version;}} ... definice objektu s funkcí  
var app={ add: function(numbers, callback) {var result=0; for (number in numbers) {result=result + numbers[number)}}; if (callback !== undefined) (callback(result);) } ... definice callbacku  
app.add([3, 5], function(result) {console.log('Součet je ' + result);}) ... volání callbacku  

##### čas, datum

var datum = new Date(); ... definice času  
datum.getTime() ... v sekundách  
datum.getFullYear() ... rok  
datum.toJSON() ... převede na JSON  
Date().getTime() ... aktuální čas  
var x=1, interval = setInterval(function() {x++; if (x === 5) {clearInterval()}}, 1000) ... vytvoří časovou smyčku 4 sekund  
var interval = setInterval(function() {console.log('ahoj')}, 5000); ... za 5 vteřin po načtení stránky vypíše ahoj  

if (typeof x##### = undefined || x

0 ) {} ... undefined - typ nedefinovane proměnné  
isNoN(var) ... je to Not-a-Number?  
##### =,

... je rovno i stejný typ, je rovno, může být jiný typ  

### konstrukce iterace, smyčky, podmínky, funkce

if(true) {} else if {} else {} ... if podmínka  
switch(age){ case "1": alert("1"); break; case "2": alert("2"); break; default:: alert("default"); break;} ... klasicý case, jako if, else if, else, ale jen na operator =  
function jmenoFunkce(parametry) { return 0; }  
for(i=1, i<5, i++) {}  
for(variable in array) {document.write(variable)}  
white(true) {if(true) {break}} ... break přeruší smyčku  
do { continue; alert("ahoj")} white(i--<1) ... continue přeskocí zbytek cyklu, neprovede další příkazy  

### console

F12 ve Firefoxu nám u
### Web javascript funkce

console.log();
alert("Ahoj") ... vykakovací okno s textem s jedinou volbou OK  
var c = confirm('Opravdu opistit stránku?') ... vyskakovací okno s OK a Cancel, výstup true/false  
if(c) { alert('zmáčkl jsi OK') } ... vystup z confim  
prompt("Kolik je Ti let", "nevím") ... vyskočí okno s textovým polem. Druhý nepovinný parametr je výchozí hodnota. Vrátí zadanou hodnotu, nebo false  
window.localtion = "http://tomas.lipensky.cz/"; ... změní aktuální URL pro aktuální okno  
escape('$~^#') ... převede text do URL kédování  
unescape(text) ... odescapování  

### DOM

[https://caniuse.com/queryselectorall](https://caniuse.com/queryselectorall) ... ukazuje které browsery opdporují metodu querySelectorAll  
document.write("I say \"hello " + name + '"' ) ... výstup textu, slepený s proměnnou name  
document.getElementById('id3').style.backgroundColor=red  
%%<input type'text' id='mojeId'><script>var id=document.getElementById('mojeId'); id.value='hodnota'</script>%%  
%%<div id='mojeId2'></div><script>var id=document.getElementById('mojeId2');id.innerHTML='<b>ahoj</b>'</script>%%  
element = document.querySelector('nav ul li a') ... vybere objekt pomocí dotazu, tedy v <nav><ul><li>  
elements = document.querySelectorAll('nav ul li a') ... pole - vybere objekty pomocí dotazu, tedy v <nav><ul><li>  

element.text ... textová hodnota elementu  
element.innertext = 'ahoj' ... změní hodnotu textu  
element.innerHTML = '<strong>ahoj</strong>' ... změní hodnotu html  
element.remove() ... smaže element  
element.getAttribute("href") ... frátí hodnotu atributu  
element.hasAttribure("href") ... vrátí jestli atribut existuje  
element.remove("href")  
element.offsetLeft ... velikost okraje z leva  
element.offsetParent.offsetTop ... velikost okraje rodičovského objektu z vrchu  
element.childNodes ... vnořené HTML objekty  
element.style.border = '1px solid #000'; ... nastaví CSS rámeček  
element.setAttribute('style', 'witdth:100px;height:100px') ... dynamické měnění stylu  

##### Přidání elementu

newelement = document.createElement('a');  
newelement.innerText = 'google';  
newelement.setAttribute('href') = 'https://google.com';  
document.body.appendChild(element)  

window(url, [name], [options], [replace]) ... otevře nové okno s danou url. name= _blank, _self, _parent, _top,  _framename, options=width, height, ...  
window("http://tomas.lipensky.cz/", "_blank", "width=100,height=100,scrollbar=no", "true");  

### události - events

onClick, onDblClick, onFocus, onBlur, onMouseDown, onMouseUp, onMouseOver, onMouseMove, onMouseOut, onKeyDown, onKeyUp, onKeyPress  

%%<span onDblClick="location.href='index.jsp'">dvakrát klikni</span>%%  ... zmena URL aktualni stranky pri kliknuti  
%%<a href="#home" onClick="location.reload()'">%%  ... znavunacteni stranky pri kliknuti  
%%<a href="#home" onMouseOver="window.open('index.jsp#home')" >%% ... otevreni noveho okna a v nem stranky pri kliknuti
%%<a href="javascript: void(0);" ></a>%% ... prázdný link, co nic nedělá  

element.addEventListener('click', function() {console.log('klik')}) ... nastavi poslouchání na události, callback volá funkci  
element.attachEvent('mouseover', function(){}) ... jak addEventListener, ale pro Explorer  
### JSON

a=["1","a",{"x":"ttmp"}] ... objekt - pole se smysenymi typy  
a.toSource()->k ... prevede objekt na JSON objekt (reprezentovany retezcem)  
b=eval("(",j,")") ... preveze JSON objekt na pole  

====Trideni pole====

```
function compare(a,b) {
  if (a.last_nom &lt; b.last_nom)
    return -1;
  if (a.last_nom > b.last_nom)
    return 1;
  return 0;
}

objs.sort(compare);
```


### JQuery

%%<script src="jquery.js"></script>%% ... inicializace jquery  
$(window).ready(function() {alert('Loaded')}); ... selektor - stránka, stav - načteno => vyskočí hláška  
var MyID = $('#elementID') ... sekektor html značky s id='elementID'  
var tucne = $('.bold') ... selektor značek s třídou class='bold'  
var body =  $('body') ... selektor značky <body>  
var names =  $('[name="name"]') ... selektor značek, co mají v sobě atribut name="name"  
$("textarea").focus(function() { $('.bold').css("display", "none") }) ... po kliknutí na <textarea> se změní css styl na none  
$("input").hover(function() {$(this).blur()}), function() {$(this).css("border", 0)}); ... při najetí na input daný objekt při najetí myší se rozmlží, při odjetí myši se změní css styl  

akce: keypress(), mouseup(), mousedown(), mouseover(), mouseenter(), mouseleave, onmouseout, click, dlbclick, focusin, focusout  
akce na objektu append("přidáno")  
$(this).next().toggle() ... když display=none, tak zobrazí, a naopak  
.hide(), .show() ... skryje, zobrazí, paramert může být jak rychle s zmizí, nebo se zobrazí v ms  
fadeIn, fadeOut, fadeToggle, slideUp, slideDown, slideToggle ... slide - bude překryto dalšími objekty a tím zmizí  
.submit() ... odešle formulář  
keypress( function(e) { $(this).append(e.keyCode ? e.keyCode : e.which)} ) ... po stisknutí přidá číslo znaku, jež byl zmáčknutý. některé browsery požívají which, některé keyCode  
$(this).html() ... dostanu vnitřek html značky  
$("div").html("nic") ... změním vnitřek značky, v div se objeví "nic"  
$(this).animate({width: "+=100"}) ... zvětší objekt  
$(this).attr("href") ... vrátí atribut href  
$(this).attr("href", "http://tomas.lipensky.cz/") ... změní atribut href  
$(this).slideUp(3000, function(alert("kuk"))) ... callback, jak skončí slideUp, tak se provede callback funkce  
$("#tady").load("file.txt") ... do elementu #tady načte obsah souboru file.txt  
$.ajax() = jQuery.ajax()  
$.ajax({url: "file.txt", success: function(data)}) ... po načtení provede funkci, více na [http://api.jquery.com/jQuery.ajax](http://api.jquery.com/jQuery.ajax)
