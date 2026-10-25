# citrix

## Citrix client

### prikazy

/opt/Citrix/ICAClient/wfica -desc "GEMB Remote desktop II" ... pripoji se k serveru definovanem timto popisem v appsrv.ini  
/opt/Citrix/ICAClient/wfica a.ica ... pripoji se k serveru definovanem v tomto souboru  
/opt/Citrix/ICAClient/wfmgr ... manazer ulozenych spojeni  

### Konfiguracni soubory

~/.ICAClient/wfclient.ini ... obecne chovani Citrix klienta  
~/.ICAClient/appsrv.ini ... nastaveni zalozek na vzdalene Citrix servery  
*.ica ... soubory obsahujici wfclient a appsrv cast pro 1 konkretni pripojeni - vetsinou se obdrzi z webu  

[Parametr v ICA souborech na nemazani souboru po spusteni](http://kb.mit.edu/confluence/display/istcontrib/How+to+make+a+Citrix+ICA+file+permanent)
