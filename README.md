# AWS AMIs with packer 

This document will describe the process to create an AWS CentOS AMI using the Packer tool

## Requirements

1. AWS Account
2. AWS Role with the minimal set of permissions to use Packer ([Packer minimal permissions](https://www.packer.io/docs/builders/amazon.html#iam-task-or-instance-role))
    - Copy this JSON file and create a new AWS Role
  ```json
  {
  "Version": "2012-10-17",
  "Statement": [{
      "Effect": "Allow",
      "Action" : [
        "ec2:AttachVolume",
        "ec2:AuthorizeSecurityGroupIngress",
        "ec2:CopyImage",
        "ec2:CreateImage",
        "ec2:CreateKeypair",
        "ec2:CreateSecurityGroup",
        "ec2:CreateSnapshot",
        "ec2:CreateTags",
        "ec2:CreateVolume",
        "ec2:DeleteKeyPair",
        "ec2:DeleteSecurityGroup",
        "ec2:DeleteSnapshot",
        "ec2:DeleteVolume",
        "ec2:DeregisterImage",
        "ec2:DescribeImageAttribute",
        "ec2:DescribeImages",
        "ec2:DescribeInstances",
        "ec2:DescribeInstanceStatus",
        "ec2:DescribeRegions",
        "ec2:DescribeSecurityGroups",
        "ec2:DescribeSnapshots",
        "ec2:DescribeSubnets",
        "ec2:DescribeTags",
        "ec2:DescribeVolumes",
        "ec2:DetachVolume",
        "ec2:GetPasswordData",
        "ec2:ModifyImageAttribute",
        "ec2:ModifyInstanceAttribute",
        "ec2:ModifySnapshotAttribute",
        "ec2:RegisterImage",
        "ec2:RunInstances",
        "ec2:StopInstances",
        "ec2:TerminateInstances",
        "ec2:RequestSpotInstances",
        "ec2:CancelSpotInstanceRequests",
        "ec2:DescribeSpotInstanceRequests",
        "ec2:DescribeSpotPriceHistory"
      ],
      "Resource" : "*"
  }]
}
```
3. AWS User with programmatic access. Assign the AWS Role created above
4. AWS Subnet with the **auto-assign public IPv4 address** setting enabled
5. Packer binary
    - [Download Packer Binary](https://www.packer.io/downloads.html)
6. AWS Packer and Nginx Ansible Github repositories
  - AWS Packer
``` bash
git clone https://github.com/EduardoVega/aws-packer.git
```
  - Nginx Ansible
```bash
git clone https://github.com/EduardoVega/nginx-ansible.git
```

## Execution
1. Export Variables
```bash
export AMI_NAME=''
export SUBNET_ID=''
export ACCESS_KEY=''
export SECRET_KEY=''
```
2. Validate Packer JSON file
```bash
# Navigate to the aws-packer github repo
cd aws-packer

# Validate packer json file
packer validate centos-7-nginx-ami.json

```
3. Run Packer JSON file
```bash
# Navigate to the aws-packer github repo
cd aws-packer

# Run packer json file
packer build centos-7-nginx-ami.json

```


