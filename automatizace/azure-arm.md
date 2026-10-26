---
title: azure-arm
---

[http://armviz.io/](http://armviz.io/) - graficke zobrazeni ARM sablony + editor  
[ARM template](https://docs.microsoft.com/en-us/azure/templates/)  
[ARM - funkce pro retezce znaku](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-functions-string)  
[for-each look](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/copy-resources) aneb copy  
[Nested sablony](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-to-resource-group) aneb deploy do jine RG, subskripce atd.  

## Prikazy

az deployment group what-if --resource-group rginappserviceSTGEA --name inappnotificationstgea-blob-privlink --template-file ../../ArmTemplates/private_link.json --parameters @inappnotificationstgea-blob-privlink.json ... testove spusteni deploye, napise, co chce udelat  
az deployment group create --resource-group rginappserviceSTGEA --name inappnotificationstgea-blob-privlink --template-file ../../ArmTemplates/private_link.json --parameters @inappnotificationstgea-blob-privlink.json ... provede deployment
