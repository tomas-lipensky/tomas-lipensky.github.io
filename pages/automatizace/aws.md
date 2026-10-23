[https://health.aws.amazon.com/health/status](https://health.aws.amazon.com/health/status) ... informace o výpadcích v AWS  
[https://aws.amazon.com/](https://aws.amazon.com/)  

AWS CloudFormation template - textová definice na vytvoreni zdroju, jako ARM  
Stack .. skupina zdrojů spravovaná společně templatou v jednom regionu a accountu  
StackSet ... templatou spravovaná množina Stacků, které mohou být v různých regionech a accountech  

## AWS CLI

~/.aws/config ... Glogablí nastavení pro AWS CLI  
~/.aws/credentials ... kredence pro AWS CLI  
`aws configure` ... nastaví kredence do konfiguračních souborů, interaktivní vstup  
`%%aws configure --profile%% AAA` ... nastaví kredence pro profil AAA, může být název účtu  
`export AWS_PROFILE=AAA` ... nastaví pro aktualní shell profil AAA  
`export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE`  
`export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`  
`export AWS_DEFAULT_REGION=eu-central-1`  
`aws sts get-caller-identity` ... ukáže, jaké identitě patří token, který požívám v AWS CLI  
`aws sts assume-role-with-web-identity --role-arn ROLEARN --role-session-name SESSION1 --web-identity-token TOKEN` ... autentikace pomoci web tokenu  
`aws sts assume-role --role-arn ROLEARN --role-session-name SESSION1` ... spojení s novou rolí  

### IAM

`aws iam list-roles` ... seznam IAM rolí  
`%%aws iam list-attached-role-policies --role-name=role%%` ... zeznam přiřazených rolí  
`aws iam list-policies` ... seznam IAM policy  

### System Manager

aws ssm describe-parameters ... vylistuje parametry ze SSM  
aws ssm get-parameters --names /muj/moje ... vypíše hodnotu parametru  

### ECR Elastic Container Registry

`%%aws ecr describe-repositories%%` ... seznam ECR repozitářů pro AWS účet  
`%%aws ecr get-authorization-token%%` ... obdrží autorizační token v base64 tvaru (jméno AWS a heslo)  
`%%aws ecr list-images --repository-name%%`  ... vylistování obsahu ECR repozitáře  
`%%aws ecr get-login-password --region region | docker login --username AWS --password-stdin%%`  
`%%aws_account_id.dkr.ecr.region.amazonaws.com%%` ... nastaví token ECR pro Docker  

### EKS Elastic Kubernetes Service

`%%aws eks update-kubeconfig --region eu-central-1 --name czdxl-non-prod-infra-applicationeks --role-arn "ARN"%%`  

### VPC - Virtual Private Cloud - virtuální sítě

`aws ec2 describe-vpcs` ... seznam virtualních privátních cloudů (sítí)  

### AC2 - Elastic Cloud Compute - virtuální počítače

`aws ec2 describe-regions` ... seznam regionů  
`%%aws ec2 describe-instances --region eu-central-1%%` ... seznam EC2 instancí - virtuálních počítačů - v regionu  
`aws ec2 describe-subnets` ... seznam subnet  

### S3 - Storage - diskové uložiště

`%%aws --profile PROFIL s3 ls%%` ... vylistuje všechna S3 uložiště  
aws s3api list-buckets --query  'Buckets[?starts_with(Name, `hands-on-cloud-example`) == `true`].[Name]'   --output text  
`%%aws --profile aws-automation s3api list-buckets --query "Buckets[].Name"%%` ... další možnost vylistování  
`aws s3 ls s3:/BUCKET/ADRESAR1/ADRESAR2 --recursive --human-readible` ... vylistování obsahu S3 Bucketu  
`%%aws s3 mb s3://hands-on-cloud-example-2 --region us-east-2%%` ... vytvoří bucket  
`%%aws s3 rb s3://hands-on-cloud-example-2 --force%%` ... smaže neprázdný bucket  
`%%aws s3 rm s3://BUCKER/SOUBOR.png%%` ... smaže soubor  
`%%aws s3 sync s3:*ULOZISTE1/ADRESAR s3:*ULOZISTE2/ADRESAR --region us-west-2 --source-region us-east-1 --sse AES256  --delete%%` ... synchronizace bucketů  
`%%aws s3 mv s3:*ULOZISTE1/CESTA s3:*ULOZISTE2/CESTA --recursive%%` ... přejmenování, přesun  
`%%aws s3api put-object --bucket ULOZISTE --key ADRESAR/%%` ... vytvoření prázdného adresáře  
%%aws s3 cp s3://ULOZISTE/ADRESAR ./ADRESAR --recursive%% ... rekurzivní kopírování  
%%aws s3 cp ./ADRESAR s3://ULOZISTE/ADRESAR --recursive --exclude "*" --include "*.png"%% ... selektivní kopírování  
%%aws s3 cp ./SOUBOR.png s3://ULOZISTE --storage-class ONEZONE_IA%% ... ukládání na konkrétnní typ storage  

### Event Bridge

časovač - scheduler - cron

### Lambda

Joby ve formě v kontejnerů
### BeanStalk

hostovaní webových aplikací

### Systems manager (SSM)

Správa infrastruktury - automatické patchování atd.

### Cloudfront - CDN

### Secretsmanager

aws secretsmanager list-secrets ... vylistuje záznamy secretů  
aws secretsmanager get-secret-value --secret-id MojeHeslo ... vypíše hodnotu secretu  
aws secretsmanager get-secret-value --secret-id SECRET_IT --query SecretString --output text | jq -r .password ... vypíše heslo ve formě textu (bez zpětných lomítek). Zpracuje ho pomocí jq  

### Bedrock

aws bedrock list-foundation-models ... seznam dostupných modulů Bedrocku, včetně modelID a jejich možností  

##### =

Amazon Q =====
