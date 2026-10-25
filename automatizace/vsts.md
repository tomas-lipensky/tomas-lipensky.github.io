# vsts

## Azure DevOps (VSTS, VSO), TFS

Azure Devops, drive Visual Studio Team Services, nebo Visual Studio Online je online platforma pro  CI a CD
TFS (Team Service Foundation) je verzovaci system jako [GIT](dev/git) a [SVN](dev/svn)

### Odkazy

[dev.azure.com](https://dev.azure.com) - Azure Devops portal  
[https://status.dev.azure.com/](https://status.dev.azure.com/) ... Stav sluzeb a reportovani vypadku  
[https://developercommunity.visualstudio.com/](https://developercommunity.visualstudio.com/) - Uservoice for DevOps, Cisual studio etc - napady na nove funkce, hlasovani  
[https://azuredevopsdemogenerator.azurewebsites.net/](https://azuredevopsdemogenerator.azurewebsites.net/) - generator demo projektu pro ucebni ucely  
[https://github.com/microsoft/azuredevopslabs](https://github.com/microsoft/azuredevopslabs) - Laby na pripravu na AZ-400  
[https://azuredevopslabs.com/labs/vstsextend/](https://azuredevopslabs.com/labs/vstsextend/) ... priklady projektu na ruzne ue casy  
### Agent

[Instalace VSTS agenta](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/v2-windows?view=vsts)  
[docker run -e VSTS_ACCOUNT=UCET -e VSTS_TOKEN=TOKEN -it microsoft/vsts-agent](https://hub.docker.com/r/microsoft/vsts-agent/) ... Spusteni VSTS agenta v kontejneru  

### TFSSecurity.exe

[tfssecurity.exe](https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2013/ms252504(v=vs.120)?redirectedfrom=MSDN) /i "Team Foundation Administrators" /server:ServerURL ... nastroj obsazeny ve Visual studiu na praci s bezpecnostnim nastavenim, nepodporovany  
### AZCLI

az extension add --name azure-devops ... nainstaluje rozsireni AZCLI  
az devops configure -l ... ukaze kam jesem pripojeny  
az devops configure - organization=https://dev.azure.com/ORG ... vychozi nastaveni organizace  
az devops user show --user xxx@yy.com  
### Prikazy

vstsom/TF.exe ... Team Foundation Version Control Tool  
vstsom/TF.exe git help ... prace s GITem  
vstsom/TF.exe vs help ... prace s TF  
vstsom/TF.exe config help ... nastaveni  

### DevOps API

[DevOps Api reference](https://docs.microsoft.com/en-us/rest/api/azure/devops/?view=azure-devops-rest-5.0)  

curl -u UZIVATEL:KLIC https://dev.azure.com/oriflame/_apis/projects?api-version=2.0 ... seznam projektu  

### Konfigurace

#### Pipeline

[Nastaveni Timeoutu](https://developercommunity.visualstudio.com/content/problem/375541/60-minutes-time-limit-per-build.html)  
[Dokumentace k Pipeline](https://docs.microsoft.com/en-us/azure/devops/pipelines/scripts/powershell?view=azure-devops)  
[$Env:BUILD_SOURCEBRANCH](https://docs.microsoft.com/en-us/azure/devops/pipelines/build/variables?view=azure-devops&tabs=yaml) ... pouziti preddefinovane hodnoty v Powershellu  
[http://aka.ms/YAMLpipelines](http://aka.ms/YAMLpipelines) ... definice pipeline z YAML, [Video](https://azure.microsoft.com/en-ca/resources/videos/build-2019-yaml-release-pipelines-in-azure-devops/), [YAML schema](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=schema)  
[Vyrazy](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops) ... porovani, vyhodnoceni, zmenseni pisma atd  
$(System.AccessToken) ... PAT token uzivatele [project] Build Service ([organizce]), pod kterym probihaji pipeliny (buildy, deploye)  

### Rozsireni

Whitesource Bold ... rozsireni, ktere projde OpenSource knihovny a zkontroluje, jestli vyhovuji politice (nejnovejsi verze, nebo bez kritickych fixu, licence atd)  
Blackduck ... jako Whitesource Bold  
Octopus ... analyza kodu pro Java  
SonarQube ... analyza kodu pro .NET, C#  
[PMD](https://pmd.github.io/) ... Staticky kodovy analyzer -  nepouzite prommenne a objekty, prazdne catch bloky, copy/paste analyzer  
SonarCloud ... staticka analyza kodu  
Cobertura ... vypocita, kolik % java kodu je pokryto testy  
Selenium ... automatizace UI testu
