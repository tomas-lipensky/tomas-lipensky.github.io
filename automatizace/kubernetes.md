# Kubernetes

## Odkazy

[Changelog](https://github.com/kubernetes/kubernetes/tree/master/CHANGELOG) ... popis změn v jednotlivých verzích  

## Architektura

Kubernetes běží nad konternerizační službou, jako Docker, ContainerD, cri-o atd. Na omezování zdrojů pro pody se používá cgroups.

Master nody - CP nody - **Control plane nody** obsahují procesy:
* kube-apiserver - kontejner který příjímá všechna api volání, validuje je a předává dalším komponentám. Jediný má přístup do etcd
* etcd - kontejner který databaze stavu konfigurace, clusteru, sítě, storage atd., jediná persistentní komponenta, protože uchovává stav. Je etcd leader a followers, kterí replikují, případně převezmou roli leadra
* kube-scxheduler - kontejner který rozhoduje na kterých nodech poběží pod, binduje volumy atd.
* kube-controller-manager - kontejner který zjištuje stav objektů a když nesedí, tak je opravuje API instrukcema
* (coud-controller-manager - ccm) - volitelná komponenta - komunikuje s externími nástroji pro správu a reporting, předává zprocesované věci kubecontroler-managerem. Lze vyvinout vlastní
**Worker nody** - hostuje servisní pody:
* kubelet - proces, který komunikuje s kontejnerizační služnou a dohlíží a startuje pody a komponenty. Příjímá API volání pro Pod specifikace (PodSpec), konfiguruje pody, nahrává secrety, config mapy, mountuje volumy a vrací stav apiserveru, případně komunikuje s Topology manager komponentou pro extra featury jako akcelerace
* kube-proxy - kontejner který zajištuje komunikaci podů, služeb a endpointů pomocí iptables a ipvs (IP Virtual Server - ipvsadm)
* CoreDNS - kontejner který nahradil kube-dns, DNS služba rozšířítelná o puginy
* (supervisord) - pouze na systémech bez Systemd - monitoruje procesy, konternery a kontejnerizační službu

API zapisuje do ETCD, kube-scheduler to zpracovava a planuje workload. Node pooly - ruzne priority, napriklad podle ceny. Pody - schranky pro kontejnery s definicema/prepisama, co ma definovane limity, predpisy...  
skalovani, bud HPA (Horizotal Pod Autoscaler), podle statistik CPU a Mem, nebo custom metrkia, co jde do metric serveru, nebo VMSS (Virtual Machine Scaling Set), potrebuje featuru doinstalovat (v azuru i samo z Gui), ktera kontroluje vytizenost, node za cca 4 min)  
Nepouzivat ETCD misto zoo.. a jine - konfiguracni databaze (MDM), kvuli SLA.  
Podskalovani - zabije a spusti pody jinde  

Controllery - objekty, které komunikují s apiserverem  
Operatory - rozšíření, které slouží na ovládání služeb a zdrojů, např. endpoint, service, deployment, které spravují stejnojmenné zdroje:
* service - operátor, který dává endpointům fixní IP adresu a definuje pod policy. Komunikuje přes apiserver s kube-proxy a network pluginem
* deployment

#### Node

/etc/kubernetes/addons/ ... definice doplňků  
/etc/kubernetes/manifests/ ... definice podů  
registry.k8s.io/pause kontejnery ... pomocné kontejnery zajišťující kontinuitu síťového nastavení podů po restartu  

### Doplňky

Storage provisioner - poskytovatel trvalých diskových uložišť  
storageclass -  
Calico - síťový doplnek na toky mezi namespacema atd. používá Container Network Interface ([CNI](https://github.com/containernetworking/cni)), pody: calico-kube-controler a calico-node, příkaz calicoctl  
Flannel - Síťový plugin (CNI)  
WeaveNet - Síťový plugin (CNI)  
Romana - Síťový plugin (CNI)  
Kube-router - CNI  

#### Cilium

CNI - síťový firewall  
kubectl -n kube-system describe configmap cilium-config  

#### Karpenter

[Karpenter](https://karpenter.sh/docs/getting-started/getting-started-with-karpenter/) škáluje Kubernetes nahoru a dolů - nody
k get nodepool -n karpenter  

[Trivy](https://trivy.dev/) ... Trivy opensource image scanner - zjišťuje zranitelnosti obrazů  
`docker run aquasec/trivy image chainguard/kube-state-metrics`  
Istio - service mesh - doplnek na bezbecnost mezi podama (kdo s kym muze a nesmi)  
Gremlin ... doplnek na testovani bezpecnosti, provede utok na CPU, pamet a overi dobre nastaveni Kubernetes clusteru  
[Keda](https://keda.sh/) ... Kubernetes Event-driven Autoscaling - Event-based skalovani, umoznuje skalovani od 0 podu, skalovani podle http requestu, poctu zprav ve fronte atd.  
DAPR - Distributted APplication Runtime - nabizi okolni zdroje (aplikace - Service mash, hesla, storage, fronty) jako localhost:xxxxx/neco URL (sidekara k aplikaci)  
Osiris ... doplnek na skalovani od 0 podu  
[automatizace:helm](helm) templatovací jazyk pro kubernetes  
Knative serving ... skalovani od 0 podu, byuziva Istio  
Linkerd ... jak istio, nebo Aspen,, ale lehci  
[kustomize](https://kustomize.io/) ... Kubernetes configuration management, umí se odkazovat na sdílený kód mezi aplikacema, nepoužívá parametry (temlaty) jako helm  
[Kyverno](https://kyverno.io/) ... policy pro Kubernetes  
[Flagger](https://flagger.app/) ... rozhazovani trafficu na ruzne verze podu - AB testovani, canary, atd  
[NFS subdir external provider](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner)  
[stakater/reloader](https://github.com/stakater/Reloader) ... automatický restart podu, když se změní config mapa, nebo secret  
fluentd - logovaní služba na sběr logů. Kubernetes nedisponuje sbíráním logů  
prometheus - logování, monitoring, alerting  
OpenTelemetry - poskytuje tracing a metriky dalším nástrojům  
Jaeger ... konzumuje metriky  

#### Nástroje

minukube ... provoz Kubernetes na lokálním stroji  
kind ... instalace Kubernetes na lokálním stroji  
kubespray ... Ansible knihovna na instalaci k8s  
kops ... instalace k8s na aws  
kube-aws ... instalace k8s na aws  
Oktant ... Web GUI na spravu Kubernetes clusteru  
Lens ... Web GUI na spravu Kubernetes clusteru  
[Portainer](https://portainer.io) ... WebGUI na správu Kubernetes, Docker, Swarm atd.  
[kubernetes-dashboard](https://github.com/kubernetes/dashboard) ... Kubernetes Dashboard - WEB GUI na správu kubernetes  
k9s ... interaktivni GUI v konzoli na správu kubernetes  

##### Managovane Kubernetí clustery

AKS ... Azure Kubernetes Service  
EKS ... Elastic Kubernetes Services - Od Amazonu  
GKE ... Google Kubernetes Engine  
Google Anthos ... Mutli-cloud, nebo hybrid cloud management, ktery umi managovat Kubernetes on-prem  

#### parametry

label ... klíč=hodnota, používají se na selekce  
annotation ... anotace/popis - klíč=hodnoty - popisné hodnoty, nepoužívají se v Kubernetes, používají je třetí strany. change-cause například se použije v kubectl rollout history deploy  

#### Scheduler

Chování scheduleru lze konfigurovat sheduler profilama. Konfigurace pomocí apis/kubescheduler.config.k8s.io/v1/KubeSchedulerConfiguration. Profil pro scheduler lze vybrat v podu vlastností .spec.schedulerName. Je spoustu [|pluginů](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins) pro konfiguraci Extension points:

queueSort - jak jsou setřízené čekající (pending) pody  
preFilter - pre-procesing podů. může nějaké pody vyloučit z plánování  
Filter - výběr nodů vhodných pro pod. Pokud žádný node, tak se pod vyloučí z plánování  
postFilter - když nějaký plugin označí pod naplánovatelný, ostatní pluginy se už nevolají  
preScore  
Score - přiřazení skóre - scheduler nasadí pod s nejvyšším skórem  
reserve  
permit  
preBind  
Bind  
postBind  
multiPoint  

Filtry:
* ImageLocality - upřednostňuje nody obsahující daaný image. Extension points: score.
* TaintToleration - Implementuje taints a tolerance. Extension points: filter, preScore, score.
* NodeName - Kontroluje, zda Pod spec node name se shoduje s node. Extension points: filter.
* NodePorts - Zjišťuje, zda node node má k dispozici dané porty. Extension points: preFilter, filter.
* NodeAffinity - Implementuje node selectory a node afinitu. Extension points: filter, score.
* PodTopologySpread - Implementuje Pod topology spread. Extension points: preFilter, filter, preScore, score.
* NodeUnschedulable - Filtruje nody, které mají .spec.unschedulable = true. Extension points: filter.
* NodeResourcesFit - Zjišťuje, zda node má všechny potřebné zdroje.
* NodeResourcesBalancedAllocation - upřednostňuje nody, které by zjískaly lépe balancované zdroje, kdyby tam pod byl. Extension points: score.

* nodeName, nodeSelector - konkrétní node, nebo konkrétní skupina nodů s daným labelem
* affinity, anti-affinity - vhodnější nody - upřednostnění
* taint - vyloučení nějakých nodů pro pod, tolerance - ignorování taintu
* schedulerName - vybere profil scheduleru

spec.affinity.pod[Anti]Affinity.[required|preffered]DuringSchedulingIgnoredDuringExecution.labelSelector.matchExpressions:
* requiredDuringSchedulingIgnoredDuringExecution - nedá na node, pokud splněná podmínka
* preferredDuringSchedulingIgnoredDuringExecution - preferuje dané nody
* podAffinity - snaží se dát pody dohromady
* podAntiAffinity - snaží se dát na jiné nody

#### HA

* vše konfigurovat pomocí hostname, ne IP
* použít loadbalancery, TLS mít na Load balanceru, např. haproxy  (/etc/haproxy/haproxy.cfg)
* na přidáni dalšího Control Plane bude nejspíš potřeba přegenerovat klíče, budou expirované
* etcd lze použít externí, musí se udělat první (nonColocated etcd)
### DNS

SERVICE.NAMESPACE.svc.cluster.local  
cat /etc/resolve.conf ... ukáže IP [CoreDNS](https://coredns.io/manual/toc/#configuration) a domenu pro servisy  
dig @10.96.0.10 -x 10.96.0.10  
rewrite name regex (.*)\.test\.io {1}.default.svc.cluster.local ... k get cm -n kube-system kube-proxy -o yaml - přidá redirekt na doménu  

### Helm

Balickovaci system pro Kubernetes yamly (konfigurace), chart je balicek Helmu. Diky [Helmu](https://helm.sh/docs/topics/charts/) jsou pak YAMLy konfigurovatelne pomoci parametru a pro kazdy deploy na jine prostredi nemusi byt extra YALM soubor. Tiller byl agent v Helm <=2, ktery deployoval helm templaty do namespace pod systemovym ucivatelem, Helm v3 už Tiller nepoužívá.  

[https://hub.helm.sh](https://hub.helm.sh) ... Repozitar Helmovych balicku  

`helm version`  
`helm install --name ingress stable/nginx-ingress --debug` ... nainstaluje nový Helm chart - debug - ladící výstup  
`helm template . --name myrelease` ... vezme defaultni hodnoty a vytvori vystup ze sablony na stdout (pro kontrolu vystupu a syntaxe)  
`helm template . --name myrelease --set app.customvariable=aa,app.customnumber=2` ... jak predtim, ale vyzkousi vymenu parametru  
`helm upgrade --install myrelease . --set app.image.repository=${DOCKER_REGISTRY} --namespace x` ... nainstaluje, nebo updatuje  
`helm upgrade -i tester ealenn/echo-server --debug` ... instaluje, nebo upgraduje z repozitáře ealenn chart echo-server pod release name tester  
`helm ls` ... seznam nainstalovanych chartu  
`helm delete --purge aaa` ... smaze helm release  
`helm search hub redis` ... vyhledá v repozitáři [ArtifactHub](https://artifacthub.io/) vše pro redis  
`helm repo add bitnami ht‌tps://charts.bitnami.com/bitnami` ... přidá repozitář  
`helm repo list` ... vylistuje repozitáře  
`helm search repo bitnami` ... prohledává v repozitářích  
`helm fetch bitnami/apache --untar` ... stáhne a rozbalí helm chart  
`helm uninstall tester` ... odinstaluje helm release tester  

#### Struktura

Chart.yaml  
README.md  
values.yaml  
templates/_helpers.tpl

#### helm bloky

jsou uzavřené ve dvojitých složených závorkách `![]()`

`![ template "fullname" ]( template "fullname" . )`  
`![ .Chart]( .Chart.Name )-![ .Chart]( .Chart.Version )`  
`![ .Release]( .Release.Name )`  
`![ b64enc | quote ]( default "" .Values.mariadbRootPassword )`  

### Kubectl

[kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/#kubectl-context-and-configuration)  

`kubectl --v=10` ... maximální verbosita, ukáže i API volání ve formě curl příkazu  
`kubectl api-resources` ... seznam zdrojů, např. pod, deploy  
`kubectl explain pods.spec.containers` ... popis zdroje pod.spec.containers  

#### Konfigurace

`kubectl config view` ... ukaze konfiguraci kubectl  
`kubectl config get-contexts`  ... ukaze konfigurovane pripojeni  
`kubectl config current-context`  ... ukaze aktualni pripojeni  
`kubectl config view --minify -o jsonpath='{..namespace}'` ... ukaze vychozi namespace  
`kubectl config use-context my-cluster-name`  ... nastavi aktualni nastaveni  
`kubectl config set-context --current --namespace=NS` ... nastavi vychozi namespace  
KUBE_EDITOR="nano" ... nastavení editoru  
~/.kube/config ... konfigurace kubectl  
~/.kube/cache/discovery ... uložené předchozí hodnoty z běhu kubectl  
kubectl --kubeconfig ./admin.conf get nodes ... pusti kubectl s vlastnim configem  

#### Informace o clusteru

`kubectl api-versions`  
`kubectl api-resources`  
`kubectl cluster-info`  
`kubectl cluster-info dump` ... diagnostické informace o clusteru  
`kubectl version` ... informace o verzi klienta a K8S serveru  

#### events, ev

`kubectl get events` ... ukaze udalosti clusteru  
`kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name>`  
`kubectl get events --field-selector type!=Normal`  

#### namespace, ns, re

`kubectl get namespaces` ... seznam jmennych prostoru  
`kubectl create ns tomasovo` ... vytvoří nový jmenný prostor "tomasovo"  
`kubectl delete ns tomasovo` ... smaže jmenný prostor "tomasovo"  
`kubectl get resourcequota` ... ukaze quoty pro namespace (maximum prostředků CPU a paměti pro namespace)  
`kubectl get limitranges`  ... ukáže qóty pro pody v namespace (maximum prostředků pro jednotlivý pod)  

#### nodes

API objekt reprezentující server, na kterém jede virtualizace a komponenty kubernetes clusteru. Vznikne pomocí `kubeadm init` a `kubeadm join`. Pokud apiserver nemůže kontaktovat kubelet 5 minut, NodeLease  naplánuje smazání nodu a NodeStatus se změní z Ready

`kubectl get nodes` ... Seznam nodu  
`kubectl describe minikube` ... popíše node, včetně využití resourců a podů  
`kubectl top nodes` ... ukáže metriky podů  
`kubectl taint nodes --all node-role.kubernetes.io/control-plane-` ... odstraní blokování nodu pro control plane aktivity  
`kubectl taint nodes worker bubba=value:PreferNoSchedule` ... nodu worker přidá taint bubba:PreferNoSchedulle  

##### pods

Pod je jeden či více kontejnerů sdílející stejnou IP adresu, případně storage. InitContainers jsou kontejnery, které se spustí před sekcí Containers. Kontejnery spolu mohou komunikovat přes sdílený storage, IPC, nebo loopback zařízení. Sidecar kontejnery mohou zpracovávat logy, nebo API.

`kubectl cp /cesta/k/souboru NAMESPACE/JMENO_PODY:/cesta/k/souboru` ... kopirovani souboru z/na POD  
`kubectl describe pod aaaa -n nnnn` ... podrobne informace o podu  
`kubeclt edit po nginx` ... editace podu  
`kubectl exec -it aaa-6d5f854689-f28zp --namespace=default -- /bin/bash` ... spusti na danem podu bash  
`kubectl attach POD1` ... připojí se do podu POD1 do spušťeného procesu  
`kubectl debug POD1 --image debian --attach`  
`kubectl get pods`  
`kubectl get po nginx -w` ... sledování podu  
`kubectl get pods -o=jsonpath="{.items[*]['metadata.name', 'metadata.namespace']}"` ... vypíše jen název a namespace ve formátu json  
`kubectl get po nginx -o yaml --export` ... yaml s definicí podu, bez pod specifických informací  
`kubectl get pods.metrics.k8s.io` ... ukáže metriky podů  
`kubectl logs POD -n namespace` ... logy podu  
`kubectl logs --since=1h <pod_name>` ... za poslední hodinu  
`kubectl logs --tail=20 -f <service_name> [-c <$container>]` ... sledování logu (musí se přerušit ctrl-c) pro kontejner  
`kubectl logs --previous POD` ... logy posledního failnutého podu  
`kubectl run nginx --image=nginx --RM --restart=Never -- bash` ... vytvoří pod a spustí na něm příkaz, po skoncě  
`kubectl run nginx2 --image=nginx --port=80 --dry-run -o yaml` ... vypíše yaml pro pod, nespustí  
`kubectl set image pod/nginx nginx=nginx:1.15-alpine` ... změní verzi obrazu (upgrade)  
`kubectl top pods` ... ukáže metriky podů  
`kubectl port-forward mongo 28015:27017` ... přesměruje tok z podu na lokálí stroj, lze směrovat i z deploymentu, replicasety a servicy (deployments/aaa, ..)  
`kubectl get ep` ... seznam endpointu PODu a jejich IP adres - ip adresa dodaná kubeletem, nebo kube proxy  

#### deployments, deploy, replicasets, rs

Deploymenty řídí replicasety, tedy identické kopie podů

`kubectl create deploy --image=nginx --dry-run=client -o yaml` ... vytvoří a ukáže yaml šablonu pro deployment  
`kubectl get pod,deploy,rs -n default` ... seznam podu, deployu a replika setu v namespace default  
`kubectl get pod -L key1,key2, -l evn=prod` ... vylistuje pody které mají label env=prod, ukáže hodnoty labelu key1 a key2  
`kubectl edit deployment.v1.apps/nginx-deployment` ... editace deploye  
`kubectl rollout restart deployment/deploy1` ... predeployovani  
`kubectl rollout undo deployment/deploy1` ... navrat na předchozí verzi deploymentu  
`kubectl rollout undo deployment/deploy1 --to-revision=2` ... navrat na předchozí revizi 2  
`kubectl rollout history deployment shopping-cart-fs` ... seznam verzí k dispozici  
`kubectl rollout status deployment/deploy1` ... stav rolování deploymentu  
`kubectl rollout pause deployment/deploy1` ... pauza rolování deploymentu  
`kubectl rollout resume deployment/deploy1` ... Obnova rolování deploymentu po pauze  
`kubectl scale deployment sftp-la-service --replicas=1 -n default` ... skalovani  
`kubectl autoscale deployment AAA --min=2 --max=10` ... autoškálování  

`kubectl apply -f azure-vote.yaml` ... Deploy aplikace  
`kubectl teplace -f azure-vote.yaml --force` ... přenasazení aplikace ze souboru /po modifikaci souboru/  
`kubectl label pods POD novy-label=bbb` ... přidá label  
`kubectl label node AAA novy-label=ccc` ... olabeluje node  
`kubectl annotate pods POD anotace1=aaa` ... přidá anotaci  
`kubectl annotate pods --all description='Production Pods' -n prod` ... pridá popisek/anotaci všem podům v namespace prod  
`kubectl -n prod annotate pod webpod description-` ... smaže anotaci  
`kubectl rolling-update` ... Rolování změn replicasetu, nesmí spadnout sešna, jinak se nepovede  
`kubectl delete rs rs-one --cascade=orphan` ... smaže replicaset, ale podechá pody, které teď nic nespravuje, když se znovu vytvoří rs, bude je opět sprovavat  

#### horizontalpodautoscalers

automatické horizontálí škálování (nové pody) pro deploy, nebo statefulset

kubectl get horizontalpodautoscalers ... ukáže pravidla pro automatické horizontálí škálování  
kubectl describe hpa ... ukáže nastavení HPA  
`k patch scaledobject SERVICE-scaledobject --type=json -p='[{"op": "add", "path": "/metadata/annotations/autoscaling.keda.sh~1paused", "value": "true"}]'` ... pauzne škálování  
`k patch scaledobject apixproxy-connector-scaledobject --type=json -p='[{"op": "remove", "path": "/metadata/annotations/autoscaling.keda.sh~1paused", "value": "true"}]'` ... odpauzuje škálování  
`k patch ScaledObject SERVICE-scaledobject --type=json -p='[{"op": "replace", "path": "/spec/minReplicaCount", "value": 1}]'` ... změní škálování od 1 repliky  

#### replicaset, rs

`kubectl describe replicaset.extensions/aaa-6d5f854689 -n default` ... popis repliky podu  
`kubectl scale --replicas=3 rs/AAA` ... nastavení škálovaní pro replica set  

#### statefulset, sts

statefullset - spravované skupiny podů, které si zachovávají svoji identitu (pořadí podu, IP adresu, disk, node...)

`kubectl get statefulset`  

#### daemonsets, ds

Daemonset zajistí, že na každém nodu poběží kopie daného podu, např. služba disků, logů, monitoringu...  

`kubectl get daemonsets`  

#### horizontalpodautoscalers, hpa

API objekt, spravující metriky pro škálování a vyvolávání žádosti o přeškálování

#### secrets

`kubectl get secrets`  
`kubectl create secret generic secret1 -from-literal=username=devuser`  
`kubectl describe secrets/secret1`  
`kubectl delete secret secret1`  
`kubectl get secret client.crt -o jsonpath="{.data.tls\.crt}" | base64 -d | openssl x509 -text` #... ukaze certifikat ze secretu  

##### =configmaps

`kubectl get cm`  
`kubectl create configmap mysqlenv --from-literal=WORDPRESS_DB_HOST="mysql:3306"` ... vytvoří config mapu  
`kubectl create configmap mycm --from-literal=text=black --from-file=./favorite --from-file=./primary/"` ... vytvoří config mapu z textu, souboru a adresáře  

#### proxy

kubectl proxy --api-prefix=/ & ... vytvoří proxy na kubernetes API na lokální port, http://127.0.0.1:8001 např.  

==Ubuntu container for debugging==

```
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
  labels:
    app: ubuntu
spec:
  containers:
  - image: ubuntu
    command:
      - "sleep"
      - "604800"
    imagePullPolicy: IfNotPresent
    name: ubuntu
  restartPolicy: Always
EOF
```

kubectl exec -it ubuntu -- /bin/bash ... stahne a spusti ubuntu a na nem bash  

nebo

kubectl run mongosh --rm -i --tty --image ubuntu --overrides='{"spec":{"containers":[{"name":"awscli","tty":true,"stdin":true,"image":"amazon/aws-cli:2.13.6","command":["bash"],"resources":{"limits":{"cpu":"+100m","memory":"128Mi"}}}]}}'

#### services, svc, endpoints, ep

Síťový load balancer. Servisa je Kubernetes operátor běžící v kube-control-manažeru ovládající network driver a kube-proxy, nebo vytváří endpoint operátor.

`kubectl get service` ... seznam servis a jejich IP (adresu dodává Cilium - Kubernetes CNI wnetworking)  
`kubectl get service azure-vote-front --watch` ... Sledovani ap  
`kubectl expose rc nginx --port=80 --target-port=3100` ... Typ servisy - ClusterIP  
`kubectl expose deployment/nginx` ... vytvoří službu na pod pro daný deployment, pokud má definovaný "containerPort", jedná se o typ ClusterIP, slouží pro interní komuinkaci  
`kubectl expose deployment nginx --type=LoadBalancer` ... vytvoří servisu typu LoadBalancer - pro venkonvní komunikaci přes většinou přes cloud  
`kubectl expose deployment/nginx --port=80 --type=NodePort` ... servisa typu NodePort - přiřadí daný port na každé NodeIP  
`kubectl expose deployment/nginx --type=ExternalName` ... vytvoří CNAME na DNS  
`kubectl get ep` ... seznam endpointu PODu a jejich IP adres - ip adresa dodaná kubeletem, nebo kube proxy  

#### Ingress - Nginx frontdoor

Aplikační gateway pro servisu - umí např. terminovat tls. Nejčastěji [Nginx](https://github.com/kubernetes/ingress-nginx/blob/main/docs/deploy/index.md), ale existují i GKE, Traefik, Contour and Envoy. Ingres je pod, kterž poslouchá na API serveru v cestě /apis/networking.k8s.io/v1/ingresses a číhá na nové objekty. Když se objeví nový endpoint, nakonfiguruje tok na danou servisu

`kubectl get ingress`  

##### network policies

[Network policy](https://github.com/ahmetb/kubernetes-network-policy-recipes) jsou pravidla síťového firewalu. Některé CNI drivery NP nepoužívají, ale mají jiný způsob kontroly. Pokud je NetPol prázdná, neobsahuje egress, ani ingress, tak zakazuje tok. Pokud tam sekce je, tak povoluje tok. podSelector: {} = všechny pody.

`kubectl get networkpolicy -n namespace` ... seznam sitovych pravidel (firewall)  
`kubectl describe networkpolicy Policy1 -n namespace` ... popis sitovych pravidel  
`kubectl edit netpol access-nginx -n default` ... editace sitovych pravidel  
`KUBE_EDITOR='vim' kubectl edit netpol access-nginx -n default -o json` ... editace policy v VI ve formatu JSON  
`kubectl delete networkpolicy default-deny-all -n namespace` ... smazani sitoveho pravidla  

##### cornjobs, jobs

cronjob - časovač na spouštění jobů, job - jednorázová úloha - spuštění podu

`kubectl create job sleep --image=ubuntu  --dry-run=client -o yaml -- "sleep 5`  
`kubectl get cronjob` ... ukaze plany ukolu  
`kubectl get job --watch` ... sledovani jednotlivych jobu/ukolu  
`kubectl describe job JOBID` ... informace o jobu, na kterem kontejneru byl spusteny atd.  
pods=$(kubectl get pods --selector=job-name=JOBID --output=jsonpath={.items[*].metadata.name}) ... najde ktery pod odpovida danemu jobu  

##### certifikaty

`kubectl get certificate` ... seznam spravovanych certifikatu  
`kubectl describe certificate AAA` ... popis certifikatu AAA  

#### disky, persistent volume

`kubectl get pv`  
`kubectl get pvc` ... persistent volume claim  

#### serviceaccounts

`kubectl get serviceaccounts`  
`kubectl create sa admin-user` ... vytvoří service account  
`kubectl create token admin-user` ... vytvoří token pro service account  

#### Bezpečnost

##### Autorizace

Kontrolována Autorizačním controlerem API serveru, umí používat různé formy autentifikace, OpenID, certifikáty, tokeny

useradd user1  
passwd user1  
openssl genrsa -out ~user1/user1.key 2048  
openssl req -new -key ~user1/user1.key -out ~user1/user1.csr -subj "/CN=DevDan/O=development"  
sudo openssl x509 -req -in ~user1/user1.csr -CA /var/lib/minikube/certs/apiserver-etcd-client.crt -CAkey /var/lib/minikube/certs/apiserver-etcd-client.key -CAcreateserial -out ~user1/user1.crt -days 45  
kubectl config set-credentials DevDan --client-certificate=~user1/user1.crt --client-key=~user1/user1.key  
kubectl config set-context minukume-user1 --cluster=minikube --namespace=development --user=user1  

##### clusterroles, role, clusterrolebindings, role bindings - RBAC

Je kontrolována module authorization controllerem API serveru

`kubectl auth can-i --list` ... zobrazí, na co mám práva  
`kubectl auth can-i create deployments --as bob --namespace developer`  
`kubectl create token default` ... vytvoření tokenu  
`kubectl get rolebindings,clusterrolebindings`  
`kubectl create clusterrolebinding admin-user-access --serviceaccount=project1:admin-user --clusterrole=cluster-admin` ... přiřadí cluster roli pro service account  
`kubectl get clusterroles`  
`kubectl get roles`  

##### Admission Controler

PodSecurityPolicy - vynucení pravidel je od 1.25 nahrazeno Pod Security Admission. PSP/PSA je kontrolováno Admission Controlerem API serveru.
SecurityContext je nastavení bezpečnosti Podu pomocí SELinux/AppArmor. Je to sekce ve YAML definice

grep admission /etc/kubernetes/manifests/kube-apiserver.yaml  

#### poddisruptionbudgets

nadefinování rozmezí planovaných odstávek podů (napčíklad, že se může vypnout jen 2 podu naráz při plánované akci (migrace podů, deploy update, ...)

`kubectl get poddisruptionbudgets`

#### kubectl pluginy

kubectl [krew](https://krew.sigs.k8s.io/docs/user-guide/setup/install/) install whoami ... nainstaluje plugin whoami  
kubectl krew search ... seznam dostupných kubectl pluginů  
kubectl whoami ... spusti plugin, co ukaze, jaký uživatel jsem  
kubectl tail --rs staging/payment-1234 ... ukazuje logy ze všech podů replikasety  
kubectl sniff bigpod-abcd-123 -c mainapp -n accounting ... odposlech síťového provozu a přeposílání do Wiresharku  

### Další rozšíření

Rozšíření, kako třeba cilium, linkerd, jsou popsány v horní části stránky, crd s nimi pracuje

k get customresourcedefinitions.apiextensions.k8s.io ... zesnam API rozšíření  
kubectl get crd --all-namespaces ... kratší zápis  

cilium  
linkerd  
[https://cloud.google.com/knative|knative] ... nástroje pro rozšíření ovládáné - skálování od 0, škálování podle eventů atd.  
[https://tekton.dev/|tekon] ... CI/CD  
[https://argoproj.github.io/|agro CI/CD] ... CI/CD  
k get vulnerabilityreports.aquasecurity.github.io ... ukáže zranitelnosti obrazů  

### kubeadm

[https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/) ... instalace kubeadm, např. na node  
[https://github.com/kelseyhightower/kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way) ... podrobná instalace Kubernetes  

kubeadm-config.yaml:

```
apiVersion: kubeadm.k8s.io/v1beta3
kind: ClusterConfiguration
kubernetesVersion: 1.27.1
controlPlaneEndpoint: "k8scp:6443" #alias in /etc/hosts
networking:
  podSubnet: 192.168.0.0/16
```

`kubeadm init --config=kubeadm-config.yaml --upload-certs | tee kubeadm-init.out` ... inicializace kubernetes pomoci ClusteConfiguration souboru, vytvoří control plane (cp) node  
kubeadm config print init-defaults ... ukáže konfiguraci  
`kubeadm token create` ... vytvoří token  
`kubeadm token list` ... vylistuje certifikáty  
`openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/ˆ.* //'` ... vytvoří discovery token  
`kubeadm join --token zzz k8scp:6443 --discovery-token-ca-cert-hash sha256:xxx` ... přidá worker node  
`kubeadm join k8scp:6443 --token xx.zz --discovery-token-ca-cert-hash sha256:xxx --control-plane --certificate-key yyy` ... přidá nový control plane do clusteru  
`helm repo add cilium https://helm.cilium.io/; helm repo update; helm template cilium cilium/cilium --version 1.14.1 --namespace kube-system > cilium.yaml; kubectl apply -f cilium-cni.yaml` ... nastaví networking na Cilium  
`kubeadm version` ... verze Kubernetes  
`kubeadm config print init-default` ... vypíše konfiguraci  
`kubeadm upgrade plan` ... plan upgrade Kubernetes  
`sudo kubeadm upgrade apply v1.29.1` ... upgrade  
`sudo kubeadm upgrade node` .. upgrade worker nodu  

### cri-o - crictl

Container Runtime Interface - Orchestrator  

`crictl events` ... seznam událostí  
`cat /etc/crictl.yaml`  

### etcdctl

příkaz je k dispozici na nodu etcd

`etcdctl snapshot save` ... uloží etcd databázi (b+ strom) do souboru  
`etcdctlsnapshot restore` ... obnoví etcd databázi ze souboru  

### minikube

Podmínkou pro běh minikube je běžící docker démon  

`curl -Lo minikube ht‌tps://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64` ... stáhne nejnovější binárku  
`chmod +x minikube` ... dá práva na spuštění  
`sudo mv minikube /usr/local/bin` ... nakopíruje do bin  
`minikube start` ... spustí služku  
`kubectl get nodes` ... validace  
`minikube addons enable ingress` ... povolí ingress  

### Upgrade

`sudo apt update`  
`sudo apt-cache madison kubeadm` ... kuáže dostupné verze  
`sudo apt-mark unhold kubeadm` ... odfixuje verzi kubeadm  
`sudo apt-get install -y kubeadm=1.28.1-00` ... upgrade na danou verzi  
`udo apt-mark hold kubeadm` ... zafixuje verzi  
`sudo kubeadm version`  
`kubectl drain cp --ignore-daemonsets`  
`sudo kubeadm upgrade plan` ... ukáže aktuální a dostupnou verzi  
`sudo kubeadm upgrade apply v1.29.1` ... provede upgrade  
`kubectl get node` ... verze nodů  
`sudo apt-mark unhold kubelet kubectl`  
`sudo apt-get install -y kubelet=1.28.1-00 kubectl=1.28.1-00`  
`sudo apt-mark hold kubelet kubectl`  
`sudo systemctl daemon-reload`  
`sudo systemctl restart kubelet`  
`kubectl uncordon cp`  

### Troubleshooting

systemctl status kubelet.service  
journalctl -u kubelet  
sudo find /var/log -name "*apiserver*log"
/etc/systemd/system/kubelet.service.d/10-kubeadm.conf  
/var/lib/kubelet/config.yaml  
/etc/kubernetes/manifests/  
Zapnotut/prozkoumat API auditing  
Bezpečnostní problém? RBAC, SELinux, AppArmor  
Síťový problém - přidat ephemeral kontejner s network nástroji  
logy a status podu  
Probél na node?  
/var/log/kube-apiserver.log  
[https://kubernetes.io/docs/tasks/debug/debug-application/](https://kubernetes.io/docs/tasks/debug/debug-application/)  
[https://kubernetes.io/docs/tasks/debug/debug-cluster/](https://kubernetes.io/docs/tasks/debug/debug-cluster/)  
[https://kubernetes.io/docs/tasks/debug/debug-application/determine-reason-pod-failure/](https://kubernetes.io/docs/tasks/debug/debug-application/determine-reason-pod-failure/)  

### REST API

Dokumentace: [https://kubernetes.io/docs/reference/kubernetes-api/](https://kubernetes.io/docs/reference/kubernetes-api/). RC 409 - přepis aktuální verze (resourceVersion) není povolen. Nová verze v parametru modifiedIndex. Běžné HTTP metody: GET, POST, PATCH, DELETE, ...

```
current_context=$(kubectl config view -o json | jq -r '."current-context"')
user=$(kubectl config view -o json | jq -r '.contexts.[] | select(.name == "'${current_context}'") | .context.user')
cluster=$(kubectl config view -o json | jq -r '.contexts.[] | select(.name == "'${current_context}'") | .context.cluster')
certificate=$(kubectl config view -o json | jq -r '.users.[] | select(.name == "'${user}'") | .user."client-certificate"')
key=$(kubectl config view -o json | jq -r '.users.[] | select(.name == "'${user}'") | .user."client-key"')
ca=$(kubectl config view -o json | jq -r '.clusters.[] | select(.name == "'${cluster}'") | .cluster."certificate-authority"')
server=$(kubectl config view -o json | jq -r '.clusters.[] | select(.name == "'${cluster}'") | .cluster.server')
export token=$(kubectl create token default)
```

`curl ${server}/api/v1 --header "Authorization: Bearer $token" -k` ... autorizace pomocí tokenu  
`curl --cert ${certificate} --key ${key} --cacert ${ca}  ${server}/api/v1/pods` ... list of pods  
https://127.0.0.1:53479/api/apps/v1  
`curl --cert /Users/lipenskyt/.minikube/profiles/minikube/client.crt --key /Users/lipenskyt/.minikube/profiles/minikube/client.key --cacert /Users/lipenskyt/.minikube/ca.crt -H "Accept: application/json, */*" -H "Content-Type: application/json" -XPOST -d '{"kind":"SelfSubjectAccessReview","apiVersion":"authorization.k8s.io/v1","metadata":{"creationTimestamp":null},"spec":{"resourceAttributes":{"namespace":"default","verb":"create","group":"apps","resource":"deployments"}},"status":{"allowed":false}}' https://127.0.0.1:53479/apis/authorization.k8s.io/v1/selfsubjectaccessreviews` ... [|selfsubjectaccessreviews](https://kubernetes.io/docs/reference/kubernetes-api/authorization-resources/self-subject-access-review-v1/) informace, zna mohu vytvářet objekty typu deployment  

/apis ... seznam dostupných API  
/api/v1  
/api/v1/pods  
api/v1/namespaces  
/api/v1/namespaces/default/pods/mujpod  
/api/v1/namespaces/default/pods/mujpod/log  
/api/v1/namespaces/default/pods/mujpod/exec  
/apis/networking.k8s.io/v1/ingresses  
/apis/metrics/k8s.io/ ... metriky  
/apis/metrics.k8s.io/v1beta1/nodes ... metriky nodů  
/apis/metrics.k8s.io/v1beta1/pods
