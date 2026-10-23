ElasticSearch je produkt pro analytiku a prohledávání. Součástí je Kibana pro vizualizaci. Data jsou ukládána v indexech ve formě JSON. Pro ovládání a hledání nabízí REST API.

### REST API

#### Inicializace příkazové řádky

`export ELSRV="elasticsearch_https_adresa"` ... Nastaví adresu ve tvaru https://domenove.jmeno  
`export ELUSR="elasticsearch_uzivalel"` ... nastaví ElasticSeach uživatele  
`read -s ELPWD`  
`export ELPWD` ... nastaví ElasticSearch heslo  

#### Konfigurace, stav

`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/_cluster/settings?include_defaults=true&flat_settings=true%%` ... vypíše konfiguraci  
`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/INDEX/_cluster/state%%` ... Ukáže stav a informaci o clusteru  
`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/INDEX/_cluster/allocation/explain | jq .%%` ... ukáže informace o alokaci  
`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/INDEX/_cluster/health%%` ... ukáže informace o zdraví clusteru  

#### Indexy

`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/_alias%%` ... vylistuje indexy a jejich aliasy  
`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/INDEX/_settings%%` ... ukáže nastavení indexu INDEX  
`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/_cat/indices?v%%` ... seznam indexů, jejich stav a velikost  
`%%curl -s -u $ELUSR:$ELPWD -X PUT -H 'Content-Type: application/json' -d '{ "index": { "blocks.read_only" : true } }' https://$ELSRV/INDEX/_settings"%%` ... nastaví index na read-only  
`%%curl -s -u $ELUSR:$ELPWD -X POST https://$ELSRV/INDEX/_clone/KOPIE%%` ... naklonuje index INDEX do KOPIE  

#### Snapshoty

`%%curl -s -u $ELUSR:$ELPWD https://$ELSRV/INDEX/_slm/policy | jq .%%` ... ukáže snapshot policy  
`%%curl -s -u $ELUSR:$ELPWD -X POST https://$ELSRV/INDEX/_slm/policy/POLICY/_execute | jq .%%` ... provede snapshot pro policy POLICY
