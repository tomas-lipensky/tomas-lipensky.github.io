# Azure DevOps

## Struktura

name: ... jméno pipeliny  
trigger: ... událost, která spustí pipelinu  
pool: ... v kterém poolu  
variables: ... proměnné  
resources: ... repozitáře pro checkout  
stages: ... jednotlivé kroky  

## Proměnné

echo "##vso[task.setvariable variable=TAJNA;issecret=true]$tasnost" ... nastavení tajné proměnné  
echo "##vso[task.setvariable variable=NORMALNI;]"hodnota"" ... nastavení proměnná  

## Tasky

bash  
task: PublishBuildArtifacts@1  
task: SecretsManagerGetSecret@1  
task: UniversalPackages@0  
download: current  
task: TerraformInstaller@0  
task: TerraformCLI@0  
task: AmazonWebServices.aws-vsts-tools.SystemsManagerGetParameter.SystemsManagerGetParameter@1
