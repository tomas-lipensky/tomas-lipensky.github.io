# Úkoly: prohlížeč markdown souborů

Cíl: stránka s levým panelem (strom adresářů a souborů bez koncovky `.md`) a pravým panelem, kde se po kliknutí zobrazí obsah souboru převedený z markdownu do HTML (`#` se změní na `h1`). Vzhled musí jít později snadno měnit.

Pozn.: `show.html` už existuje jako první verze (výběr adresáře a seznam souborů). Úkoly níže ji rozšiřují na strom a oddělují kód od vzhledu.

## 1. Příprava struktury
- [ ] Vytvořit adresář `viewer/` s `viewer.css` a `viewer.js`.
- [ ] Vytvořit `viewer/index.html` (nebo přestavět `show.html`) a odkázat na CSS a JS.
- [ ] Rozhodnout, jestli se `index.md` zobrazí jako úvodní stránka.

## 2. Zdroj stromu stránek
- [ ] Vygenerovat seznam souborů při buildu Jekyllu pomocí Liquid (`site.static_files`, filtr na `.md`) do JSON, například `tree.json`.
- [ ] Seskupit soubory podle adresářů a seřadit je abecedně.
- [ ] Vynechat adresáře bez `.md` souborů a soubory, které nemají být vidět (`README.md`, `TASKS.md`).
- [ ] Ošetřit soubory s front matter (Jekyll je převede na HTML a ve `static_files` nebudou). Buď front matter odstranit, nebo je přidat ze `site.pages`.
- [ ] Záložní varianta: skript (`build-tree.sh` nebo `.py`), který `tree.json` vygeneruje lokálně.

## 3. Levý panel (navigace)
- [ ] Načíst `tree.json` a vykreslit strom: adresáře jako rozbalovací položky, soubory jako odkazy.
- [ ] Název souboru zobrazit bez `.md`.
- [ ] Adresáře ve výchozím stavu sbalené. Po kliknutí se rozbalí a sbalí, přidat šipku a přístupnost z klávesnice (`button`, `aria-expanded`).
- [ ] Zvýraznit aktivní soubor a rozbalit adresář, ve kterém je.
- [ ] Přidat filtr (vyhledávání podle názvu) a volitelně tlačítka „rozbalit vše“ a „sbalit vše“.

## 4. Pravý panel (obsah)
- [ ] Po kliknutí na soubor načíst `.md` přes `fetch`.
- [ ] Převést markdown na HTML knihovnou `marked`.
- [ ] Výsledek sanitizovat přes `DOMPurify` před vložením do stránky.
- [ ] Přepsat relativní odkazy a obrázky v markdownu tak, aby fungovaly vzhledem k adresáři souboru.
- [ ] Odkazy na jiné `.md` soubory otevírat uvnitř prohlížeče, ne jako stažení.
- [ ] Zvýraznění syntaxe bloků kódu (`highlight.js`).
- [ ] Ošetřit chyby: soubor nenalezen, prázdný soubor.

## 5. Navigace a URL
- [ ] Ukládat otevřený soubor do hashe (`#dev/git`), aby šel sdílet odkaz a fungovalo tlačítko zpět.
- [ ] Při načtení stránky otevřít soubor z hashe a rozbalit jeho adresář.
- [ ] Při změně souboru posunout obsah nahoru a nastavit `document.title`.

## 6. Příprava na design
- [ ] Všechny barvy, písma a rozměry dát do CSS proměnných (`:root { --bg; --fg; --accent; --sidebar-width; ... }`).
- [ ] Layout postavit na CSS Grid (sidebar + obsah) a oddělit ho od vizuálního stylu.
- [ ] Obsah renderovat do kontejneru s třídou (například `.markdown-body`), aby se styly dokumentu daly vyměnit jedním souborem.
- [ ] Připravit světlé a tmavé téma přes `data-theme` na `<html>` (přepínač a `prefers-color-scheme`).
- [ ] Responzivní verze: na úzké obrazovce skrýt sidebar za tlačítko (hamburger).
- [ ] Vytvořit `theme-default.css` jako výchozí téma, ke kterému se později přidají další.

## 7. Dokončení
- [ ] Vyzkoušet na všech adresářích (`automatizace`, `blog`, `data`, `db`, `dev`, `matematika`, `net`, `os`, `ostatni`, `other`, `sq`, `sw`, `web`, `wiki`, `www`).
- [ ] Zkontrolovat soubory s netypickými názvy (mezery, diakritika, tečky) a velké soubory.
- [ ] Odkaz na prohlížeč přidat do `index.html` nebo `index.md`.
- [ ] Otestovat nasazení na GitHub Pages (`jekyll serve` lokálně).
- [ ] Rozhodnout o `os_aix.txt` (převést na `.md`, nebo vynechat).
