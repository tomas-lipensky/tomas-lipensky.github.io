### Argo CD CLI

argocd login URL ... --sso = SSO login  
argocd proj create PROJEKT  
argocd cluster add CONTEXT  
argocd app create APLIKACE --repo REPOURL --path CESTA_V_REPU --dest-namespace NAMESPACE --dest-server KUBE_API_URL  
argocd app sync  
argocd app history APP  
argocd app logs APP --container KONTEJNER
