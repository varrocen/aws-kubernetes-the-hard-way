# AWS Kubernetes The Hard Way

## Commands

Create stack (example VPC) :

````
aws cloudformation create-stack \
    --stack-name kubernetes-vpc \
    --template-body file://cloudformation/0-vpc.yaml
````

Update stack :

````
aws cloudformation update-stack \
    --stack-name kubernetes-vpc \
    --template-body file://cloudformation/0-vpc.yaml
````

Delete stack :

````
aws cloudformation delete-stack \
    --stack-name kubernetes-vpc
````