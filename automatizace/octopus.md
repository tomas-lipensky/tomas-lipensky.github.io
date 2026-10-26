---
title: Octopus
---

## Agent - Tentacle

### Instalace

$URL='https://download.octopusdeploy.com/octopus/Octopus.Tentacle.3.24.0-x64.msi'  
$output = "C:\Windows\Temp\Octopus.Tentacle.3.24.0-x64.msi"  
Invoke-WebRequest -Uri $url -OutFile $output  
. $output  
msiexec /i $output /quiet  

### Ziskani otisku prstu ze serveru

C:\Program Files\Octopus\Tentacle\Tentacle.exe show-thumbprint --instance "Tentacle" --nologo  

### Inicializace

cd "C:\Program Files\Octopus Deploy\Tentacle"  
./Tentacle.exe create-instance --instance "Tentacle" --config "C:\Octopus\Tentacle.config" --console  
./Tentacle.exe new-certificate --instance "Tentacle" --if-blank --console  
./Tentacle.exe configure --instance "Tentacle" --reset-trust --console  
./Tentacle.exe configure --instance "Tentacle" --home "C:\Octopus" --app "C:\Octopus\Applications" --port "10933" --console  
./Tentacle.exe configure --instance "Tentacle" --trust "YOUR_OCTOPUS_THUMBPRINT" --console
netsh advfirewall firewall add rule "name=Octopus Deploy Tentacle" dir=in action=allow protocol=TCP localport=10933  
./Tentacle.exe register-with --instance "Tentacle" --server "https://OCTOPUS_SERVER" --apiKey="API-xxxxx" --role "Management" --environment "Management" --comms-style TentaclePassive --console  
./Tentacle.exe service --instance "Tentacle" --install --start --console

## Nastroje

octopack ... zabali cely framework .NET aplikaci z CI build procesu  
[octo.exe](https://octopus.com/docs/packaging-applications/creating-packages/nuget-packages/using-octo.exe) ... dalsi balickovaci nastroj na .NET aplikace, vice flexibilni  
[octopus.server.exe](https://octopus.com/docs/octopus-rest-api/octopus.server.exe-command-line/configure) ... nastroj na konfigurace Octopus Deploy serveru  
## Promenne

[Systemove promenne](https://octopus.com/docs/deployment-process/variables/system-variables)  

## Octopus API

[https://octopus.com/docs/api-and-integration/api](https://octopus.com/docs/api-and-integration/api)  
URL/api  
URL/swagger  

Invoke-RestMethod -Method GET "https://octopus.ori/api/authentication" -Headers @{"Accept"="application/xml"}  
curl -X GET "https://octopus.ori/api/authentication" -H  "accept: application/json"
