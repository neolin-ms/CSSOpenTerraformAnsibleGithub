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
> ```bash
> deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main
> ``` 
> Command:<br>
> ```bash
> $ sudo vi /etc/apt/sources.list 
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
2. Then run these commands:
> Command:
> ```bash
> $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
> $ sudo apt update 
> $ sudo apt install ansible
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_1.png "2_1")<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_2.png "2_2")<br>
3. Run the below command to verify the ansible version.
> Command:
> ```bash
> $ sudo ansible --verion
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_3.png "2_3")<br>
3. Install the pip, setuptools, packaging, msrestazure, and ansible[azure]. 
> Command:<br>
> ```bash
> $ wget https://bootstrap.pypa.io/get-pip.py
> $ sudo python get-pip.py
> $ pip install setuptools					 
> $ pip install packaging
> $ pip install msrestazure
> $ pip install ansible[azure]
> ```

**Create an Azure service principal with Azure CLI**
1. Enter the following command by replacing ServicePrincipalName with your desired value. It will give you a JSON output as shown in the image. Copy the output to notepad. This details required in your next tasks.
> Command:<br>
> ```bash
> $ az ad sp create-for-rbac --name ansibleservice
> ```

or

> Command:<br>
> ```bash
> $ az ad sp create-for-rbac --output json 
> ``` 
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_4.png "2_4")<br>
2. Enter the following command to get Azure SubscriptionID and copy the same to notepad.
> Command:<br>
> ```bash
> $ az account show 
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_5.png "2_5")<br>
3. Create Ansible credentials file
> Command:<br>
> ```bash
> $ cd ~/.azure
> $ vi credentials 
4. Insert the following lines into the file. Replace the placeholders with the service principal values.
> ```bash
> [default]
> subscription_id=<your-subscription_id>
> client_id=<security-principal-appid>
> secret=<security-principal-password>
> tenant=<security-principal-tenant>
> ```
> Save and close the file.
5. Define Ansible environment variables.
> Command:<br>
> ```bash
> $ export AZURE_SUBSCRIPTION_ID=<your-subscription_id>
> $ export AZURE_CLIENT_ID=<security-principal-appid>
> $ export AZURE_SECRET=<security-principal-password>
> $ export AZURE_TENANT=<security-principal-tenant>
> ```

**Test Ansible installation**
1. Create an Azure resource group. Save the following code as `create_rg.yml`. 
> Command:
> ```bash
> $ vi create_rg.yml
> ``` 
> YAML
> ```yaml
> ---
> - hosts: localhost
>   connection: local
>   tasks:
>     - name: Creating resource group - "{{ name }}"
>       azure_rm_resourcegroup:
>         name: "{{ name }}"
>         location: "{{ location }}"
>       register: rg
>     - debug:
>         var: rg
> ```
2. Run the playbook using ansible-playbook. Replace the placeholders with the name and location of the resource group to be created.
> Command:<br>
> ```bash
> $ ansible-playbook create_rg.yml --extra-vars "name=<resource_group_name> location=<resource_group_location>"
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_6.png "2_6")<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_7.png "2_7")<br>
3. Check the resource group by command.
> Command:<br>
> ```bash
> $ az  group list --output table
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_8.png "2_8")<br>

**Manage Linux virtual machines - Stop a virtual machine**
1. Check the VM status via Azure CLI.
> Command:<br>
> ```bash
> $ az vm show -g MYTFRESOURCEGROUP -n myVM -d --query powerState -o table 
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_9.png "2_9")<br>
2. Create a file named `azure-vm-stop.yml`, and open it in the editor.
> Command:<br>
> ```bash
> $ vi azure-vm-stop.yml
> ```
> YAML
> ```yaml
> - name: Stop Azure VM
>   hosts: localhost
>   connection: local
>   tasks:
>     - name: Stop virtual machine
>       azure_rm_virtualmachine:
>         resource_group: "{{ resource_group_name }}"
>         name: "{{ vm_name }}"
>         allocated: no```yaml
> ```
> Save the file and exit the edior.
3. Run the playbook using ansible-playbook.
> Command:<br>
> ```bash
> $ ansible-playbook azure-vm-stop.yml --extra-vars "resource_group_name=<resource_group_name> vm_name=<vm_name>"
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_10.png "2_10")<br>
4. Check the VM status via Azure CLI.
> Command:<br>
> ```bash
> $ az vm show -g MYTFRESOURCEGROUP -n myVM -d --query powerState -o table 
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_11.png "2_11")<br>

**Manage Linux virtual machines - Start a virtual machine**

1. Create a file named `azure-vm-start.yml`, and open it in the editor.
> Command:<br>
> ```bash
> $ vi azure-vm-start.yml
> ```
> YAML
> ```yaml
> - name: Start Azure VM
>   hosts: localhost
>   connection: local
>   tasks:
>     - name: Start virtual machine
>       azure_rm_virtualmachine:
>         resource_group: {{ resource_group_name }}
>         name: {{ vm_name }}
> ```
> Save the file and exit the editor.
2. Run the playbook using ansible-playbook.
> Command:<br>
> ```bash
> $ ansible-playbook azure-vm-start.yml --extra-vars "resource_group_name=<resource_group_name> vm_name=<vm_name>"
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/AnsibleImages/2_12.png "2_12")<br>


## Lab3 - Git/Github

## References

1. [Get Started - Azure - Install Terrafrom](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/azure-get-started)
2. [Create a Linux VM with infrastructure in Azure using Terraform](https://docs.microsoft.com/en-us/azure/developer/terraform/create-linux-virtual-machine-with-infrastructure) 
3. [Installing Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
4. [Manage Linux virtual machines in Azure using Ansible](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-managei)
5. [Create a service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest#create-a-service-principal)
