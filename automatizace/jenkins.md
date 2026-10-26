---
title: Jenkins
---

Integracni nastroj postaveny na Jave (frontend bezi na Tomcatu). Podporuje SCM (Source Contrl Management):  
AccuRev, CVS, Subversion, Git, Mercurial, Perforce, Clearcase and RTC  
a ruyne typy nasazeni: Apache Ant, Apache Maven, shell a batch skripty  

[Male edu o Jenkins](http://w3.devops.ibm.com/devops/#/toolchain/advanced/jenkins)  
[Prezentace o Jenkinsovi](http://www.slideshare.net/dstine4/jenkins-and-chef-infrastructure-ci-and-automated-deployment)  

## Dokumentace

JENKINS_URL/env-vars.html ... popis preddefinovanych promennych  
/queue/api/  
/api  
/script ... scriptovaci konzole  
/jnlpJars/jenkins-cli.jar ... stáhne jenkins-cli.jar pro Jenkins CLI  

## Jenkins CLI

java -jar jenkins-cli.jar -s http://jenkins-test.oskarmobil.cz/ -noCertificateCheck -http -auth user:password  groovy = <plugins.groovy  
## API

curl -u UZIVATEL:TOKEN -k https://SERVER/cesta  
curl -u $juser:$token -k https://SERVER/job/CESTA/job/JOB/1201/doDelete -v -X POST ... smazání buildu  

https://SERVER/job/SLOZKA/job/SLOZKA/job/JOB/457/api/json ... informace o jobu 457 v json formě  
https://SERVER/job/SLOZKA/job/SLOZKA/job/JOB/457/api/xml ... informace o jobu 457 v XML formě  
xml?xpath=/*/*[0] ... selekce pomocí xpath  
xml?tree=jobs[name],views[name,jobs[name]] ... podobjekt  
json?tree=jobs[name]  
json?tree=jobs[name]{0,10} ... 0 až 10 prvek z pole  
json?depth=4  
json?pretty=true&tree=result ... hezký výpis a výpis pouze objektu result  
python?pretty=true  
https://SERVER/job/SLOZKA/job/SLOZKA/job/deployer/457/consoleText ... výstup z konzole jobu 457 v textové formě  
https://SERVER/job/SLOZKA/job/SLOZKA/job/deployer/457/consoleFull ... výstup z konzole jobu 457 v HTML formě  
https://SERVER/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins ... seznam pluginů a jejich verzí  
### Skripty Groovy

[Groovy](https://groovy-lang.org/documentation.html) jazyk  
[Environment variables](https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#using-environment-variables) ... výchozí hodnoty prostředí Jenkinse, přistupuje se k nim přes ${env.WORKSPACE}  

### Kostra kódu

kdekoliv může být definice proměnné, ne jen v environment sekci:
def skipPublishDefault = (BRANCH_NAME == 'hotfix') ? true : false ... podmíněná definice

```groovy
@Library([path])
pipeline {
  agent none //
  options {}
  triggers {}
  parameters {}
  environment {}
  stages {
    stage {}
    stage {}
    post {}
  }
  post {}
}
```

nebo když se nedefinuje akce souborem ale v UI:

```groovy
node {
  stage {}
  stage {}
}
```

#### sekce agent

label "docker" || "linux" ... selekce agenta podle labelu  

any ... jakykoliv

none ... žádný agent se nealokuje

node {} ... jak label, ale umožňuje další možnosti, vice na [https://www.jenkins.io/doc/book/pipeline/syntax/](https://www.jenkins.io/doc/book/pipeline/syntax/)

```groovy
docker {
image 'maven:1.2.3'
label 'moje'
args '-v /tmp'
registryUrl 'https://myregistry.com/'
registryCredentialsId 'myPredefinedCredentialsInJenkins'
}
```

dockerfile {} ... vice na [https://www.jenkins.io/doc/book/pipeline/syntax/](https://www.jenkins.io/doc/book/pipeline/syntax/)

```groovy
kubernetes {
                            label "android-slave-dynamic"
                            defaultContainer "android-slave"
                            yaml libraryResource("agents/android-agent.yaml")
                        }
```

#### tools

sekce v pipeline, nainstaluje pro běh na agentovi nástroj dané verze: maven, jdk, gradle

#### sekce triggers

cron cron('H */4 * * 1-5') ... časové spouštění

pollSCM('H */4 * * 1-5')

upstream(upstreamProjects: 'job1,job2', threshold: hudson.model.Result.SUCCESS) ... když skončí specifikované joby specifikovaným tresholdem

#### sekce options

Parametry celkového běhu, komplet popis viz [https://www.jenkins.io/doc/book/pipeline/syntax/](https://www.jenkins.io/doc/book/pipeline/syntax/)

disableConcurrentBuilds()  
buildDiscarder(logRotator(numToKeepStr: '40', artifactNumToKeepStr: '40'))  
timeout(time: 3, unit: 'HOURS')  
timestamps ()  

#### sekce parameters

vstupní parametry pro běh pipeliny

`string name: 'SERVICE_NAME', description: 'Service name.', trim: true` ... textový parametr  
`choice name: 'ENVIRONMENT', choices: ['dev', 'stg'], defaultValue: 'NotProvided', description: 'Target environment.'` ... výběr  
''booleanParam name: 'PIPELINE_REFRESH', description: """
OPTIONAL
Reload this pipeline from pipeline definition, parameters etc."""'' ... pravda, nepravda, popis na víc řádků  
text(name: 'BIOGRAPHY') ... víceřádkový text  
password(name: 'PASSWORD') ... heslo - skryje se v logu  

#### sekce environment

Proměnné, přistupuje se k nim přes ${TARGET}

KLIC = 'hodnota'  
SETTINGS_XML = credentials('maven_settings') ... mžnost použít i secret text  

#### sekce stage

agent {} ... viz sekce agent  
when {} ... podmínka, kdy step jede a jestli  
environment {} ... viz sekce environment  
options {} ... parametry pro stage, jako trřeba timeout, více na [https://www.jenkins.io/doc/book/pipeline/syntax/](https://www.jenkins.io/doc/book/pipeline/syntax/)  
input {} ... uživatlský vstup  
stages {} || parallel {} || matrix {} || steps {} ... obsahuje max. 1 z uvedených  
try {} catch () {}  
for (int i = 0; i < browsers.size(); ++i) { echo "${pole[i]} " }  

#### sekce when

beforeAgent true  
expression { !params.SPUSTIT && BRANCH ==~ /(dev|test|PR-.*)/ }  

#### sekce steps

script {} ... umožnuje vnořit akce, včetně smyček atd.  
if (sharedTools.shouldRun("build")) {} .. podmínka, provede akce v {} když je podmínka spněna  
dir('android') {} ... provede akce v {} v adresáři android  
script {} ... posloupnost akcí v {}  
echo '' ... nativni Jenkins funkce pro echo  
sh 'echo ahoj' ... shell skript  

withCredentials() {} ... obsah {} se provede s kredencema načtenýma ze secretu, přiřazenýmá do proměnné  
withCredentials([file(credentialsId: "AA${BB}", variable: 'VAR')]) { writeFile file: '.env.'+ ENV_TYPE.toLowerCase(), text: readFile(VAR) }  
withCredentials([ string(credentialsId: 'AA', variable: 'BB'), string(credentialsId: 'CC', variable: 'DD') ]) { echo "${CC} ${DD}"}
withCredentials([ usernamePassword(credentialsId: 'dxl-cz-github-user', usernameVariable: 'username', passwordVariable: 'password') ]) {sh 'git remote set-url origin "https://${username}:${password}@github.vodafone.com/VFCZ-DXL/${microserviceName}.git"' }  
withNPM(npmrcConfig: 'npmrcs-cz') {} ... použije file npmrcs-cz a udělá z něj .npmrc  
checkout([$class: 'GitSCM', branches: [name: 'develop'](name/ 'develop'), extensions: [$class: 'CleanBeforeCheckout']($class/ 'CleanBeforeCheckout'),userRemoteConfigs: [credentialsId: 'secret1',url: 'https://user@github.bbb.com/ccc/ddd.git'](credentialsId/ 'secret1',url/ 'https///user@github.bbb.com/ccc/ddd.git')])  
withDockerRegistry([credentialsId: 'aaa', url: "https://REPOSITORY"]) ... provede docker login s kredencema

```groovy
configFileProvider([fileId:'conf_file', variable:'soubor']) {
      script {
        echo "Ctu soubor '${soubor}' ..." 
        servers = readJSON(file:soubor)  } }
```

#### sekce post

Je buď ve sekci pipelines, nebo steps, více viz [https://www.jenkins.io/doc/book/pipeline/syntax/](https://www.jenkins.io/doc/book/pipeline/syntax/). Je to jako step, ale záleží na okolnostech:

always {} ...vždy  
changed {} ... jen když se změnil status od minulého běhu (success > fail např.)  
fixed {} ...  
regression {} ...  
aborted {} ... jen, když se běh přeruší  
success {} ... jen když vše bylo v pořádku  
unstable {} ...  
unsuccessful {} ...  
cleanup {} ... poslední step, provede se po všech ostatních post krocích, ať dopadly jakkoli  

#### Definice funkcí

def call(body) {def pipelineParams = [:] } ... definice funkce v knihovně. 1 soubor = jedna funkce, název funkce = název souboru, např. /vars/aaa.groovy, funkce aaa(parametr1=2), pipelineParams.parametr1 je vstupní parametr s hodnotou 2
