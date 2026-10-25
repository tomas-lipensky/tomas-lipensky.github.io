# Scripting - batch files

### Externi odkazy

[Seznam NT preikazu](http://ss64.com/nt/)  

### Prikazy

##### Promenne, cykly, podminky, vystupy

SET AAA=HELO  
ECHO %AAA%
@echo %time% ... vypise aktualni cas  
ECHO %OS% ... bypise verzi operacniho systemu  
%USERNAME% ... aktualni uzivatel  
%PATH% ... cesta ke spustitelnym souborum  
%CD% ... Current directory - aktualni adresar  

[IF](http://ss64.com/nt/if.html)  
PRIKAZ1 && PRIKAZ2 ... jestli prikaz1 je v poradku, proved prikaz 2  
[FOR](http://www.robvanderwoude.com/for.php) %A IN (1 2) DO ECHO %A ... pouziti FOR v prikazove radce  
[FOR](http://www.robvanderwoude.com/for.php) %%A IN (1 2) DO ECHO %%A ... pouziti FOR v BAT souboru  

##### Ostatni prikazy

ATTRIB ... meni prava na pristupy k souborum  
ATTRIB +R +A +S -H D:\adresar\soubor ... zapne atribut na cteni, archiv a systemovy soubor, vypne skryty soubor  
ATTRIB -R D:\ /S /D ... zapne atribut na cteni v aktualnim adresari a jeho souborech (/S) i jeho podadresarich (/D)  
CACLS ... meni pristupy ACL k souborum a slozkam  
CACLS D: /T /G uzivatel:F ... na Disku D: a ve vsech podadresarich da uzivateli plny pristup (G-Grant, F-Full access)  
CACLS D:\adresar /E /R uzivatel ... Nanahradi prava, ale edituje je (/E). Odebere uzivatele z ACL  
CACLS D:\soubor /E /P uzivatel1:N uzivatel2:RWC /D uzivatel3 ... Nahradi ALC pro uzivatele1 na None, uzivatele2 Read Write Change a zakaze uzivatele 3 (Deny)  
CALL D:\BATCH\SendSuccessMail.vbs ... spusti VBS  
cscript ... jednotny prikaz na spousteni skriptu a kodu (perl, python, vbs), sluzby se musi registrovat  
@echo OFF ... vypne vypisovani prikazu na obrazovku  
md c:\users\<username> ... zalozi adrasar  
[net user](http://support.microsoft.com/kb/251394) klint >nul 2>&1 && echo User Exists || echo User doesn't exist  
rmtshare \\SERVER\UZIVATEL$=c:\users\uzivatel /grant uzivatel:f /grant administrator:f /remove everyone ... nasdileni adresare v siti. Pristup maji jen uzivatele uzivatel a administroator (f-full,r-read,w-write,c-change), nikdo jiny  
time /t ... ukaze aktualni cas  
type soubor.txt ... vypise obsah souboru  
where ... ukaze cestu ke spustitelnemu programu, ktery je v aktualnim adresari, nebo v PATH  
whoami ... vypise aktualniho uzivatele vcetne domeny
