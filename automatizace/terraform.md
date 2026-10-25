Terraform je abstrakce pro konfiguraci infrastruktury (jak ARM, mozna Cloud Foundry, ...)

### Komponenty

tflint ... linter - zkontroluje kód a navrhne změny kvůli čitelnosti a standartizaci kódu  
terraform-doc ... automatické generování dokumentace  
Terratest ... testovani Tarraformovych sablon  
Terragrunt ... umí generovat terraformy podle terragrunt parametrů - terraform soubory jsou šablona s parametrama  
Yeoman ... pro praci s modulama  

#### soubory

main.tf ... povinny soubor, ktery se odkazuje na dalsi  
inputs.tf ... nadefinovane vstupni promenne  
terraform.tfvars ... pevne definovane vychozi promenne  
terraform.tfstate ... status nasazenych zdroju, muze obsahovat citlive udaje  

#### systémové proměnné

TF_LOG=TRACE ... úroveň logování, DEBUG, INFO, WARN, ERROR  
TF_LOG_CORE, TF_LOG_PROVIDER ... úroveň logování jednotlivých složek  
TF_LOG_PATH=./terraform.log ... logování do souboru  
TF_INPUT=0 ... vypne vstup  
TF_VAR_promenna=hodnota ... nastavení hodnoty proměnné pro tf soubory  
TF_WORKSPACE=prod ... nastavení workspace  
TF_DATA_DIR=/prod ... kde se nachárá .terraform složka  

#### prikazy

cd /adresar .. prejdu do adresare ktery obsahuje main.tf
terraform init ... vytvori si docasne soubory, kde si kompiluje tf soubory  
terraform validate ... overi syntaxi  
terraform plan ...  pokusi se udelat deployment na necisto  
terraform apply -autoapprove ... aplikuje zmenu, nevyzaduje schvalovani  
terraform apply --var-file=dev.tfvars -var user=tomas ... vezme vstupni parametry se souboru dev.tfvars a nadefinuje promennou user=tomas  
terraform apply --target='docker_service.vault[1]' ... naimplementuje změny pouze pro tento resource  
terraform destroy -auto-approve ... smaze, co je nadefinovano v terraform definici  
terraform import ... naimportuje do tfstate objekty z cloudu podle tf definic (objekty zminene v tf se nactou do tfstate  
terrafrom state rm azuread_service_principal.sp[3] ... odebere tento objekt z tfstate  
terraform state list ... seznam objektů v tfstate  
terraform state show vault_mount.volume ... ukáže nastavení daného objektu  
terraform show -json ... ukáže komplet tfstate, včetně secretů  
terraform force-unlock 9db590f1-b6fe-c5f2-2678-8804f089deba ... udemknutí tfstate, pokud předchozí terraform běh selže  

terraform workspace list ... vylistuje worspaces - prostřředí = instance tfstate souboru  
terraform workspace select prod ... vybere workspace prod a nastaví ho jako výchozí  

### tf moduly

[terraform-aws](terraform-aws)  

### tf soubory

#### locals {}

seznam_jmen = [for i in var.jmena: "$i.txt"]  

===variable "region" {}===

```
variable "muj_tuple" {
  description = "example tuple"
  type        = tuple([string, number, bool])
  default     = ["jablko", 1, true]
  validation {
    condition = length(var.name)
    error_message = "nespravna delka"
  }
}
```

##### datové struktury

list ... uspořádaný seznam hodnot stejného typu  
tuple ... uspořádaný seznam hodnot růžných typů  
set ... neuspořádaný sezname unikátních hodnot stejného typu  
map ... asociativní pole  
object ... seznam objektů  
toset()

#### output "timestamp" {}

#### import{}

#### moved{}

přejmenuje v tfstate (při refaktoringu objektů

moved {
from = resource.id
to = resource.id
}

#### remove{}

odstraní z tfstate (jako terraform state rm)

remove {
from = resource.id
lifecycle {
 destroy = false
}
}

#### provider {}

#### check {}

data ... ziská data pro test  
assert ... condition a error_message  

#### provisioner {}

local-exec  
remote-exec  
file  

#### resource {}

terraform_data ... třeba local  
null_resource  

for_each = toset(local.seznam_jmen) ... iterace celého resourcu

```
dynamic "statemen" {
  for_each = var.dpc_s3_designer-postfixes
  content {
    parametr = "${statement.value}"
  }
}
```
 ... iterace bloku v resourcu

```
lifecycle{
 precondition {}
 postcondition {}
}
```

timeout ... timeout pro ukončení aktivity na resourcu, zachrání to tfstate, když to ukončí něco z venku násilně  
provider = aws-we ... použití provideru s daným aliasem  

#### podmínky a iterace

count=var.istest == true ? 1 : 0 ... podmínka  
count=3 ... provede blok 3x  
for_each = [for i in local.instances: "i.name"]  

#### funkce

sensitive() ... obsah se považuje za důvěrný obsah, nezobrazí se ve výstuperch  
merge() ... sloučí mapy, poslední má přednost  
lookup(local.clovek, "vek", 12) ... vrátí buď hodnotu z mapy, pokud existuje, nebo default hodnotu  
trimsuffix("abcd", "cd") ... odřízne koncovku z řetězce, když se shoduje, v tomto případě vrátí ab  
base64encode() ... zakóduje řetězed co base64  
templatefile("a.tftpl", {a=["bb", "cc"]}) ... vezme hodnoty a a doplní je do vzoru z a.tftpl a vrátí to jako text  
file("a.txt") ... načte obsah souboru  
yamldecode(file("a.yaml")) ... dekóduje yaml do objektu  
join("-", ["aa", "bb"]) ... spojí řetězce, výsledek aa-bb  
concat(["a", "c"], ["b", "c"]) ... spojí seznamy, výsledek ["a", "b", "c"]  
formatdate("YYYYMMDDhhmmss", timestamp()) ... časová známka a formátování data  
endswith("abc.txt", ".txt") ... vrátí true, když 1. řetězec končí 2. řetězcem  
can ... true, když uvnitř platí  
contains("pes", local.savci) ... vrátí true, pokud je "pes" členem pole local.savci
