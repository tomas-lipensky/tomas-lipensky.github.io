---
title: HashiCorp Vault
---

## API

https://SERVER.cz:8200/ui/vault/storage/raft ... ukáže seznam nodá a který je aktivní  
/v1/sys/health ... stav o zdraví služby  

### Autentifikace

curl --request POST --data '{"role_id":"aaa","secret_id":"bbb"}' http://127.0.0.1:8200/v1/auth/approle/login ... pomocí App Role získá token  
curl --header "X-Vault-Token: AAA"  http://127.0.0.1:8200/v1/auth/approle/role/my-role/role-id ... vypíše role_id pro my_role  
curl --insecure -H "X-Vault-Request: true" -H "X-Vault-Token: AAA" "https://127.0.0.1:8200/v1/KVv2/data/cesta/cesta" ... čtení secretů z Vaultu typu Secrets v2, z cesty cesta/cesta  

## CLI

**[Proměnné prostředí](https://developer.hashicorp.com/vault/docs/commands)**  
export VAULT_TOKEN=aaa ... token pro autorizaci  
export VAULT_SKIP_VERIFY=true ... ignoruje nevalidní certifikát  
export VAULT_ADDR=https://vault.aaa.bbb ... nastavení URL pro vault server  
vault auth enable approle ... povolí app role  
vault write auth/approle/role/my-role token_type=batch token_ttl=20m ... vytvoří app roli  
vault read auth/approle/role/my-role/role-id ... vypíše App Role role_id  
vault write -f auth/approle/role/my-role/secret-id ... vygeneruje secret_id  
vault write auth/approle/login role_id=aaa secret_id=bbb ... pomocí App Role získá token  

### systém

vault secret list ... seznam včech secret enginu  
vault list auth/token/accessors ... seznam všech tokenů  
vault list identity/entity/id ... seznam entit  
vault list identity/entity/id ... seznam entit  
vault list identity/entity-alias/id ... seznam entit  
vault auth list ... seznam authentikačních mechanizmů  
vault auth enable -path="userpass-test" userpass ... povolí authentifikaci userpass  
vault login -method=userpass user=tomas ... přihlášení pomocí userpass  
vault policy list ... seznam policy  
vault policy read aaa ... ukáže definici policy aaa  
vault token capabilities secret/data/training_test ... informace o možnostech tokenu na daný objekt  
vault write -format=json identity/entity name="bob-smith" policies="base" metadata=organization="ACME Inc."  metadata=team="QA" ... vatvoří entitu  
vault write identity/entity-alias name="bob" canonical_id=$(cat entity_id.txt)  mount_accessor=$(cat accessor_test.txt)  custom_metadata=account="Tester Account" ... vytvoří entity alias  
vault audit enable file file_path=/var/log/vault.txt ... zapne auditing  
vault event subscribe kv-v2/data-write  
wss://VAULT:8200/v1/sys/events/subscribe/kv-v2/data-write  
wscat -H "X-Vault-Token: $(vault print token)" --connect 'ws://127.0.0.1:8200/v1/sys/events/subscribe/kv-v2/data-write?json=true'  

### Práce se secretama a hodnotama

vault kv delete aaa/bbb/ccc ... smaže hodnoty pro secret  
vault kv get -field config aaa/bbb/ccc ... vratí hodnotu pro klíc config v cestě aaa/bbb/ccc  
vault kv get -format=json  ... výstup ve formě json  
vault kv list java/list ... seznam secretů/složek  
vault kv metadata get java/list ... získá informace o složce včetně metadat  
vault kv metadata delete java/aaa ... smaže secret (složku)  
vault auth list ... seznam policy?  
vault read auth/token/lookup-self ... informace o tokenu  
vault read sys/policy  
vault print token ... vypíše hodnotu tokenu  

### Práce s Vault službou

vault operator step-down ... tento node přestane být hlavní node  
vault status -tls-skip-verify ... vypíše status služby, nekontroluje certifikáty  
vault operator unseal ... odblokuje node z maintenance modu  
vault operator rekey -init -key-shares=5  -key-treshold=3 ... vydá nonce kód nutný pro rotaci unseal hesel a root hesla  
vault operator rekey -nonce=aaaaa ... spustí se tolikrát, kolik je treshold, zadají je unikátní klíče a poté se vygenerují nové unseal klíče a operation nonce klíč pro generování root klíče  
vault operator generate-root ... zadají se 3 unseal klíče a vygeneruje se nový root klíč  

### Vault v Dockeru, backup/restore

docker volume create vault-volume  
docker run --rm -it --name vault_local --cap-add=IPC_LOCK -e VAULT_ADDR='http:*0.0.0.0:8200' -e 'VAULT_LOCAL_CONFIG={"storage": {"raft": {"path": "/vault/"}}, "listener": [{"tcp": { "address": "0.0.0.0:8200", "tls_disable": true}}], "default_lease_ttl": "168h", "max_lease_ttl": "720h", "ui": true, "cluster_addr": "http:*127.0.0.1:8201", "api_addr": "http://0.0.0.0:8200"}' -p 8200:8200 -v vault-volume:/vault hashicorp/vault:1.14.10 server  
docker cp vault-snap/vault-raft-2023-11-24-14-45-00.snapshot vault_local:/tmp  
docker exec -it vault_local /bin/sh  
vault status  
vault operator init  
vault operator unseal -tls-skip-verify  
vault login  
vault operator raft snapshot restore -force /tmp/vault-raft-2023-10-09-23-45-00.snapshot  
vault operator unseal -tls-skip-verify
