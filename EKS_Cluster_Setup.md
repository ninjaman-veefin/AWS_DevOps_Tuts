
## 1. Create EKS Cluster ##

1) Launch new Ubuntu VM using AWS Ec2 ( t3a.micro ) 

2) Connect to machine and install kubectl using below commands

```

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin

kubectl version --short --client

```

3) Install AWS CLI latest version using below commands

```

sudo apt install unzip

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install

aws --version

```

  

4) Install eksctl using below commands

```

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin

eksctl version

```

### 2. Create IAM role & attach to EKS Management Host ##

  

1) Create New Role using IAM service ( Select Use case - EC2 )

2) Add below permissions for the role <br/>

- Administrator - acces <br/>

3) Enter Role Name (eksroleec2)

4) Attach created role to EKS Management Host (Select EC2 => Click on Security => Modify IAM Role => attach IAM role we have created)

  

###  3. Create EKS Cluster using eksctl ##

```

eksctl create cluster \
  --name my-test-eks-cluster \
  --region ap-south-1 \
  --version 1.33 \
  --nodegroup-name standard-workers \
  --node-type t3.medium \
  --nodes 3 \
  --nodes-min 1 \
  --nodes-max 4 \
  --managed

```

### **Note:** This process uses AWS CloudFormation in the background and will take **15–20 minutes** to complete 

```

kubectl get nodes

```


### We are done with our Setup ###

###  4. Delete the Cluster ###

  

```

eksctl delete cluster --name my-test-eks-cluster --region ap-south-1

```