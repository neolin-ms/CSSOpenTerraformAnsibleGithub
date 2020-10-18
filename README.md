# CSSOpen - Session 4 - Lab1&2&3: Terraform, Ansible, Github

## Lab1 - Terraform

**Install Terraform on Debian**

1. Add the HashiCorp GPG key.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~$ curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_1.png "1_1")<br> 
2. Add the official HashiCorp Linux repository.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~$ sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main" 
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_2.png "1_2")<br> 
3. Update and install.
> Command:
> ```bash
> neolin@tw-hslin-207a:~$ sudo apt-get update && sudo apt-get install terraform
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_3.png "1_3")<br> 
4. Verify that the installation worked by opening a new terminal session and listing Terraform's available subcommands.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~$  terraform -help
> ``` 
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_4.png "1_4")<br> 
5. Enable tab completion for Terraform commands, and then restart your shell. 
> Command:
> ```bash
> neolin@tw-hslin-207a:~$ terraform -install-autocomplete
> ``` 

**Create a Virtual Machine on Azure by Terrafrom**
1. Creae a directory named `learn-terraform-azure`.
> Command:<br> 
> ```bash
>  neolin@tw-hslin-207a:~$ mkdir learn-terraform-azure && cd $_
> ``` 
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_5.png "1_5")<br>
2. Paste the following Terraform configuration into a file and name it `main.tf`.
> ```bash 
> neolin@tw-hslin-207a:~/learn-terraform-azure$ vi main.tf
> ```
> The file contents:
> ```bash
> # Configure the Azure provider
> terraform {
>   required_providers {
>     azurerm = {
>       source = "hashicorp/azurerm"
>       version = ">= 2.26"
>     }
>   }
> }
>
> provider "azurerm" {
>   features {}
> }
>
> provider "azurerm" {
>   features {}
> }
>
> resource "azurerm_resource_group" "rg" {
>   name     = "myTFResourceGroup"
>   location = "westus2"
> }
> ```
3. Initialize your learn-terraform-azure directory in your terminal. 
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform init
> ``` 
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_6.png "1_6")<br>
4. Before you can create infrastructure, Terraform needs to generate an execution plan. Run the `terraform plan` command to view the execution plan for your configuration.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform plan
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_7.png "1_7")<br>


## Lab2 - Ansible

## Lab3 - Git/Github

## References

1. [Get Started - Azure - Install Terrafrom](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/azure-get-started)
