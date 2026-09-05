## 3 Tier Application Deployment on EKS

#### AWS CLI Installation
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin --update
```

#### Docker Installation
```
sudo apt-get update
sudo apt install docker.io
docker ps
sudo chown $USER /var/run/docker.sock
```

#### kubectl Installation
```
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
```

#### eksctl Installation
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

#### Setup Cluster on EKS using eksctl

```
eksctl create cluster --name threetier-cluster --region ap-south-1 --node-type t2.medium --nodes-min 2 --nodes-max 2
```
It takes 15-20 mins to fully setup cluster  

Let CLI know to work with which cluster
```
aws eks update-kubeconfig --region ap-south-1 --name threetier-cluster
``` 

#### Cleanup
* To delete the EKS cluster:
> eksctl delete cluster --name threetier-cluster --region ap-south-1
