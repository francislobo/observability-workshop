# Creating a virtual machine using AZURE for the purposes of installing the observability workshop stack. Alot of these instructions were taken from 
Parveeen Khan's blog post https://www.parveenkhans.com/2020/02/testing-tour-stop-10-pairing-up-on.html

## BackGround 
The observability workshop stack consists of ~ 8 microservices, each with database. There's also tools such as grafana, kibana, prometheus that assist in providing visibility to logging, tracing and metrics. 

The VM has a minimum requirement of 16GB of Memory 

OS:  Ubuntu. 
Instance Type: Standard D4s v3 (4 vcpus, 16 GiB memory)

We're assuming you are new to AZURE and don't have resource groups setup 

## Prerequisites

1) Create a free account on Azure
Sign up and get an account on Azure where the virtual machine will be created - https://azure.microsoft.com/. (I'd recommend you do this a few hours before you plan to start creating the VM. It felt that AZURE took a while to setup my account properly)  

2) Bash shell on your local computer 

3) SSH KEy 
1) Create an SSH Key for security purposes [full instructions here](https://docs.microsoft.com/en-gb/azure/virtual-machines/linux/quick-create-portal)
-Type 
``` bash
`ssh-keygen -t rsa -b 2048`
``` 
to create the ssh key.

- Press Enter to save in the default location, listed in brackets.
- Type a passphrase for your SSH key or press Enter to continue without a passphrase.
- Type:
``` bash 
cat ~/.ssh/id_rsa.pub
``` 
- you should see something like:
```` bash 
ssh-rsa ZZZZB3NzaC1yc2EAAAADAQABAAABAQCmgvFLEhF1hjtnbyeVi8DdM0idYLgncDDmxdFu6GrkWMimvpG1afJwAsUVbN9BwYlzgy9XJeBk+YAi1Nyu/nzxfZuYIfsWPawZB04G/2nZyZgR/0hVQjgPSdfuJYyIbxNubUqnja5sDx+pKZU5wXoJl4mxUMtJRfYcgfB+kd6icpnzcptcBvGvQ8ynVS/mSeD8TbLiN4eldRH65Q22+TgedxyEx+kS4EOXNTylt+P1sCAK2Ppa3nUxJoLHXhY/gua95n+NBdTEqcWrugFR2XTe7NnWNAZ2hdxa47Xdv2xwZsnL8FPxasvc1ljSovqIN9PsqQwxwJ6lPEq6SGULH+oj
````
- Copy and store this key (in a text file) for later 

## Create the VM on Azure  
- If you haven't already, login to the azure portal 
- Project Details 
-- Virtual Machine > Create a Virtual Machine > Add 
-- Resource Group > Create New > Observability
- Instance Details 
-- Virtual Machine Name: Observability
-- Region: <Your Region> 
-- Image: Ubuntu Server 16.04 TLS <or similar> 
-- Azure Spot Instance: No
-- Size: Standard D4s v3 <this is not default you will need to change> 
-Administrator Accoun t 
-- username: olly 
-- SSH public key (the one you generated and looks like a heap of scrambled text) 
-Inbound port rules
--HTTP(80, HTTPS(443), SSH (22) 

- Review and once validation has passed hit CREATE 
- Go back to Virtual Machine link and you should see your VM (Observability) there


## Test Connectivity 
- Go Virtual Machine > Observability > Connect > SSH > Test Connection 
You want a feedback message  "Network connectivity allowed" 

## Connect to the VM 
Next we want to connect and login to our VM. We need to login to install the workshop stack. 
- Go Virtual Machine > Observability > Connect > SSH 
- Ignore steps 1) and 2) 
- Step 3. Type in where your public key lives on your local machine. Mine was ~/.ssh 
- Step 4. Copy the command and paste into a bash shell on your local computer 
- Watch as you magically login to your account 
- Type the following to verify you are in your VM instance:
``` bash 
whoami 
``` 
- You are now ready to install the workshop stack 
