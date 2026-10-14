<div align="center">

# ☁️ AWS VPC CONNECTIVITY LAB

### 🚀 Build. Secure. Deploy. Connect.

**A Hands-On AWS Cloud Infrastructure & Networking Project**

Designing cloud networks, deploying Linux servers, securing access,
and hosting a publicly accessible web server using AWS.

<br>

![AWS](https://img.shields.io/badge/AWS-Cloud%20Infrastructure-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![VPC](https://img.shields.io/badge/Amazon-VPC-8C4FFF?style=for-the-badge&logo=amazonaws&logoColor=white)
![EC2](https://img.shields.io/badge/Amazon-EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-Web%20Server-009639?style=for-the-badge&logo=nginx&logoColor=white)

![CloudFormation](https://img.shields.io/badge/Infrastructure-as%20Code-7B42BC?style=for-the-badge)
![AWS CLI](https://img.shields.io/badge/AWS-CLI-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Administration-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-Version%20Control-F05032?style=for-the-badge&logo=git&logoColor=white)

**👨‍💻 Author: Kiran Babu**

**🌍 AWS Region: Asia Pacific (Mumbai) — `ap-south-1`**

</div>

---

## 📌 Table of Contents

- 🌟 [Project Overview](#-project-overview)
- 🎯 [Project Objectives](#-project-objectives)
- 🏗️ [Architecture](#️-architecture)
- 🧰 [Technology Stack](#-technology-stack)
- 🌐 [Network Design](#-network-design)
- 🔐 [Security Configuration](#-security-configuration)
- ⚙️ [Implementation Workflow](#️-implementation-workflow)
- 🖥️ [EC2 and Nginx Deployment](#️-ec2-and-nginx-deployment)
- 🧪 [Validation Results](#-validation-results)
- 📂 [Repository Structure](#-repository-structure)
- 🛡️ [Security Best Practices](#️-security-best-practices)
- 💰 [Cost Management](#-cost-management)
- 🧹 [Cleanup Guide](#-cleanup-guide)
- 🚀 [Future Enhancements](#-future-enhancements)
- 💡 [Key Learnings](#-key-learnings)
- 👨‍💻 [Author](#-author)

---

## 🌟 Project Overview

**AWS VPC Connectivity Lab** is a practical cloud engineering project
that demonstrates how AWS networking components work together to
host a publicly accessible website.

The infrastructure foundation was provisioned using AWS CloudFormation.
The AWS CLI was used to inspect network resources, configure a custom
Security Group, launch an Ubuntu EC2 instance, and verify connectivity.

An Ubuntu 24.04 LTS server was deployed in the public subnet.
Nginx was installed and enabled as a system service. SSH access,
local HTTP responses, EC2 health checks, and browser access to the
Nginx welcome page were successfully verified.

### ✨ Project Highlights

| Capability | Implementation |
|---|---|
| ☁️ Cloud networking | AWS VPC with public and private subnet design |
| 🏗️ Infrastructure as Code | AWS CloudFormation |
| 🛣️ Routing | Internet Gateway and public route table |
| 🔐 Network security | Custom Security Group |
| 🖥️ Compute | Ubuntu EC2 instance |
| 🔑 Remote administration | SSH key-based authentication |
| 🌐 Web hosting | Nginx HTTP server |
| 🧪 Verification | AWS CLI, system status, SSH, and HTTP tests |
| 📚 Documentation | Architecture and operational workflow |

> **Final outcome:** The EC2 instance was launched successfully,
> SSH access worked, Nginx returned `HTTP 200 OK`, and the Nginx
> welcome page opened in a web browser through the instance's public IP.

---

## 🎯 Project Objectives

- ☁️ Understand AWS Virtual Private Cloud fundamentals.
- 🧱 Design public and private IP address ranges using subnets.
- 🛣️ Configure an Internet Gateway and default route.
- 🔐 Restrict inbound traffic using Security Group rules.
- 🖥️ Deploy and inspect an Ubuntu EC2 instance.
- 🔑 Connect to a Linux server through SSH.
- ⚙️ Install and manage Linux services with `systemctl`.
- 🌍 Deploy Nginx and validate HTTP connectivity.
- 🧪 Verify infrastructure using the AWS CLI.
- 💰 Understand AWS resource lifecycle and cost management.

---

## 🏗️ Architecture

### High-Level Architecture Diagram

```text
                  👨‍💻 ADMINISTRATOR
                    Ubuntu Laptop
                          |
              +-----------+-----------+
              |                       |
          SSH : 22                 HTTP : 80
       Restricted IP              Public access
              |                       |
              +-----------+-----------+
                          |
                          v
                 ☁️ AWS CLOUD
                   ap-south-1
                          |
                          v
                 🌐 INTERNET GATEWAY
                          |
                          v
             ┌───────────────────────────┐
             │       AWS VPC             │
             │      10.0.0.0/16          │
             │                           │
             │  ┌─────────────────────┐  │
             │  │   PUBLIC SUBNET     │  │
             │  │    10.0.1.0/24      │  │
             │  │                     │  │
             │  │  🔐 Security Group  │  │
             │  │         |           │  │
             │  │         v           │  │
             │  │  🖥️ Ubuntu EC2      │  │
             │  │         |           │  │
             │  │         v           │  │
             │  │     🌐 NGINX        │  │
             │  │      TCP : 80       │  │
             │  └─────────────────────┘  │
             │                           │
             │  ┌─────────────────────┐  │
             │  │  PRIVATE SUBNET      │  │
             │  │    10.0.2.0/24       │  │
             │  │                     │  │
             │  │  Future workloads   │  │
             │  └─────────────────────┘  │
             └───────────────────────────┘
```

### 🔄 HTTP Traffic Flow

1. A browser requests the EC2 instance's public IPv4 address.
2. The request reaches AWS through the Internet Gateway.
3. The public route table provides the default IPv4 route.
4. The Security Group evaluates inbound HTTP traffic.
5. Nginx receives the request on TCP port `80`.
6. Nginx returns the welcome page to the browser.

### 🔑 SSH Traffic Flow

1. The administrator initiates an SSH connection.
2. The Security Group permits TCP port `22` from the configured
   administrator public IP address.
3. SSH authenticates the user with the associated private key.
4. The administrator receives a Linux shell on the EC2 instance.

**Scope note:** The private subnet is part of the network design.
Private workload connectivity has not yet been implemented or tested.

---

## 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| ☁️ Amazon VPC | Isolated cloud networking |
| 🏗️ AWS CloudFormation | Infrastructure provisioning |
| 🖥️ Amazon EC2 | Cloud-based Linux server |
| 🌐 Internet Gateway | Internet connectivity for the public subnet |
| 🛣️ Route Tables | Network traffic routing |
| 🔐 Security Groups | Instance-level virtual firewall |
| 🐧 Ubuntu 24.04 LTS | Server operating system |
| 🔑 OpenSSH | Secure remote administration |
| 🌍 Nginx | Web server |
| 🧰 AWS CLI | AWS resource inspection and management |
| 🐚 Bash | Command-line administration |
| 📦 Git | Version control |
| 🐙 GitHub | Source code and documentation |
| 🧪 cfn-lint | CloudFormation template linting |

---

## 🌐 Network Design

### 🧱 VPC Configuration

| Component | Configuration |
|---|---|
| AWS Region | `ap-south-1` |
| VPC CIDR | `10.0.0.0/16` |
| Public Subnet CIDR | `10.0.1.0/24` |
| Private Subnet CIDR | `10.0.2.0/24` |
| Public Subnet AZ | `ap-south-1a` |
| Public IPv4 assignment | Enabled for the public subnet |
| Internet Gateway | Attached to the VPC |

### 🛣️ Public Route Table

| Destination | Target | Status |
|---|---|---|
| `10.0.0.0/16` | `local` | Active |
| `0.0.0.0/0` | Internet Gateway | Active |

The default route sends eligible Internet-bound IPv4 traffic through
the Internet Gateway. Direct Internet connectivity also requires an
appropriate public IPv4 address and suitable security rules.

### 🔎 Route Verification

```bash
aws ec2 describe-route-tables \
  --region ap-south-1 \
  --filters "Name=association.subnet-id,Values=<PUBLIC_SUBNET_ID>" \
  --output json
```

Replace `<PUBLIC_SUBNET_ID>` with the actual public subnet ID.

---

## 🔐 Security Configuration

A dedicated Security Group was created for the web server.

### Inbound Rules

| Protocol | Port | Source | Purpose |
|---|---:|---|---|
| TCP | 22 | Administrator public IP `/32` | SSH administration |
| TCP | 80 | `0.0.0.0/0` | Public HTTP access |

### Outbound Rules

The current Security Group permits outbound IPv4 traffic to
`0.0.0.0/0`.

For production environments, review outbound access and restrict
traffic to the destinations and ports required by the application.

### 🛡️ Security Principles

- 🔑 SSH restricted to a specific administrator IP.
- 🔒 Private SSH key permissions set to `400`.
- 🚫 Private keys and AWS credentials excluded from GitHub.
- 🧱 Dedicated Security Group for the application server.
- 🔍 Configuration verified using AWS CLI commands.
- 💰 Cost and resource cleanup considered during operations.

> **Production recommendation:** Add HTTPS with a valid TLS certificate,
> use least-privilege IAM policies, review outbound traffic, and
> evaluate AWS Systems Manager Session Manager for administration.

---

## ⚙️ Implementation Workflow

### Phase 1 — 🏗️ Infrastructure Provisioning

- Created VPC infrastructure using AWS CloudFormation.
- Verified the CloudFormation stack status.
- Inspected public and private subnet configuration.
- Verified the public route table and Internet Gateway route.

```bash
aws cloudformation describe-stacks \
  --stack-name aws-vpc-connectivity-lab \
  --region ap-south-1 \
  --query 'Stacks[0].StackStatus' \
  --output text
```

Verified stack status: `CREATE_COMPLETE`.

### Phase 2 — 🔐 Security Group Configuration

- Created a custom Security Group.
- Added SSH access for the administrator public IP.
- Verified the SSH inbound rule.
- Inspected the outbound traffic policy.

### Phase 3 — 🖥️ EC2 Deployment

- Selected the Ubuntu 24.04 LTS AMI.
- Selected the `t3.micro` instance type.
- Launched EC2 in the public subnet.
- Configured an 8 GiB gp3 root volume.
- Associated the EC2 SSH key pair.
- Enabled public IPv4 assignment.
- Added project identification tags.

### Phase 4 — 🩺 Instance Health Verification

```bash
aws ec2 describe-instance-status \
  --instance-ids <INSTANCE_ID> \
  --include-all-instances \
  --region ap-south-1 \
  --output table
```

The instance reached `running`, and both system and instance
status checks returned `ok`.

### Phase 5 — 🔑 SSH Connection

```bash
ssh -i ~/vpc-connectivity-lab-key.pem \
  ubuntu@<CURRENT_EC2_PUBLIC_IP>
```

SSH authentication succeeded.

**Note:** Replace the placeholders with the actual current values.
Never upload the `.pem` private key to GitHub.

### Phase 6 — 🌍 Nginx Deployment

Update package information:

```bash
sudo apt update
```

Install Nginx:

```bash
sudo apt install nginx -y
```

Enable and start the service:

```bash
sudo systemctl enable --now nginx
```

Verify service status:

```bash
sudo systemctl status nginx --no-pager
```

### Phase 7 — 🧪 HTTP Verification

Run on the EC2 instance:

```bash
curl -I http://localhost
```

Verified response:

```text
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
```

After adding the HTTP Security Group rule, the Nginx welcome
page opened successfully in the browser.

---

## 🖥️ EC2 and Nginx Deployment

| Setting | Value |
|---|---|
| Operating System | Ubuntu 24.04 LTS |
| Instance Type | `t3.micro` |
| Root Volume | 8 GiB gp3 |
| SSH User | `ubuntu` |
| Web Server | Nginx |
| SSH Port | TCP `22` |
| HTTP Port | TCP `80` |
| Deployment Location | Public subnet |

Live resource identifiers and public IP addresses are not hardcoded
as permanent values in this public documentation.

Public IPv4 addresses may change after an instance is stopped and
started. Retrieve the current address before connecting.

---

## 🧪 Validation Results

| Test ID | Validation | Result |
|---|---|---|
| NET-01 | CloudFormation stack | ✅ PASS |
| NET-02 | Public subnet configuration | ✅ PASS |
| NET-03 | Internet Gateway route | ✅ PASS |
| SEC-01 | Custom Security Group | ✅ PASS |
| SEC-02 | Restricted SSH rule | ✅ PASS |
| EC2-01 | EC2 instance launch | ✅ PASS |
| EC2-02 | EC2 health checks | ✅ PASS |
| SSH-01 | SSH authentication | ✅ PASS |
| WEB-01 | Nginx installation | ✅ PASS |
| WEB-02 | Nginx service running | ✅ PASS |
| WEB-03 | Local HTTP response | ✅ PASS |
| WEB-04 | Browser access to Nginx | ✅ PASS |
| PRIV-01 | Private subnet workload test | ⏳ NOT TESTED |
| TLS-01 | HTTPS configuration | ⏳ FUTURE WORK |

The results above reflect the commands and browser checks completed
during this lab. Private subnet workload connectivity and HTTPS
have not yet been implemented or verified.

---

## 📂 Repository Structure

```text
aws-vpc-connectivity-lab/
├── templates/
│   └── vpc-setup.yaml
├── docs/
│   ├── traffic-flow.md
│   ├── security-design.md
│   ├── verification-report.md
│   └── cleanup.md
├── diagrams/
├── screenshots/
├── tests/
├── .gitignore
└── README.md
```

This is the intended project layout. Verify that each listed file
exists before treating every item as complete.

### 📸 Recommended Evidence

Capture genuine screenshots and save them in `screenshots/`:

- `01-vpc-overview.png` — VPC configuration.
- `02-subnets.png` — Public and private subnet details.
- `03-route-table.png` — Internet Gateway route.
- `04-security-group.png` — SSH and HTTP rules.
- `05-ec2-instance.png` — EC2 running state and health checks.
- `06-ssh-login.png` — Successful SSH login.
- `07-nginx-status.png` — Nginx service status.
- `08-nginx-browser.png` — Nginx welcome page.

Do not include credentials, private keys, access tokens, or other
sensitive information in screenshots.

---

## 🛠️ Troubleshooting

### ❌ SSH Connection Timeout

Check:

1. EC2 state and health checks.
2. Current EC2 public IPv4 address.
3. Security Group TCP port `22` source CIDR.
4. Public route table and Internet Gateway.
5. Whether the administrator public IP has changed.

### ❌ SSH Permission Denied

```bash
chmod 400 ~/vpc-connectivity-lab-key.pem
```

Confirm that the correct key pair and SSH username are being used.

### ❌ Website Not Reachable

Check Nginx:

```bash
sudo systemctl status nginx --no-pager
```

Test locally:

```bash
curl -I http://localhost
```

Verify the HTTP Security Group rule, public IPv4 address,
and route table configuration.

### ❌ AWS CLI Access Problems

```bash
aws sts get-caller-identity
aws configure get region
```

Never share AWS credentials or private SSH keys while troubleshooting.

---

## 💰 Cost Management

AWS charges depend on account eligibility, region, resource type,
usage, and applicable credits.

Potential cost sources include:

- 🖥️ EC2 instance runtime.
- 💾 EBS storage.
- 🌐 Public IPv4 addresses.
- 🏗️ Additional networking resources.
- 📊 Optional monitoring services.

### 💡 Cost-Saving Practices

- Choose instance sizes appropriate for the workload.
- Monitor AWS Billing and Cost Management.
- Stop instances when compute is not required.
- Remember that EBS storage charges may continue while stopped.
- Terminate resources when the lab is permanently finished.
- Review resource dependencies before deleting CloudFormation stacks.

Do not assume an instance is free merely because it is small.

---

## 🧹 Cleanup Guide

Before cleanup, verify resource IDs and dependencies.

### Step 1 — Inspect the Lab Instance

```bash
aws ec2 describe-instances \
  --region ap-south-1 \
  --filters "Name=tag:Project,Values=aws-vpc-connectivity-lab" \
  --query 'Reservations[].Instances[].{ID:InstanceId,State:State.Name,Name:Tags[?Key==`Name`]|[0].Value}' \
  --output table
```

### Step 2 — Terminate Only the Verified Lab Instance

When the lab is permanently finished:

```bash
aws ec2 terminate-instances \
  --instance-ids <INSTANCE_ID> \
  --region ap-south-1
```

Replace `<INSTANCE_ID>` with the verified lab instance ID.

### Step 3 — Review Remaining Resources

The EC2 instance and custom Security Group were created using
separate AWS CLI commands. Do not assume that CloudFormation manages
those resources.

Review the CloudFormation stack resources and dependencies before
deleting the stack. Remove separately created resources only after
confirming that they are no longer needed.

**Never run destructive cleanup commands against unverified resources.**

---

## 🚀 Future Enhancements

### 🔐 Security
- [ ] Configure HTTPS with a valid TLS certificate.
- [ ] Review and restrict outbound traffic.
- [ ] Explore Systems Manager Session Manager.
- [ ] Apply least-privilege IAM policies.

### 🌐 Networking
- [ ] Deploy a workload in the private subnet.
- [ ] Test public-to-private network communication.
- [ ] Evaluate NAT Gateway requirements and costs.
- [ ] Enable VPC Flow Logs.

### ⚙️ Automation
- [ ] Add automated infrastructure verification scripts.
- [ ] Expand regression and connectivity tests.
- [ ] Improve deployment reproducibility.
- [ ] Add infrastructure validation to GitHub Actions.

### 📊 Operations
- [ ] Add CloudWatch monitoring and alarms.
- [ ] Document incident troubleshooting.
- [ ] Add repeatable cleanup checks.
- [ ] Capture architecture and deployment evidence.

---

## 💡 Key Learnings

Through this practical implementation, the project demonstrates:

- 🧠 AWS VPC and subnet fundamentals.
- 🌐 Internet Gateway and route table behavior.
- 🔐 Security Group ingress and egress configuration.
- 🖥️ EC2 provisioning and health verification.
- 🔑 Linux SSH authentication.
- 🐧 Ubuntu package and service administration.
- 🌍 Nginx installation and HTTP validation.
- 🧪 AWS CLI-based troubleshooting.
- 💰 Cloud resource lifecycle and cost awareness.
- 📚 Technical documentation for a cloud portfolio.

These are foundational skills for AWS Cloud Engineering
and infrastructure operations.

---

## 👨‍💻 Author

<div align="center">

### Kiran Babu

**Aspiring AWS Cloud Engineer**

☁️ AWS | 🐧 Linux | 🌐 Networking | 🖥️ EC2 | 🔐 Cloud Security

Building practical cloud infrastructure projects and documenting
real-world deployment and troubleshooting workflows.

<br>

### ⭐ Thanks for Visiting This Project!

**Learn by Building. Validate by Testing. Improve Through Practice.**

☁️ AWS Cloud Engineering — Hands-On Learning Portfolio 🚀

</div>
