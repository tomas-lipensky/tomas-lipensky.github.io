## TFVC - Team Foundation Version Control

TFS - Team Foundation Server hostuje TFVC

### TEE - Team Explorer Everywhere

[https://github.com/microsoft/team-explorer-everywhere](https://github.com/microsoft/team-explorer-everywhere)  
Rider od JetBrains  

#### =TFS-CLI

[https://github.com/microsoft/tfs-cli](https://github.com/microsoft/tfs-cli)  
[https://docs.microsoft.com/en-us/azure/devops/repos/tfvc/use-team-foundation-version-control-commands?view=azure-devops](https://docs.microsoft.com/en-us/azure/devops/repos/tfvc/use-team-foundation-version-control-commands?view=azure-devops)  

#### Instalace

sudo apt install default-jre openjdk-8-jremkdir ~/bin  
update-alternatives --config java  
unzip Downloads/TEE-CLC-14.134.0.zip  
alias tf="`pwd`/TEE-CLC-14.134.0/tf"  

tf workspace -new ORGANIZACE -collection:https://ORGANIZACE.visualstudio.com ... registrace organizace, authentifikace  
tf wokrspaces ... listovani workspace  
tf changeset 420564 ... informace o changesetu  
tf dir -workspace:ORGANIZACE $/  
tf workfold -workspace:ORGANIZACE -map "$/PROJEKT" /project/PROJEKT ... zmapovani workspace s adresarem  
cd /project/PROJEKT; tf workfold ... ukaze informace o mappingu  
tf dir /adresar/podadresar ... vylistuje soubory/adresare  
tf get /adresar/podadresar ... stahne rekurzivne danou cestu  
tf getcs -changeset:420564 ... informace o changesetu  
tf info /adresar/podadresar ... indormace o souboru z TFVS (changeset, ...)  
tf checkin soubor1 soubor2 -comment:'komentar' ... checkin (commit) souboru  
[tf merge](https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2010/bd6dxhfy(v=vs.100)?redirectedfrom=MSDN) /recursive /version:C162489~C162489 "$/SourceBranch" "$/TargetBranch" ... merge z jedne vetve do druhe, pouzije changeset C162489, vyzaduje checkin(commit) k synchronizaci se serverem, je treba byt v rootu (adresar odkud jsou videt branche  

[tf checkin](https://docs.microsoft.com/en-us/azure/devops/repos/tfvc/checkin-command?view=azure-devops) -comment:"added readme"  ... udela commit (checkin)  

tf resolve -auto:AutoMerge ... kdyz konflikty, vyresi  
tf resolve -auto:TakeTheirs ... kdyz konflikty, vyresi, preferuje source branch  

### GIT-TFS

[https://github.com/git-tfs/git-tfs](https://github.com/git-tfs/git-tfs)
