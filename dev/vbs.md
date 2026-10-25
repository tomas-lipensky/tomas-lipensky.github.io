# VBScript

### Externi odkazy

[Seznam prikazu a objektu](http://ss64.com/vb/)  
[Scriptovani na MS](http://technet.microsoft.com/en-us/library/ee198844.aspx)  

### Spousteni VBScriptu

wscript a.vbs ... otevre VBScript v okne (neumoznuje vystup na stdout)  
cscript a.vbs ... otevre VBScript v konzoli  

### Promenne a komentare

dim aaa ... deklarace nove promenne  
Const PI=3.14 ... definice konstanty  
Chr(56) ... znak o asci kodu 53  
aaa = #1/1/2000# ... nastavi cas  
dim a(3) ... deklaruje 3 rozmerne pole  
dim aa() ... deklaruje pole  
dim b(3,3) ... deklaruje matici 3x3  
ReDim a(5) ... zmeni dimenzi pole a na 5  
A=Array(1, 2, 3) ... Nadefinuje 3 rozmerne pole o prvcich 1, 2, 3  
Join(A) ... Vsechny prvky pole vsadi do jednoro retezce, prvky oddelene mezerou  
Split("ahoj cau nazdar") ... rozdeli retezec na pole  
Split("D:\aaa\bbb","\",2) ... rozdeli retezec na pole, "\" oddelovac, maximalne na 2 pole  
Filter(pole, "Tomas", false) ... vrati nove pole, ktere neobsahuje zadne prvky obsahujici slovo Tomas  
UBound a ... vrati velikost pole  
Set Args = Wscript.Arguments ... prirazeni objektu Wscript.Arguments promenne (pole) Args (argumentu skriptu)  
Args(0) ... prvni parametr skriptu  
'komentar ... komentar pokud je prvni slovo na radku i jinak  
Rem komentar ... komentar, pokud je prvni slovo na radku, jinak :Rem  

### Podminky, cykly, vlastni funkce

If ? then ?  Else

```
If (A>1 And B=True) Then
?
Else
?
End If
```

```
For I = 1 To 6
?
Next
```

```
do
?
Loop Until ?
```

```
do While ?
?
Loop
```

```
Select Case promenna
 Case "A"
  ?
 Case "B"
  ?
End Case
```

```
Function FUNKCE (jedenParametr, druhyParametr)
  ?
  FUNKCE=1
End Function
```

Vysledek = FUNKCE (1, 2) ... volani funkce  
Exit Function ... predcasne ukonceni funkce

```
Sub PODPROGRAM (jedenParametr, druhyParametr)
  ?
End Sub
```

Call PODPROGRAM (1, 2) ... volani podprogramu  

##### Funkce na promennych

String(0, "*") ... vystup je 60 hvezdicek  
UCase(aaa) ... prevede na velka pismena  
LCase("aHoJ") ... prevede na mala pismena  
a=StrComp("ahoj", "Aahoj") ... porovna retezce, 0 stejne  
Trim("  a  ") ... oseka mezery na zacatku a na konci (LTrim, RTrim zleva, zprava)  
Len("Ahoj") ... delka retezce  
Mid("a b v d", 3,1) vybere podretez zacinajici na 3. pozici dlouhy 1 znak  
Right("Ahoj",2) ... Vybere prave 2 znaky retezce ("oj")  
Left("Ahoj",2) ... Vybere leve 2 znaky retezce ("Ah")  
Replace("Ahoj chlape", "Ahoj", "Nazdar") ... nahradi sekvence znaku v retezci jinymi  
Replace("ahoj chlape, aby ale.", "a", "A", 1, 2) ... nahradi 2 sekvence znaku v retezci jinymi, zacne na prvnim znaku (prvni 2 a nahradi na A)  
Instr("Ahoj Chlape", "Ch") ... Vrati pozici podretezce "Ch"  
Instr(5, "Ahoj Chlape", "ch", vsTextCompare) ... Vrati pozici podretezce "Ch" bez ohledu na velikost pismen. Zacina od 5 pozice  
Instr("aaa.jpg", ".jpg") ... Jako Instr, ale hleda od zadu  
Int(cislo) ... prevede promennou na cele cislo  
IsInt(a) ... vrati True pokud je a cislo  
IsStr, IsEmpty, IsDate, IsArray ... otestovani typu argumentu  
IsNumeric(cislo) ... vrati True, pokud je promenna cislo cislo  
FormatNumber(3,2) ... naformatuje cislo na tisk, ze obsahuje 2 desetinna cisla  
FormatPercent(1,2) ... naformatuje cislo na tisk, ze obsahuje 2 desetinna cisla a procenta (100,00 %)  
FormatCurrency(3,2) ... naformatuje cislo na tisk, ze obsahuje 2 desetinna a menu (3,00 Kc)  
FormatNumber(Now, vbGeneralDate) ... naformatuje cas na tisk, datum i cas (vbLongDate, vbShortDate, vbLongTime, vbShortTime)  
Rnd ... vrati nahodne cislo mezi 0 a 1  
Randomize ... vynuluje predchozi nahodne cislo  
Fix(6 * Rnd) + 1 ... vrati nahodne cislo mezi 1 a 6  
Now ... aktualni datum a cas  
Date ... Aktualni datum  
Time ... Aktualni cas  
DateSerial(2012,20,40) ... Ukaze 20 mesicu a 40 dni od 1.1. 2012  
DateValue ... prevadi retezec na datum  
Hour ... Aktualni hodina
DateDiff ... rozdim mezi 2 datumy  
Round(5.7) ... zaokrouhli cislo (6)  
Sgn(-4) ... vrati znamenko  
Abs(-4) ... vrati absolutni hodnotu  
Sqr(2) ... vrati mocninu (4)  
Exp, Log, Sin, Cos ... Matematicke funkce  
CInt ... prevede vyraz na cislo  
CLng, CSng, CDbl, CCur, CStr, CBool, CByte, CDate ... prevede argument na urcity datovy typ  

### funkce obecne

Wscript.Echo "Ahoj" ... Vypise "Ahoj" na std vystup  
Document.Write "Ahoj" & jemnp & "!" ... tisk na "Ahoj" do aktualniho dokumentu (treba html)  
aaa=InputBox("Zadej cislo") ... vyskakovaci okno pro zadani vstupu  
MsgBox("Chyba uzivatele") ... vyskakovaci okno se zpravou  
AAA=MsgBox("Ano, ne?",vbYesNo) ... vykakovaci okno na Ano, ne (jine moznosti vbOKOnly, vbOKCancel, vbAbortRetryIgnore, vbYesNoCancel, vbRetryCancel, vbCritical, vbQuestion, vbExclamation, vbInformation)  
WScript.StdOut.Write("Enter Your full Name>") ... vypis na std. vystup  
WScript.StdIn.Read(0) ... cteni ze vstupu  
strMyName = WScript.StdIn.ReadLine() ... Prirazeni cteni ze vstupu  

### Objekty

Set Args=Wscript.Arguments ... Argumenty skriptu  
Set objShell=CreateObject("WScript.Shell") ... vytvori novy objekt  
Set objCmdExec = objshell.exec("cmd /s dir C:") ... Na novem objektu spusti prikaz  
objCmdExec.StdOut.ReadAll ... vystup prikazu  
wscript.sleep 500 ... pocka 500 ms  
Set objFSO = CreateObject("Scripting.[FileSystemObject](http://ss64.com/vb/filesystemobject.html)") ... prace s File Systemy  
Set zip = objFSO.OpenTextFile(target, 2, vbtrue) ... otevre soubor pro zapis  
zip.Write "PK" & Chr(5) & Chr(6) & String( 18, Chr(0) ) ... zapise do souboru (hlavicku ZIPu)  
zip.Close ... uzavre soubor  
Set zip = nothing ... odstrani vazani promenne na objekt  
Set ObjSehll(<a href="http://msdn.microsoft.com/en-us/library/windows/desktop/bb774063%28v=vs.85%29.aspx|shell.application]])  

##### Pouziti v HTML

&gt;SCRIPT LANGUAGE="VBSCRIPT"&lt; ... Zacatek VBScript bloku  
&gt;!-- ... VBScript blok musi byt v kometari  
window.open "http://google.com" ... otevre URL google.com  
1.-&lt; ... konec komentare  
&gt;/SCRIPT&lt;  

&gt;SCRIPT LANGUAGE="VBSCRIPT"&lt; SRC="C:\VBS.vbs"&lt;&gt;/SCRIPT&lt; ... nacteni scriptu ze souboru
