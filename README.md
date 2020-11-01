# CSSOpen - Session 4 - Lab1&2&3: Terraform, Ansible, Github

**Prerequisites**

- Azure subscription: If you don't an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin. 
- [Authenticate via Microsoft account](https://docs.microsoft.com/en-us/azure/developer/terraform/get-started-cloud-shell), then [set the current Azure subscription](https://docs.microsoft.com/en-us/azure/developer/terraform/get-started-cloud-shell#set-the-current-azure-subscription).

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
5. Run the terraform apply command to apply your configuration.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform apply
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_8.png "1_8")<br>
6. Validate the resource group by AzureCLI command.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ az group list --output table
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_9.png "1_9")<br>
7. Inspect the current state using `terraform show`.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform show 
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_10.png "1_10")<br>
8. Create a Linux VM with infrastructure in Azure using Terraform. Complete Terraform script, please refer [here](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/tf_main_example).
> 8.1 Create Azure connection and resource group<br>
> 8.2 Create virtual network<br>
> 8.3 Create public IP address<br>
> 8.4 Create Network Security Group<br> 
> 8.5 Create virtual network interface card<br>
> 8.6 Create storage account for diagnostics<br>
> 8.7 Create virtual machine<br>
9. Ensures that Terraform has all the prerequisites to build your template in Azure
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform init
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_11.png "1_11")<br>
10. Compares the requested resources to the state information saved by Terraform and then outputs the planned execution.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform plan
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_12.png "1_12")<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_13.png "1_13")<br>
11. Apply the template in Terraform.
> Command:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform apply
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_14.png "1_14")<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_15.png "1_15")<br>
12. The public IP address of your VM with az vm show.  
> Command:
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ az vm show --resource-group myTFResourceGroup --name myTFVM -d --query [publicIps] -o tsv
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_16.png "1_16")<br>
13. Then SSH to your VM, and verify the Ubuntu Linux version.
> Command1:<br>
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ ssh azureuser@{PUBLIC IP ADDRESS}
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_17.png "1_17")<br>
> Command2:<br>
> ```
> azureuser@myTFvm:~$ cat /etc/*release 
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_18.png "1_18")<br>
14. Use terraform destroy to remove infrastructure from your Azure cloud account. When prompted, type `yes` to execute this plan and destroy the infrastructure.
> Command:
> ```bash
> neolin@tw-hslin-207a:~/learn-terraform-azure$ terraform destroy
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_19.png "1_19")<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_20.png "1_20")<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_21.png "1_21")<br>

## Lab2 - Ansible

**Installing Ansible on Debian**
1. Add the following line to /etc/apt/sources.list:
> Command:<br>
> ```bash
> neolin@tw-hslin-270a:~$ vi /etc/apt/sources.list 
>      1 deb http://deb.debian.org/debian buster main
>      2 deb http://deb.debian.org/debian buster-updates main
>      3 deb http://security.debian.org/debian-security/ buster/updates main
>      4 deb http://ftp.debian.org/debian buster-backports main
>      5 deb [arch=amd64] https://download.docker.com/linux/debian buster stable
>      6 # deb-src [arch=amd64] https://download.docker.com/linux/debian buster stable
>      7 deb [arch=amd64] https://apt.releases.hashicorp.com buster main
>      8 # deb-src [arch=amd64] https://apt.releases.hashicorp.com buster main
>      9 deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main 
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/2_1.png "2_1")<br>


## Lab3 - Git/Github

## References

1. [Get Started - Azure - Install Terrafrom](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/azure-get-started)
2. [Create a Linux VM with infrastructure in Azure using Terraform](https://docs.microsoft.com/en-us/azure/developer/terraform/create-linux-virtual-machine-with-infrastructure) 
