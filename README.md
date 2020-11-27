# terraform-cheatsheet

## Alias
```bash
alias tf=terraform
```

## Terraform Plan
```bash
# pre-deployment plan
terraform plan
```

## Terraform Apply
```bash
# prompt before creating resources described in tf
terraform apply

# create resources without prompt
terraform apply --auto-approve

```

## Terraform Import
```bash
# import the azure storage account specified in tf
terraform import azurerm_storage.account.storage_account
```

## HEREDOC
```hcl
# input stream literal and redirect to command
# insert script from source for azure vm extension

extension {
    name                 = "${var.server_name}-extension"
    publisher            = "Microsoft.Compute"
    type                 = "CustomScriptExtension"
    type_handler_version = "1.10"

    settings = <<SETTINGS
    {
        "fileUris" : ["https://raw.githubusercontent.com/eltimmo/learning/master/azureInstallWebServer.ps1"],
        "commandToExecute" : "start powershell -ExecutionPolicy Unrestricted -File azureInstallWebServer.ps1"
    }
    SETTINGS
  }
```

## Count
```hcl
/* 
if the environment variable is equal to "prod"
then create 0(none), else create 1
*/
count = var.environment == "production" ? 0 : 1

/*
if the environment variable is equal to "prod"
then set allocation method to "static", else set to "Dynamic"
*/
allocation_method = var.environment == "prod" ? "static" : "Dynamic"

```

## Terraform Destroy
```bash
# destroy all
tf destroy 

# only destroy specific resource
tf destroy -target aws_instace.my_instance

```

## Logging
```bash
# enable trace logging
export TF_LOG=TRACE

# set log path to output to a file
export TF_LOG_PATH="terraform.txt"

```

## Comments
```hcl
/*
resource "digitalocean_droplet" "my_droplet" {
    image = "ubuntu-18-04-x64"
    name = "web-1"
    region = "nyc1"
    size = "s-1vcpu-1gb"
}
*/
```