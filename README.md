# OS Images with Packer 

This repository contains a Packer template to create an Image of CentOS 7 Images and Nginx

## Supported Providers

- Amazon Web Services
- Google Cloud Platform

## Prerequisites

### General

1. Packer binary
    - [Download Packer Binary](https://www.packer.io/downloads.html)
2. centos 7 nginx packer and nginx ansible Github repositories
``` bash
git clone https://github.com/EduardoVega/centos-7-nginx-packer.git

git clone https://github.com/EduardoVega/nginx-ansible.git
```

### Amazon Web Services

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


### Google Cloud Platform

1. GCP Account
2. Follow the steps to create a service account with the required permissions to run packer (https://www.packer.io/docs/builders/googlecompute.html#running-without-a-compute-engine-service-account)

## Execution
1. Set and export Environment Variables
    - Amazon Web Services
      ```bash
      bash aws-env-vars.sh
      ```
    - Google Cloud Platform
      ```bash
      bash gcp-env-vars.sh
      ```
2. Run and Validate Packer JSON file

    Packer supports parallel builds, so you can create the images for AWS and GCP at the same time; or you can specify the specific builder you want to run

    - Validate
    ```bash
    # Navigate to the github repo
    cd centos-7-nginx-packer

    # Validate packer json file (all providers)
    packer validate centos-7-nginx.json

    # Validate packer json file (AWS only)
    packer validate -only='aws' centos-7-nginx.json

    # Validate packer json file (GCP only)
    packer validate -only='gcp' centos-7-nginx.json

    ```
    - Build
    ```bash
    # Navigate to the github repo
    cd centos-7-nginx-packer

    # build packer json file (all providers)
    packer build centos-7-nginx.json

    # build packer json file (AWS only)
    packer build -only='aws' centos-7-nginx.json

    # build packer json file (GCP only)
    packer build -only='gcp' centos-7-nginx.json

    ```


