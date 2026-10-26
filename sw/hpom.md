---
title: HP Operations Manager
---

## Start/stop/status:

PATH=$PATH:/opt/OV/bin # for AIX PATH=$PATH:/usr/lpp/OV/bin ... Prida do cesty HPOM binarky  
ovc -status ... status jaci agenti jedou  
ovconfget ... ukaze nastaveni klienta  
ovpolicy -list -host SUPETL11 ... ukaze nastaveni politiky  

## Lokace

/var/opt/OV/bin/instrumentation ... skripty  
/var/opt/pepsov/conf ... konfigurace
