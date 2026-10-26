---
title: Solaris - Sluzby
---

## Tisk

Start:
/usr/lib/lp/lpsched
Stop:
/usr/lib/lp/lpshut
admintool ... nastaveni tiskovych sluzeb
lpadmin ... prida, odebere, zmeni, ukaze tiskarnu, tiskovou frontu
enable, disable ... Zakaze razeni do fronty
lpstat ... status tiskove fronty
cancel, lprm ... zrusi tiskovou ulohu
lp, lpr ... tisk

## Audit

**status:**
ps -ef | grep auditd
**Ostatni**
audit ... zapne/vypne auditing, restartuje demona, zapise audit log soubor do jineho souboru
auditreduce ... Spoji audit log soubory
praudit ... prevede binarni kod log soubory do citelneho kodu
