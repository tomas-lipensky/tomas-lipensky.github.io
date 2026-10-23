# Solaris - Sluzby

## Tisk

Start:<br />
/usr/lib/lp/lpsched<br />
Stop:<br />
/usr/lib/lp/lpshut<br />
admintool ... nastaveni tiskovych sluzeb<br />
lpadmin ... prida, odebere, zmeni, ukaze tiskarnu, tiskovou frontu<br />
enable, disable ... Zakaze razeni do fronty<br />
lpstat ... status tiskove fronty<br />
cancel, lprm ... zrusi tiskovou ulohu<br />
lp, lpr ... tisk<br />

## Audit

<b>status:</b><br />
ps -ef | grep auditd<br />
<b>Ostatni</b><br />
audit ... zapne/vypne auditing, restartuje demona, zapise audit log soubor do jineho souboru<br />
auditreduce ... Spoji audit log soubory<br />
praudit ... prevede binarni kod log soubory do citelneho kodu<br />
