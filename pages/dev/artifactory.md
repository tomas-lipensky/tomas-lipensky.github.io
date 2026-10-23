URL:

curl http://JFROG_URL/router/api/v1/system/ping ... ping, jestli je služba dostupná  

curl -u<USERNAME>:<TOKEN> http://JFROG_URL/artifactory/api/npm/auth ... ověření kredencí a získání bearer tokenu  
curl -H"Authorization: Bearer <BEARERTOKEN>" http://JFROG_URL/router/api/v1/system/ping ... užití bearer tokenu  
curl -H"Authorization: Bearer <BEARERTOKEN>" http://JFROG_URL/access/api/v1/tokens ... seznam tokenu  
curl -H"Authorization: Bearer <BEARERTOKEN>" -X POST -d "username=UZIVATEL" http://JFROG_URL/access/api/v1/tokens ... seznam tokenu pro uživatele UZIVATEL
