# nokia_assignment

## Task >> Setup single server K8s cluster and deploy an application of your choosing (nginx container) into it.

## Asumption 
- Ansible control machine is up and running and it has ansible installed on it. 
- For my assignment I will be creating one in Azure Cloud and will document steps for that as well.
- I will be using azure cloud for completing my assigment, however azure related steps can be ignored while reviewing the assignment. I am using azure to practically deploy the k8s single node cluster. 
- In case infrastructure is already ready jump to
link: [Step 2 Configure single node k8s](#step-2-configure-single-node-k8s)

# Step 1 - (Optional)
This step is optional. In case we have 2 servers already available then we can directly jump to k8s setup.
## Make ansible control machine
For making ansible control machine in azure make sure you have azure cli installed on your machine.

```bash
az group create --name nokia_assignment-rg --location northeurope

az vm create \
--resource-group nokia_assignment-rg \
--name ansiblectrl \
--image OpenLogic:CentOS:7.5:latest \
--admin-username ansibleuser \
--admin-password <password> \
--vnet-name ansiblectrlVNET \
--subnet ansiblectrlSubnet

az vm show -d -g nokia_assignment-rg -n ansiblectrl --query publicIps -o tsv

```

Note the IP of virtual machine and login to VM using

```bash 
ssh ansibleuser@<ip of ansiblectrl>
```

## Install ansible on ansiblectrl and azure ansible module

Execute following command in order to install ansible and ansible azure module

```bash
yum install -y git
git clone https://github.com/pushpendera/nokia_assignment.git

cd nokia_assignment/azure_resources
chmod +x ansible-install.sh

./ansible-install.sh
```

Login to azure and do initial setup
```bash
az login
```
Follow instruction and complete login process. Now do initial setup as follow

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

paste following lines

```vi
[default]
subscription_id=<your-subscription_id>
client_id=<security-principal-appid>
secret=<security-principal-password>
tenant=<security-principal-tenant>
```

Now we are ready to create k8server machine.


# Step 2 Configure single node k8s



# Step 3 Deploy nginx in k8s
