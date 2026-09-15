# AWS CLI – EC2 Management Practice

This repository contains hands-on **AWS CLI commands for managing Amazon EC2 instances**, including AMI discovery, key pairs, instance creation, monitoring, stopping, termination, multi-region operations, and EC2 tagging.

## 📌 Prerequisites

Before running the commands, make sure you have:

* AWS CLI installed
* AWS account
* IAM credentials configured
* An EC2 key pair
* PowerShell on Windows
* Appropriate IAM permissions for EC2

Check AWS CLI installation:

```powershell
aws --version
```

---

# 1. Check AWS Credentials

Verify the AWS identity currently being used by AWS CLI:

```powershell
aws sts get-caller-identity
```

Example:

```text
Account: 123456789012
Arn: arn:aws:iam::123456789012:user/example
```

---

# 2. Check AWS Region

Check the currently configured default region:

```powershell
aws configure get region
```

Set Mumbai region:

```powershell
aws configure set region ap-south-1
```

Verify:

```powershell
aws configure get region
```

---

# 3. Find Ubuntu AMI

## Using Canonical Ubuntu Owner ID

The official Canonical Ubuntu AMI owner ID is:

```text
099720109477
```

Find the latest Ubuntu 24.04 AMI:

```powershell
aws ec2 describe-images `
    --owners 099720109477 `
    --filters "Name=name,Values=ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*" `
              "Name=state,Values=available" `
    --query "Images | sort_by(@,&CreationDate)[-1].[ImageId,Name,CreationDate]" `
    --output table
```

Get only the AMI ID:

```powershell
aws ec2 describe-images `
    --owners 099720109477 `
    --filters "Name=name,Values=ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*" `
              "Name=state,Values=available" `
    --query "Images | sort_by(@,&CreationDate)[-1].ImageId" `
    --output text
```

> **Note:** AMI IDs are region-specific. An AMI ID from `ap-south-1` should not automatically be used in another region.

Example AMI ID used during practice:

```text
ami-0c0fd09cfe77b59dc
```

---

# 4. Verify EC2 Key Pair

Check whether the key pair exists:

```powershell
aws ec2 describe-key-pairs `
    --region ap-south-1 `
    --key-names mum-srisolutions-kp
```

List all key pairs:

```powershell
aws ec2 describe-key-pairs `
    --region ap-south-1 `
    --query "KeyPairs[].{Name:KeyName,ID:KeyPairId,Type:KeyType,Fingerprint:KeyFingerprint}" `
    --output table
```

> EC2 key pairs are **region-specific**.

---

# 5. Create an EC2 Instance

Create a `t3.micro` Ubuntu instance:

```powershell
aws ec2 run-instances `
    --image-id ami-0c0fd09cfe77b59dc `
    --instance-type t3.micro `
    --key-name mum-srisolutions-kp `
    --count 1
```

> Replace the AMI ID with a valid Ubuntu AMI for your target region.

---

# 6. Find the Newly Created Instance

Check pending and running instances:

```powershell
aws ec2 describe-instances `
    --filters "Name=instance-state-name,Values=pending,running" `
    --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,IP:PublicIpAddress}" `
    --output table
```

---

# 7. Connect to Ubuntu EC2

Use the private key:

```powershell
ssh -i "C:\Users\SESHU_VANI\Downloads\mum-srisolutions-kp.pem" ubuntu@PUBLIC_IP
```

Example:

```powershell
ssh -i "C:\Users\SESHU_VANI\Downloads\mum-srisolutions-kp.pem" ubuntu@13.201.20.148
```

---

# 8. List Running EC2 Instances

```powershell
aws ec2 describe-instances `
    --filters "Name=instance-state-name,Values=running"
```

Display in table format:

```powershell
aws ec2 describe-instances `
    --filters "Name=instance-state-name,Values=running" `
    --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,PublicIP:PublicIpAddress,PrivateIP:PrivateIpAddress}" `
    --output table
```

---

# 9. List All EC2 Instances

```powershell
aws ec2 describe-instances `
    --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,PublicIP:PublicIpAddress}" `
    --output table
```

---

# 10. Stop an EC2 Instance

```powershell
aws ec2 stop-instances `
    --region ap-south-1 `
    --instance-ids i-011c8f17bdb950492
```

Verify the instance state:

```powershell
aws ec2 describe-instances `
    --region ap-south-1 `
    --instance-ids i-011c8f17bdb950492 `
    --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name}" `
    --output table
```

---

# 11. Terminate an EC2 Instance

> ⚠️ **Warning:** Termination is destructive. A terminated EC2 instance cannot normally be recovered.

```powershell
aws ec2 terminate-instances `
    --region ap-south-1 `
    --instance-ids i-011c8f17bdb950492
```

---

# 12. List Running Instances with Name

Display the EC2 Name tag:

```powershell
aws ec2 describe-instances `
    --region ap-south-1 `
    --filters "Name=instance-state-name,Values=running" `
    --query "Reservations[].Instances[].{ID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,Type:InstanceType,IP:PublicIpAddress}" `
    --output table
```

---

# 13. Terminate All Running Instances

## PowerShell

First get all running instance IDs:

```powershell
$ids = aws ec2 describe-instances `
    --region ap-south-1 `
    --filters "Name=instance-state-name,Values=running" `
    --query "Reservations[].Instances[].InstanceId" `
    --output text
```

Convert the IDs into an array:

```powershell
$ids = $ids -split '\s+' | Where-Object { $_ }
```

Review the IDs:

```powershell
$ids
```

Then terminate:

```powershell
foreach ($id in $ids) {
    aws ec2 terminate-instances --region ap-south-1 --instance-ids $id
}
```

> ⚠️ Always review `$ids` before executing the termination command.

---

# 14. Work With Multiple AWS Regions

Define the regions:

```powershell
$regions = @("ap-south-1", "us-east-1")
```

List EC2 instances from both regions:

```powershell
foreach ($region in $regions) {
    Write-Host "`n========== $region ==========" -ForegroundColor Green

    aws ec2 describe-instances `
        --region $region `
        --query "Reservations[].Instances[].{Region:'$region',ID:InstanceId,State:State.Name,Type:InstanceType,PublicIP:PublicIpAddress,PrivateIP:PrivateIpAddress}" `
        --output table
}
```

---

# 15. List Stopped Instances From Multiple Regions

```powershell
$regions = @("ap-south-1", "us-east-1")

foreach ($region in $regions) {
    Write-Host "`n========== $region ==========" -ForegroundColor Green

    aws ec2 describe-instances `
        --region $region `
        --filters "Name=instance-state-name,Values=stopped" `
        --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,PublicIP:PublicIpAddress}" `
        --output table
}
```

---

# 16. List Key Pairs From Multiple Regions

```powershell
$regions = @("ap-south-1", "us-east-1")

foreach ($region in $regions) {
    Write-Host "`n========== $region ==========" -ForegroundColor Green

    aws ec2 describe-key-pairs `
        --region $region `
        --query "KeyPairs[].{Name:KeyName,ID:KeyPairId,Type:KeyType,Fingerprint:KeyFingerprint}" `
        --output table
}
```

---

# 17. Show EC2 Instance + Region + Key Pair

```powershell
$regions = @("ap-south-1", "us-east-1")

foreach ($region in $regions) {
    aws ec2 describe-instances `
        --region $region `
        --query "Reservations[].Instances[].{Region:'$region',InstanceID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,State:State.Name,Type:InstanceType,KeyPair:KeyName,PublicIP:PublicIpAddress}" `
        --output table
}
```

This provides:

```text
Region
Instance ID
Instance Name
State
Instance Type
Key Pair
Public IP
```

---

# 18. List Instances in a Specific Region

```powershell
aws ec2 describe-instances `
    --region ap-south-1 `
    --query "Reservations[].Instances[].{ID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,State:State.Name}" `
    --output table
```

---

# 19. Change EC2 Instance Name

The EC2 instance name is stored as the `Name` tag.

Example:

```powershell
aws ec2 create-tags `
    --region ap-south-1 `
    --resources i-0d82d99c532db4b18 `
    --tags "Key=Name,Value=Jenkins-Server"
```

For names containing spaces, use quotes:

```powershell
aws ec2 create-tags `
    --region ap-south-1 `
    --resources i-0d82d99c532db4b18 `
    --tags "Key=Name,Value=shell scripting"
```

Verify:

```powershell
aws ec2 describe-instances `
    --region ap-south-1 `
    --instance-ids i-0d82d99c532db4b18 `
    --query "Reservations[].Instances[].{ID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,State:State.Name}" `
    --output table
```

---

# 20. Get All AWS Regions

If the AWS CLI does not have a default region configured, specify a region for the `describe-regions` request:

```powershell
$regions = aws ec2 describe-regions `
    --region ap-south-1 `
    --all-regions `
    --query "Regions[].RegionName" `
    --output json | ConvertFrom-Json
```

Check the number of regions:

```powershell
$regions.Count
```

Display them:

```powershell
$regions
```

---

# 21. Reset the AWS CLI Default Region

To check the configured region:

```powershell
aws configure get region
```

To change it:

```powershell
aws configure set region ap-south-1
```

If you want no default region, edit the AWS config:

```powershell
notepad "$HOME\.aws\config"
```

The configuration can contain:

```ini
[default]
```

without:

```ini
region = ap-south-1
```

Then verify:

```powershell
aws configure get region
```

> When no default region is configured, commands such as `describe-instances` require an explicit `--region`.

---

# 22. Useful AWS CLI Output Options

### Table

```powershell
--output table
```

### JSON

```powershell
--output json
```

### Text

```powershell
--output text
```

### Query specific information

```powershell
--query "Reservations[].Instances[].InstanceId"
```

---

# 23. Important AWS CLI Concepts

## Region

AWS resources such as EC2 instances and key pairs are generally associated with a specific AWS region.

Examples:

```text
ap-south-1
us-east-1
```

## AMI

An AMI is the image used to launch an EC2 instance.

Example:

```text
ami-0c0fd09cfe77b59dc
```

## Instance ID

Every EC2 instance has a unique ID:

```text
i-0d82d99c532db4b18
```

## Key Pair

A key pair is used for SSH authentication when launching an EC2 instance.

Example:

```text
mum-srisolutions-kp
```

The `.pem` file is the private key stored on your computer:

```text
C:\Users\SESHU_VANI\Downloads\mum-srisolutions-kp.pem
```

## Name Tag

The EC2 console's instance name is normally the `Name` tag:

```text
Key = Name
Value = Jenkins-Server
```

---

# ⚠️ Safety Notes

Be careful with destructive commands.

### Stop

```powershell
aws ec2 stop-instances --instance-ids INSTANCE_ID
```

The instance can normally be started again.

### Terminate

```powershell
aws ec2 terminate-instances --instance-ids INSTANCE_ID
```

Termination is destructive.

Before terminating multiple instances:

```powershell
aws ec2 describe-instances `
    --filters "Name=instance-state-name,Values=running" `
    --query "Reservations[].Instances[].{ID:InstanceId,Name:Tags[?Key=='Name']|[0].Value,Type:InstanceType,IP:PublicIpAddress}" `
    --output table
```

Always verify the instance IDs and AWS region before running termination commands.

---

# 🧰 Technologies Used

* AWS CLI
* Amazon EC2
* Ubuntu
* AWS IAM
* PowerShell
* SSH
* AWS AMI
* EC2 Key Pairs
* AWS Regions
* AWS Tags

---

# 🎯 Learning Objectives

Through this practice, you will learn how to:

* Configure AWS CLI
* Verify AWS credentials
* Work with AWS regions
* Find Ubuntu AMIs
* Create EC2 instances
* Connect to Ubuntu EC2 using SSH
* List EC2 instances
* Filter EC2 instances by state
* Stop EC2 instances
* Terminate EC2 instances
* Manage EC2 key pairs
* Manage EC2 Name tags
* Work with multiple AWS regions
* Use AWS CLI queries
* Format AWS CLI output
* Automate AWS CLI operations using PowerShell

---

# 📚 Useful Commands Cheat Sheet

| Task                   | Command                                                                          |
| ---------------------- | -------------------------------------------------------------------------------- |
| Check identity         | `aws sts get-caller-identity`                                                    |
| Check region           | `aws configure get region`                                                       |
| Set region             | `aws configure set region ap-south-1`                                            |
| List instances         | `aws ec2 describe-instances`                                                     |
| List running instances | `aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"` |
| Stop instance          | `aws ec2 stop-instances --instance-ids ID`                                       |
| Start instance         | `aws ec2 start-instances --instance-ids ID`                                      |
| Reboot instance        | `aws ec2 reboot-instances --instance-ids ID`                                     |
| Terminate instance     | `aws ec2 terminate-instances --instance-ids ID`                                  |
| List key pairs         | `aws ec2 describe-key-pairs`                                                     |
| Create EC2             | `aws ec2 run-instances`                                                          |
| Add/change Name tag    | `aws ec2 create-tags`                                                            |
| List regions           | `aws ec2 describe-regions`                                                       |

---

## 👨‍💻 Author

**Seshukumar Katamneni**

AWS CLI / DevOps Hands-on Practice
