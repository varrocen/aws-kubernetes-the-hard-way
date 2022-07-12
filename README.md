# AWS Kubernetes The Hard Way

## Commands

Create VPC :

````
aws cloudformation create-stack \
    --stack-name kubernetes-vpc \
    --template-body file://cloudformation/vpc.yaml
````

Update VPC :

````
aws cloudformation update-stack \
    --stack-name kubernetes-vpc \
    --template-body file://cloudformation/vpc.yaml
````