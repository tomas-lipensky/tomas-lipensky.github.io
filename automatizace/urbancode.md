# urbancode

### UrbanCode

Integracni a automatizacni nastroj (CI - Continuous Integration, Configuration management, Application Release Automation), puvodne [AnthillPro](https://en.wikipedia.org/wiki/AnthillPro), pote UrbanCode.  

Komponenty: UrbanCode Build, UrbanCode Deploy (uDeploy), UrbanCode Release  

### Odkazy

[developer.ibm.com/urbancode/](https://developer.ibm.com/urbancode/) ... domovska stranka  
[Male edu o mDeploy](http://w3.devops.ibm.com/devops/#/toolchain/advanced/ucd)  
[Objednani uDeploy na IBM Cloudu](http://w3.devops.ibm.com/devops/#/toolchain/onboard)  
[uDeploy na DW](https://developer.ibm.com/urbancode/products/urbancode-deploy/) - trial, info, architektura, atd.  
[developer.ibm.com/urbancode/blog/](https://developer.ibm.com/urbancode/blog/) ... blog projektu  
[UrbanCode Deploy with Patterns](http://www.ranger4.com/blog/bid/76646/UrbanCode-Deploy-with-Patterns) ... Ranger4.com - portal o DevOps  
[Porovnani UrbanCode s Jenkinsem a configuration managery](http://www.ranger4.com/blog/jenkins-chef-puppet-and-ansible-and-urbancode-devops-happy-together)  
[FAQ na DW](https://developer.ibm.com/answers/smart-spaces/23/urbancode.html)  
[SlideShare - UrbanCode Deploy course and product overview slides](http://www.slideshare.net/ibmrational/urbancode-deploy-course-and-product-overview-slides)  
[YouTube -  IBM UrbanCode Deploy 6.0.1 Concepts and Demonstration for Beginners ](https://www.youtube.com/watch?v=uDTmFFH24Xo)  
[DW - UrbanCode Release and Deploy Learning Roadmap](https://www.ibm.com/developerworks/mydeveloperworks/activities/service/html/mainpage#activitypage%2C657e717a-8c4a-4835-a1c1-c65fbd226103)  
[IBM UrbanCode Deploy: Building Continuous Delivery Pipeline](https://www.youtube.com/watch?v=ip9HxkZSGjw&t=314s) - ukazka UCD pipline  

### [uDeploy](http://www.ranger4.com/blog/bid/76893/What-is-UrbanCode)

- Automaticke deploye a rollbacky v pripade potreby
- deploy konfiguraci napric ruznymi servery, sluzbami, vrstvami
- Integrace s middlewarem, cloudem a virtualizaci
- prehled deployu, historie, reporting, bezpecnost, inventar
- Jednoduchy process designer - drag&amp;drop
- podpora skalovatelnosti, vysoke dostupnosti (HA)
- podpora procesu - schvalovani atd.
- [Agent / agentless deploye](http://www.ranger4.com/blog/bid/75183/Agents-to-be-or-not-to-be-in-IBM-UrbanCode)
- [Podpora pluginu](http://www.ranger4.com/blog/bid/75217/All-About-UrbanCode-Plugins), [pluginy ke stazeni](https://developer.ibm.com/urbancode/plugins/)

### Skoleni

[Youtube - uDeploy v4.8 3-day training (part 1 of 6)](https://www.youtube.com/watch?v=lUNPm1T0LHY)  
[Youtube - uDeploy v4.8 3-day training (part 2 of 6)](https://www.youtube.com/watch?v=0dPntG_svsE)  
[Youtube - uDeploy v4.8 3-day training (part 3 of 6)](https://www.youtube.com/watch?v=tNU5R10ReNY)  
[Youtube - uDeploy v4.8 3-day training (part 4 of 6)](https://www.youtube.com/watch?v=miLBQNRgl-c)  
[Youtube - uDeploy v4.8 3-day training (part 5 of 6)](https://www.youtube.com/watch?v=A1BP-dNog0w)  
[Youtube - uDeploy v4.8 3-day training (part 6 of 6)](https://www.youtube.com/watch?v=Azw6yw69G70)  
[UrbanCode and Jenkins Webcast](https://www.youtube.com/watch?v=slEQ88zDtzY)  

### [uRelease](http://www.ranger4.com/blog/bid/76893/What-is-UrbanCode)

- Na potlaceni rizik spojenych s vydavanim novych verzi
- Planovani, dohl/ed nad projekty, prehled verzi, analyza vlivu, lessons learned, zavislosti atd.

### udclient

udclient -username jsmith -password passwd -weburl https://myserver.example.com:8443 addTagToApplication -application JPetStore -tag Tag1 ... java interpret na
komunikaci s UCD pomoci REST API (/cli/), vystup v JSON  

### URL - REST API - /cli/

vystup v JSON, novy podporovany REST API

/cli/application.wadl ... definice REST API  
IP:8443/cli/applications ... seznam aplikace  
IP:8443/cli/component ... seznam component  
IP:8443/cli/resource  
/cli/application/environmentsInApplication?application=JPetStore" ... vylistuje prostredi v aplikaci  
Copy
https://IP:8443/cli/resource/tag?resource=/SYSTEM/lnx024  
https://IP:8443/cli/application/info?application=APLIKACE ... informace o aplikaci  

### URL - interni REST API - /rest/deploy

vystup v JSON, stary REST API pouzivany web portalem, nepodporovany IBM supportem

IP:8080/landscaper ...  IBM UrbanCode Deploy with Patterns server - design server  
IP:8443/rest/deploy/application ... [REST api](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.1/com.ibm.udeploy.reference.doc/topics/rest_api_ref_commands.html) - seznam aplikaci  
/rest/application.wadl  
IP:8443/rest/deploy/application/[import](https://developer.ibm.com/answers/questions/261232/how-to-import-a-component-into-ucd-via-the-command.html)?upgradeType=USE_EXISTING_IF_EXISTS&processUpgradeType=USE_EXISTING_IF_EXISTS”  
IP:8443/rest/deploy/application/AP_ID/export ... export aplikace do json  
/rest/deploy/applicationProcessRequest/table ...  
/rest/deploy/applicationProcessRequest/table[?filterFields=application.id&amp;filterValue_application.id=155d0e05-52e0-4d7b-87e2-8de4c684c7b8&amp;filterType_application.id=eq&amp;filterClass_application.id=UUID"](https://developer.ibm.com/urbancode/docs/paging-results-rest-api/) ... Filtrace  
/rest/deploy/applicationProcessRequest//properties  
IP:8443/rest/deploy/component ... seznam component  
/rest/deploy/version  
IP:8443/rest/deploy/component?[?filterFields=name&amp;filterValue_name=JPetStore&amp;filterType_name=like&amp;filterClass_name=String"](https://developer.ibm.com/urbancode/docs/filtering-results-rest-api/) ... Filtr na listovani  
IP:8443/rest/deploy/component?name=abcd ... informace o aplikaci se jmenem abcd  
:8443/rest/deploy/version  

### Procedury

promenne: ${d:PROMENNA} nebo ${PROMENNA}  
working dir: /opt/ibm-ucd/agent/bin
