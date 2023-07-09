# Deploy_Helm_Chart_EKS

![helm and EKS](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/0e0f0d80-80ed-4983-a658-8aebe0d59e4e)

# What is Helm?🤔
Helm is a package manager for Kubernetes applications that includes templating and lifecycle management functionality. It is essentially a package manager for Kubernetes manifests (such as Deployments, ConfigMaps, Services, etc.) that are grouped into charts. A chart is just a template for creating and deploying applications on Kubernetes using Helm. Charts are written in YAML and contain metadata about each resource in your app (e.g., labels, values, etc.). A chart can be used by itself or combined with other charts into composite charts which can be used as templates for creating new applications or modifying existing ones. Helm essentially allows you to manage one chart for your environment.

# What is EKS?
![K8s+aws=EKS](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/7733edde-fb50-46bb-933a-5ffb4ca8fcca)

Amazon Elastic Kubernetes Service (Amazon EKS) is a managed Kubernetes service that makes it easy for you to run Kubernetes on AWS and on-premises. Kubernetes is an open-source system for automating the deployment, scaling, and management of containerized applications. Amazon EKS is certified Kubernetes-conformant, so existing applications that run on upstream Kubernetes are compatible with Amazon EKS.
Amazon EKS automatically manages the availability and scalability of the Kubernetes control plane nodes responsible for scheduling containers, managing application availability, storing cluster data, and other key tasks.
Amazon EKS lets you run your Kubernetes applications on both Amazon Elastic Compute Cloud (Amazon EC2) and AWS Fargate. With Amazon EKS, you can take advantage of all the performance, scale, reliability, and availability of AWS infrastructure, as well as integrations with AWS networking and security services, such as application load balancers (ALBs) for load distribution, AWS Identity and Access Management (IAM) integration with role-based access control (RBAC), and AWS Virtual Private Cloud (VPC) support for pod networking.


```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
```
![1-key](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/3ee34041-d8c1-441e-a1b2-9163a4ee6126)

```
sudo apt-get install apt-transport-https --yes
```
![2-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/d7b98f8a-976f-40ab-8562-b892e822d5b1)

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
```
```sudo apt-get update```

```
sudo apt-get install helm
```
## Step 2: Install AWS CLI on Ubuntu

```
 sudo curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```
![4-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/9a8b50e2-3e29-4ee5-8c62-e4dd7991bf95)

`apt-get install unzip `

`sudo unzip awscliv2.zip`

`sudo ./aws/install`
![5-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/55f0261d-b221-4f9d-9d78-cac4f29df5c7)

## Step 3: Install eksctl CLI tool for creating EKS clusters on AWS

```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```

```
sudo mv /tmp/eksctl /usr/local/bin 
```
![6-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/d0662421-e7ea-41eb-953a-c890b6f4b528)

## Step 4: Install kubectl binary with curl

```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

![7-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/5b505ee2-e835-4ced-9401-cec5d1e3ebf4)

`sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl`

![8-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/d0ab967b-c78c-469b-8866-106c3676018d)

## Step 5: Configure AWS CLI

`aws configure`

## Step 7: Create Amazon EKS cluster using eksctl

```
eksctl create cluster --name dhruvcluster --region ap-south-1 --version 1.27 --nodegroup-name linux-nodes --node-type t2.micro --nodes 2
```
![9-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/dd610090-2530-4adf-9662-70dd6e926f7c)

`kubectl get nodes`

![image](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/a0e02754-9b7a-4f1c-9273-62a7ec024821)
![11-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/18b0bf05-fd03-4ab5-8c10-1b69db3a7275)

## Step 8: Deploy Helm Chart on EKS cluster

`helm create dhruvcluster`

![12-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/033a6875-b292-4871-8e29-d6dabfcee261)

`kubectl config current-context`

![13-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/9aabbf61-05a6-4fb6-8bb4-a08288c422e8)

`cd dhruvcluster`

`helm install dhruvcluster .`

![14-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/380ba6f0-f653-498a-925b-eb398cd70a58)

`kubectl get pods`
![15-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/83c5fd58-efd7-4e2e-8d8f-d71aa35174f2)

`helm upgrade dhruvcluster .`

![17-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/fd9018a1-dd93-4f87-a82a-81811bf393e6)

`kubectl get svc`

![18-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/bd53e57b-ab19-4e45-bf87-b5846f64c860)

![19-](https://github.com/darjidhruv26/Deploy_Helm_Chart_EKS/assets/90086813/e11e1591-2947-4ca3-a4f7-b668267925e8)
