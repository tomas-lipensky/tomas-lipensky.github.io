### Repozitáře

[https://dev.to/jajera/understanding-the-github-repository-2fpj|.github]] repozitář - šablony pro celou organizaci  

#### .github adresář

[speciální soubory v .github adresáři](https://medium.com/code-factory-berlin/github-repository-structure-best-practices-248e6effc405)  
[Copilot soubory](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions)  

### Akce

#### Runner

%%VERSION=2.311.0 curl -o actions-runner.tar.gz -L "https://github.com/actions/runner/releases/download/v${VERSION}/actions-runner-linux-x64-${VERSION}.tar.gz"%%  
tar xzf ./actions-runner-linux.tar.gz && rm ./actions-runner-linux.tar.gz  
%%./config.sh --url https://github.com/VFCZ-Digital/cicd-automation --token XXXX --runnergroup '' --name runner-1 --unattended --labels aws --replace%%  
sudo ./svc.sh install ... instalace služby  
sudo ./svc.sh start ... spuštění služby  

#### Struktura

definuje se v .github/workflows, napr. build_workflow.yml

```
name: JMENO
run-name: nepovinne - delší popis
on: push
env:
  promenna1: hodnota1
  
jobs:
 unikátní_název_jobu:
   runs_on: windows-latest
   outputs:
     cislo: ${{ steps.vystup.outputs.promenna }}
   steps:
   - run: echo "ahoj, promenna1: ${{env.promenna1}}"
   - run: echo "promenna=3" >> $GITHUB_OUTPUT
   - run: |
        echo "### Test Summary" >> $GITHUB_STEP_SUMMARY
     id: vystup
   - name: failure
     id: aaa
     run: exit 1
   - name: If block
     if: ${{ failure() && steps.aaa.conclusion == 'failure' }}
```

#### Proměnné

%%$![ CONTEXT]( CONTEXT.OBJEKT )%% ... Seznam contextů a objektů: [https://docs.github.com/en/actions/reference/workflows-and-actions/contexts](https://docs.github.com/en/actions/reference/workflows-and-actions/contexts)  
%%$![ github]( github.repository )%%  
%%$![ env]( env.MY_VARIABLE )%% ... jsou tam i výchozí proměnné [https://docs.github.com/en/actions/reference/workflows-and-actions/variables](https://docs.github.com/en/actions/reference/workflows-and-actions/variables)  
%%$![runner](runner.os)%%  
%%$![matrix](matrix.version)%% ... provede krok několikrát, doplní data ze sekce matrix pro každý běh jiná  
#### root sekce

##### on

%%push.branches: -master, 'releases/**'%% ... nastavení push requestu v určitých GIT větvích  
pull_request.branches: - master, develop ... pull requesty  
workflow_dispach: ... manuální spouštění  

##### workflow_call

[workflow_call](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

```
inputs:
  config-path:
    required: true
    type: string
secrets:
  token:
    required: true
```

workflow_call.outputs.PRVNI.description: "popis"  
workflow_call.outputs.PRVNI.value: %%$![ job.EXAMPLE.outputs]( job.EXAMPLE.outputs.output1 )%%

##### concurency

běh na více prostředích

%%concurency.group: environment-$![github](github.ref)%%  
concurency.cancel-in-progress: true  

##### jobs

#### job

runs_on: ubuntu-latest ... na jakém agentoviúworkeru job pojede  

outputs: ... vystupy  
outputs.vystup1: %%$![ steps.step1.outputs]( steps.step1.outputs.proměnná )%%  

if: github.ref_name == 'master' ... podmínka pro spuštění jobu  

stragegy: ... strategie  
strategy.matrix.target: [dev, stage, prod]  

permissions:  
permissions.contents: read  
permissions.pull-requests: write  

uses: octo-org/another-repo/.github/workflows/workflow.yml@v1 ... volání jiného workflow  
uses.with.config-path: .github/configdata.yml  
uses.secrets:envPAT: %%$![ secrets]( secrets.envPAT )%%  

steps:  
#### Kroky, steps

##### run

spustí příkaz, nebo příkazy  
shell: bash ... volba shellu, kde se to supustí  
%%echo "### Test Summary" >> $GITHUB_STEP_SUMMARY%% ... výstup do Job summary  
%%echo "image_tag=$![ github]( github.run_id)" >> $GITHUB_ENV%% ... výstup do GitHub proměnné pro další joby, nebo stepy  
%%echo $![ env]( env.image_tag )%% ... pozdější použití proměnné  

##### github

run: gh repo list aaa
env.GITHUB_TOKEN: %%$![secrets](secrets.token)%%

##### actions/cache

uses: actions/cache@v1.2.1  
with:  
with.path: ~/.m2 ... ve kterém adresáři se cachuje. ~/.m2 pro maven, %%**%%/node_modules pro node  
%%with.key: $![ runner]( runner.os )-cache%%  
with.restore-keys: ""  

##### actions/checkout

##### actions/setup-node@v3

with.node-version: '16'
with.registry-url: https://registry.npmjs.org/

##### actions/setup-java

with.java-version: '11'  
with.distribution: 'temurin'  
with.cache: 'maven'  

##### docker/setup-buildx-action

##### docker/login-action

with.username: %%$![ secrets]( secrets.DOCKER_USR )%%  
with.password: %%$![ secrets]( secrets.DOCKER_PWD )%%  

##### docker/build-and-push

with.context: .  
with.push: true  
with.tags: aa/bb:cc
