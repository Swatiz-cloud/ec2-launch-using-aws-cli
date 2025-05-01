# EC2-Launch-using-aws-cli

## 🧾 What is EC2?

**Amazon EC2 (Elastic Compute Cloud)** is a service that allows you to run virtual servers (called instances) on the AWS cloud. You can choose an OS, instance type (CPU/memory), storage, security settings, and more.



## 🖥️  Using AWS CLI

The AWS CLI lets you control AWS services from the command line.


### Step 1: Configure CLI (once per system)

```bash
aws configure
```

Enter:

- AWS Access Key
- AWS Secret Key
- Region (e.g., `us-east-1`)
- Output format (e.g., `json`)



### Step 2: Run `aws ec2 run-instances` command

```bash
aws ec2 run-instances \
  --image-id ami-0c02fb55956c7d316 \
  --instance-type t2.micro \
  --key-name my-key-pair \
  --security-groups my-security-group \
  --region us-east-1 \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=MyEC2Instance}]'
```


**Explanation of parameters**:

- `--image-id`: AMI ID for Amazon Linux (or your desired OS)
- `--instance-type`: Type like `t2.micro` (Free Tier)
- `--key-name`: Existing EC2 key pair to SSH into instance
- `--security-groups`: Pre-existing security group name
- `--tag-specifications`: Add a "Name" tag for easy identification




### Step 3: Get the public IP

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,PublicIpAddress]' --output table
```




### Step 4: Terminate Instance

```bash
aws ec2 terminate-instances --instance-ids i-xxxxxxxxxxxxxxxxx
```



## 🛡️ Important Notes

- Make sure you have an existing **key pair** in your AWS account.
- Use security groups that allow **port 22 (SSH)** from your IP or 0.0.0.0/0 (not recommended for production).
- Always destroy unused resources to avoid charges.


Would you like a ZIP file with all Terraform files ready to use?
