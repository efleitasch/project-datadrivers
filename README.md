# Probeaufgabe
- Create a Pipeline in Azure DevOps using terraform to deploy Data Lake Storage and Data Factory in Azure

## Prerequisities
- A subscription ID in Azure
- A Service principal in Azure that has `Owner` rights for the subscription (to be able to manage role assignments)
- Create a service connection in Azure Devops to Github (https://github.com/settings/tokens)
 

1. login to azure and set correct subscription
```
az login -u <your AAD credentials>
az account set --subscription <subscription in>
```

2. store the secret values in Azure DevOps Pipeline as secret variables
```
Azure DevOps Variables:
subscription_id             = <subscription_id>
client_id                   = <client_id>
client_secret               = <client_secret>
tenant_id                   = <tenant_id>
service_principal_object_id = <service_principal_object_id>

Powershell:
$env:ARM_SUBSCRIPTION_ID=<SUBSCRIPTION_ID>
$env:ARM_TENANT_ID="_TENANT_ID"
$env:ARM_CLIENT_ID="CLIENT_ID" 
$env:ARM_CLIENT_SECRET="CLIENT_SECRET"

Unix:
export ARM_SUBSCRIPTION_ID=<SUBSCRIPTION_ID>
export ARM_TENANT_ID="_TENANT_ID"
export ARM_CLIENT_ID="CLIENT_ID" 
export ARM_CLIENT_SECRET="CLIENT_SECRET"
```


3. install the following apps for azure pipelines from azure marketplace 
```
Terraform 1 (https://marketplace.visualstudio.com/items?itemName=ms-devlabs.custom-terraform-tasks)
Terraform 2 (https://marketplace.visualstudio.com/items?itemName=charleszipp.azure-pipelines-tasks-terraform)
```

4. Terraform Commands
```
terraform init
terraform validate
terraform plan --var-file=env/<environment>/variables.tfvars --var-file=secrets/secrets.tfvars -out="<environment>.tfplan"
terraform apply "<env>.tfplan"
terraform destroy --var-file=env/<environment>/variables.tfvars --var-file=secrets/secrets.tfvars #-auto-approve
```
