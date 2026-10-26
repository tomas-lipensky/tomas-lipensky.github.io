---
title: UNIX - C
---

so ... shared objects - sdilene knihovny  
.a ... staticke knihovny  
LD_LIBRARY_PATH ... cesta ke knihovnam  
LIBPATH ... cesta ke knihovnam  

ar -x libssl.a ... rozbali knihovny zabalene v archivu libssl.a  
ar -a -v libssl.so libssl.a ... zabali knihovnu libssl.so do archivu  
ld -rpath "/usr/local/ssl" -shared -o libssl.so *.o ... slinkuje knihoven *.o do libssl.so v adresari /usr/local/ssl  
lddd cesta/program ... ukaze, ktere knihovny uziva
