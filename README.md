# AWS-EKS-cluster installations on an Ec2 instance in Aws using Aws CLi,IAM,Eksctl,Helm charts 

# Update the ubuntu image to latest version:

    sudo apt-get update && apt-get upgrade -y

# Install AWS CLI tool:

    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" 
    apt install unzip 
    unzip awscliv2.zip 
    ./aws/install
    aws --version 


# Install Kubernetes Kubectl:

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
    kubectl version 

# Install eksctl:

    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
    sudo mv /tmp/eksctl /usr/local/bin
    eksctl version

# Install Helm 

    curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
    sudo apt-get install apt-transport-https --yes
    echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
    sudo apt-get update
    sudo apt-get install helm

# Create the cluster:

     eksctl create cluster \
                 --name myEKS \
                 --version 1.21 \
                 --region us-west-1 \
                 --nodegroup-name worker-nodes \
                 --node-type t3.small \
                 --nodes 2
            
# Delete the cluster:

    eksctl delete cluster --name myEKS
    
