# azcli

## Azure CLI

az login ... pripojeni k Azure  
az account list --output table ... seznam predplatnyh  
az account set --subscription "Testovani" ... vyber predplatneho  
az account list-locations ... seznam lokaci  
az account show … ukaze kde jsem pripojeny  
az account show --query id … ukaze jenom subscription ID, kde jsem pripojeny  
az rest --method get --url "https://management.azure.com/subscriptions/XYZ/providers/Microsoft.Authorization/roleAssignmentScheduleRequests?api-version=2020-10-01" ... PIM  

## VM

az vm list ... seznam VM  
az vm list --query [*].[name,resourceGroup] ... seznam jen jmen a RG, vypis v tabulce  
az account list-locations ... seznam datacenter/lokaci  
az group create --name mojeRG --location eastus ... vytvori novy resource group  
az vm image list ... seznam obrazu  
az vm create --resource-group RGtlipensky --name VMtlipensky --size Standard_B1s --image UbuntuLTS --admin-username azureuser --generate-ssh-keys ... vytvori VM  
az vm delete --resource-group RGtlipensky --name VMtlipensky  
az account list-locations … seznam vsech lokaci  
az vm extension set --resource-group RG --vm-name VM  --name IaaSDiagnostics --settings public-settings.json … nastaveni rozsirujicich metrik pro monitoring a statistiky  
az vm run-command invoke -g RGSquidEA -n SquidEA02 --command-id RunShellScript --scripts 'hostname' ... spusteni linux prikazu na VM  

### konfigurace diagnostickeho nastaveni

$DS=az vm diagnostics get-default-config --is-windows-os | ConvertFrom-Json
$DS.storageAccount="satlipensky"
$storage_sastoken=az storage account generate-sas --account-name satlipensky --expiry 2037-12-31T23:59:00Z --permissions wlacu --resource-types co --services bt -o tsv
convertTo-Json -InputObject $DS -Depth 9 -Compress > config.json
az vm diagnostics set --settings json.json --resource-group  RGtlipensky --vm-name VMtlipensky

## storage account

az storage account create --name satlipensky --resource-group RGtlipensky ... vytovori storage account  

## Resource

az resource show --id "$ID" --query [id,location] --o tsv  
## AAD applikace

az ad app create --display-name "MyBuildTestApp1" --homepage "http:*/localhost/MyBuildTestApp1" --password "VerySecureLongStringHereToRepresetTheSecretForTheApp" --identifier-uris http:*/localhost/MyBuildTestApp1 ... vytvori AD Aplikaci  
az ad sp create-for-rbac -n "postman_ucet" … vytvori service principal s mymi pravy  
az ad sp reset-credentials --name "postman_ucet" … resetne heslo  
az ad sp create --id "bbbddd-aaa-43d0-8c34-b6ef52581b41" ... vytvori Service Principal pro zrovna vytvorenou aplikaci  
[az role assignment create](https://docs.microsoft.com/en-us/cli/azure/role/assignment) --assignee-object-id "dad4c094-1d9b-499c-9b38-71ce9eb7b4c8" --role "Reader" --scope "/subscriptions/00000" ... prida roli Reader pro uzivatele Service Principal ve zminenem subscription  
az login --service-principal --username "bbbddd-aaa-43d0-8c34-b6ef52581b41" --password "VerySecureLongStringHereToRepresetTheSecretForTheApp" --tenant "e46bc88e-1a4b-44ff-a158-1b9f7eb4561e" --allow-no-subscriptions ... pripoji se ro Azuru s kredenci Ser

## Site

az network public-ip list ... seznam verejnych IP adres  
az network lb outbound-rule create --address-pool MyAddressPool --frontend-ip-configs myfrontendoutbound --idle-timeout 5 --lb-name MyLb --name MyOutboundRule --outbound-ports 10000 --protocol Udp --resource-group MyResourceGroup ... nastavi outbound pravidlo  

## AKS - Azure Kubernetes Service

https://docs.microsoft.com/en-us/azure/aks/ssh - zpusob pripojeni se na AKS node  
`az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys` ... Vytvori AKS cluster  
`az aks install-cli` ... Stahne a nainstaluje kubectl  
`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster` ... Stahne a naistaluje kredence do kubectl (~/.kube/config)  
`az aks browse --resource-group myResourceGroup --name myAKSCluster` ... vytvori tunel do Web GUI pro kubectl\

## ACR - Azure Container Registry

az login --identity ... pripojeni do AZ  
az acr login --name ManiTempRegistry ... pripoji se k ACR  
az acr list ... seznam registru  
docker pull manitempregistry.azurecr.io/hello-world:01 ... stahne obraz z registru do dockru
