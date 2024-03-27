## Instructions

#### Clusture setup
1. Install Terraform
2. Install Azure Cli
3. Login to Azure cloud
```
az login
```
4. Clone the repo using below command:
```
git clone git@github.com:nitishkaushik007786/mediawiki-with-aks.git
```
5. Go into `terraform` directory by `cd terraform`
6. Run below commands to set up the AKS clustur
```
terraform init
terraform plan
terraform apply
```
#### Application Deployment
1. Install `kubectl` to access the clustur
2. To provide referece to the clustur, run below command
```
az aks get-credentials --resource-group aks_terraform_rg --name terraform-aks --overwrite-existing
```
3. Create the namespace
```
kubectl create ns mediwiki
```
4. Install helm locally
5. Go to directory `mediawiki` using `cd mediawiki`
6. Deploy the application using Helm with below command:
```
helm install mediawiki ./
```

_Note: When deploying a revision of application use below command:_
```
helm upgrade --install mediawiki ./
```

#### Accessing the Application
1. Get the External IP of the application with below command:
```
kubectl get svc -n mediawiki
```
2. The application is accessible on `http://{external-ip}`

#### Auto Scaling
We can use HPA (Horizontal Pod AutoScaler) and/or Node auto scaling to scale the application.

_Note:Currently There is no HPA setup for scaling of pods/application but it can be accommodated based upon cpu util./load  and autoscaling can also be enabled on top of AKS to bring up a new node based upon metrics._

