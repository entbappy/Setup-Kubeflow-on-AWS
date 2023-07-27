# How to setup Kubeflow on AWS

## 1. Create an IAM User with the policies

```bash
AdministratorAccess
```

## 2. Launch an EC2 instance

```bash
# Amazon Machine Image (AMI) - Ubuntu

Ubuntu Server 20.04 LTS (HVM), SSD Volume Type

# Instance type

t2.large

# Storage size

60 gb atleast
```


## 3. Run the commands in the instance

```bash
sudo apt update

sudo apt-get update

sudo apt upgrade -y
```


## 4. Visit kubeflow website for the installation guide on AWS

[link](https://www.kubeflow.org/docs/distributions/aws/)
```bash
# Install the necessary tools:

- sudo apt install git curl unzip tar make sudo vim wget -y

-   export KUBEFLOW_RELEASE_VERSION=v1.7.0
    export AWS_RELEASE_VERSION=v1.7.0-aws-b1.0.2
    git clone https://github.com/awslabs/kubeflow-manifests.git && cd kubeflow-manifests
    git checkout ${AWS_RELEASE_VERSION}
    git clone --branch ${KUBEFLOW_RELEASE_VERSION} https://github.com/kubeflow/manifests.git upstream


- sudo nano Makefile  #check the jq version

- curl -sS https://bootstrap.pypa.io/get-pip.py | python3

- make install-tools

- cd /home/ubuntu/.local/bin/

- ls

- sudo mv * /usr/bin/

- cd /home/ubuntu/kubeflow-manifests/
```


## 5. Create an EKS Cluster

```bash
export CLUSTER_NAME=kubeflow
export CLUSTER_REGION=us-east-1
```

```bash
# set the AWS Access Key ID & Secret Access Key

aws configure
```

```bash
eksctl create cluster --name kubeflow --version 1.22 --region us-east-1 --zones us-east-1a,us-east-1b --nodegroup-name kubeflow-nodes --node-type t2.large --nodes-min 3 --nodes-max 4 --with-oidc
```

```bash
kubectl get nodes
```


## 6. Build Manifests and install Kubeflow

```bash
make deploy-kubeflow INSTALLATION_OPTION=kustomize DEPLOYMENT_OPTION=vanilla
```

```bash
kubectl get pods --all-namespaces
```


