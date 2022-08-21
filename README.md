# AWS Kubernetes The Hard Way

[![cfn_nag](https://github.com/varrocen/aws-kubernetes-the-hard-way/actions/workflows/cfn-nag.yaml/badge.svg?branch=main)](https://github.com/varrocen/aws-kubernetes-the-hard-way/actions/workflows/cfn-nag.yaml)

## Commands

### VPC stack

Create VPC stack :

````
aws cloudformation create-stack \
    --stack-name kubernetes-vpc \
    --template-body file://cloudformation/0-vpc.yaml
````

Update VPC stack :

````
aws cloudformation update-stack \
    --stack-name kubernetes-vpc \
    --template-body file://cloudformation/0-vpc.yaml
````

Delete VPC stack :

````
aws cloudformation delete-stack \
    --stack-name kubernetes-vpc
````

### EC2 stack

Create EC2 stack :

````
export SUBNET_IDS=$(aws ec2 describe-subnets --filters "Name=default-for-az,Values=false" --query "Subnets[*]" | jq -r '. | sort_by(.AvailabilityZone) | map(.SubnetId) | join(",")')
aws cloudformation create-stack \
    --stack-name kubernetes-ec2 \
    --template-body file://cloudformation/1-ec2.yaml \
    --parameters ParameterKey=SubnetIds,ParameterValue=\"$SUBNET_IDS\" \
    --capabilities CAPABILITY_IAM
````

Update EC2 stack :

````
aws cloudformation update-stack \
    --stack-name kubernetes-ec2 \
    --template-body file://cloudformation/1-ec2.yaml \
    --parameters ParameterKey=SubnetIds,ParameterValue=\"$SUBNET_IDS\" \
    --capabilities CAPABILITY_IAM
````

Delete EC2 stack :

````
aws cloudformation delete-stack \
    --stack-name kubernetes-ec2
````