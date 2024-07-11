## Project Title: ANOTHER METHOD OF INSTALLING AWS EKS
AWS-EKS-cluster--Helm 

### using Aws CLi,IAM,Eksctl,Helm charts  etc

 ### Requirement for provisioning Aws Eks cluster: 
 Spin up an ubuntu Ec2 instance in Aws of type t2 small
 connect to it through ssh connection from vscode or git bash or from your terminal if using mac

### Update the ubuntu image to latest version:

    sudo apt-get update && apt-get upgrade -y

### Install AWS CLI tool:

    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" 
    sudo apt install unzip 
    unzip awscliv2.zip 
    sudo ./aws/install
    aws --version 


### Install Kubernetes Kubectl:

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
    kubectl version 

### Install eksctl:

    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin
    eksctl version

### Install Helm (helm installation)

    curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
    sudo apt-get install apt-transport-https --yes
    echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
    sudo apt-get update
    sudo apt-get install helm

### From Script (Another installation option for helm)
 Helm now has an installer script that will automatically grab the latest version of Helm and install it locally.

 You can fetch that script, and then execute it locally. It's well documented so that you can read through it and understand what it is doing before you run it.

 $ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

 $ chmod 700 get_helm.sh

 $ ./get_helm.sh

 ### Now go to aws and install IAM user with accesskey and secretkey
 create user and create a role with adminstratorFullaccess (as policy  permision)
 download accesskey and secret key
 Now on your terminal or favourite IDE run
 aws configure

 accesskey:<enter your aws IAM user accesskey>

 secetkey:<enter your aws IAM user secretkey>

 Region:<enter your aws Region>

 formart:JSON

 ### Now check if you are authenticated to aws by runnig any of these commands

 $aws sts get-caller-identity

 $aws s3 ls

 $aws iam list-users



### Now create the cluster:

     eksctl create cluster \
                 --name eks-cluster-104 \
                 --version 1.30 \
                 --region eu-west-2 \
                 --nodegroup-name worker-nodes-group-104 \
                 --node-type t3.small \
                 --nodes 2
            
### Delete the cluster:

    eksctl delete cluster --name eks-cluster-104
    
