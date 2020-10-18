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

**Quick start tutorial - Provision an NGINX server using Docker on WSL2**

1. On last session, we have a lab for install Docker Desktop on [WSL2](https://github.com/neolin-ms/CSSOpenAzureCLIDocker). Confirm the Docker status on Windows 10. 
> Steps:<br> 
> ```bash
> Windows desktop > status bar > the hidden icons > Docker Desktop is Running<br>
> ```
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_5.png "1_5")<br> 
2. Creae a directory named `terraform-docker-demo`.
> Command:<br> 
> ```bash
>  neolin@tw-hslin-207a:~$ mkdir terraform-docker-demo && cd $_
> ``` 
> Output:<br>
> ![GITHUB](https://github.com/neolin-ms/CSSOpenTerraformAnsibleGithub/blob/main/TerraformImages/1_6.png "1_6")<br> 
3. Paste the following Terraform configuration into a file and name it `main.tf`.
> ```bash
> vi main.tf
>  terraform {
>   required_providers {
>     docker = {
>       source = "terraform-providers/docker"
>     }
>   }
> }
>
> provider "docker" {
>   host    = "npipe:////.//pipe//docker_engine"
> }
>
> resource "docker_image" "nginx" {
>   name         = "nginx:latest"
>   keep_locally = false
> }
>
> resource "docker_container" "nginx" {
>   image = docker_image.nginx.latest
>   name  = "tutorial"
>   ports {
>     internal = 80
>     external = 8000
>   }
> }
> ```
4. Intialize the project, which downloads a plugin that allows Terraform to interact with Docker.
> Command:<br>


**Create a Virtual Machine on Azure by Terrafrom**

## Lab2 - Ansible

## Lab3 - Git/Github

## References

1. [Get Started - Azure - Install Terrafrom](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/azure-get-started)
