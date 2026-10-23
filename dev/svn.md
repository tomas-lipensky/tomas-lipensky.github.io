# Subversion

### Externi odkazy

[Subversion](http://artis.imag.fr/~Xavier.Decoret/resources/svn/index.html)  
[Kniha Version Control with Subversion](http://svnbook.red-bean.com/)  

svn help ... seznam prikazu SVNka  
svnadmin help ... seznam prikazu SVNADMINa  

### Konfigurace SVN

~/.subversion/config ... Globalni nastaveni promennych klienta SVN  
echo "diff-cmd = tkdiff" >> ~/.subversion/config ... nastaveni grafickeho diff programu  
~/.subversion/server ... Globalni nastaveni pro server  

### SVN server

##### Spusteni a konfigurace SVN serveru

svnserve ... spusteni SVN serveru, ktery nabizi SVN databazi na portu 3690  
svnserve -d -r /svn ... spusti svn server jako demon, svn repozitar je /svn  
WebDAV ... WebDAV poskytuje SVN repozitar pres http protokol.  
davfs2, fusedav ... Umozni na linuxu namountovat WebDAV repozitar jak FS  
$SVN/conf/passwd ... definice uzivatelu  
$SVN/conf/svnserve.conf ... konfigurace svn serveru  

##### vytvoreni SVN repozitare

svnadmin create /home/user/projekt1 ... vytvori databazi produjtu v adresari /home/user/projekt1  
svn mkdir file:///home/user/projekt1/verze1 ... vytvori adresar vezre1 v /home/user/projekt1  
svn import soubor file:*/home/user/projekt1/verze1 ... naimportuje soubor do file:*/home/user/projekt1/verze1  
svnadmin create /home/user/projekt2 ... vytvori databazi produjtu v adresari /home/user/projekt2  
svn import adresar file:*/home/user/projekt2/verze1 ... naimportuje adresar i s podadresarema do file:*/home/user/projekt2  

==konfigurace WebDAV==

```
LoadModule dav_module         modules/mod_dav.so
LoadModule dav_svn_module     modules/mod_dav_svn.so
&lt;Location /svn&gt;

	DAV svn
	SVNParentPath D:/svn
&lt;/Location&gt;
```


##### Zaloha a oprava SVN repozitare

svnadmin dump /svn > backup.svn.dumpfile ... zazalohovani SVN repozitare do dump souboru  
svnadmin load /svn < backup.svn.dumpfile ... obnoveni zazalohovaneho SVN repozitare z dump souboru  
svnadmin recover ... opravi poskozenou Berkley DB SVN repozitare  

### SVN klient

##### Ziskani kodu - checkout

svn co file:*/home/user/projekt2/verze1 ... (prvotni stazeni projektu) vytvori adresar verze2 a stahne do nej vse z repozitare file:*/home/user/projekt2/verze1  
svn checkout http:*server/user/projekt1 . ... vytvori adresar projekt1 a stahne do nej vse z repozitare http:*server/user/projekt1 do aktualniho adresare  
svn co svn+ssh://1.2.3.4/project/a adresar ... stahne kompletni adresar project/a z ssh lokace (svn serveru) do adresare adresar (nikoli do projekt/a)  

##### Listovani, informace a porovnani objeku na lokale a repozitari

svn ls file:///home/user/projekt2/verze1 ... vylistuje adresar v repozitari  
svn list --verbose file:///home/user/projekt1/verze1 ... vylistuje adresar v repozitari i s detaily  
svn status ... porovna lokalni verze a verze v repzitari a napise jejich status  

svn diff ... vypise zmeny v zouborech oproti repozitari  
svn diff soubor --diff-cmd tkdiff ... graficke prohlizeni zmen  
svn info readme.txt ... informace o souboru readme.txt (revize atd.)  

##### Aktualizace zmen kodu a nahrani kodu do repozitare

svn commit soubor -m "komentar" ... updatuje soubor na SVN serveru (ktery je nadefinovan v .svn) (vytvori se pomoci checkout)  
svn ci soumor -m "dalsi commit" ... updatuje soubor na SVN serveru
svn add soubbor -m "komentar" ... prida soubor do repozitare, (ktery je nadefinovan v .svn - vytvori se pomoci checkout), ktery tam jeste neexistuje  
svn mv A B ... presune soubor A na B (v podstate udela cp + rm)  
svn rename A B ... prejmenuje soubor A na B (stejne jako svn ren, svn move, svn mv)  

svn resolve ... vyresi konflikty mezi lokalni verzi a verzi v repozitari  
svn rm soubor ... smaze soubor v repozitari i na lokale  
svn update ... updatuje lokalni soboru v aktualnim adresari a podadresarich z SVN serveru (data pro svn server se ctou z .svn)  
svn update -r 20 ... update lokalni verze podle repository na revizi c. 20  

##### Vlastnosti souboru v SVN

svn propset ... nastavi vlastnosti pro jednotlive soubory (napriklad ze se ingoruji SVNkem, ci keywords - doplneni textu misto $promenne$, napr. $id$)  
svn propget install.txt ... ukaze vlastnosti u souboru install.txt  
svn proplist * ... vylistuje promenne k urcitym objektum, napriklad ke vsem souborum  

##### Vytvoreni TAGu z TRUNK vetve

cd /path/to/project  
svn mkdir tags  
svn copy trunk/ tags/before-change  
svn commit -m "Tagged version before switching to Qt" tags/  
cd /tmp/
svn checkout file:///home/user/svn/project/tags/before-qt
