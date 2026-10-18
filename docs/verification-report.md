# AWS VPC Connectivity Verification Report

## 1. Project Information

- Project: AWS VPC Connectivity Lab
- AWS Region: ap-south-1
- CloudFormation Stack: aws-vpc-connectivity-lab
- CloudFormation Stack Status: CREATE_COMPLETE
- VPC ID: vpc-0caa65075d440bd58
- VPC CIDR: 10.0.0.0/16

## 2. Subnet Configuration

| Property | Public Subnet | Private Subnet |
|---|---|---|
| Subnet ID | subnet-00beaa61e9f1ada32 | subnet-0f6aea71cf8a9b070 |
| CIDR | 10.0.1.0/24 | 10.0.2.0/24 |
| Auto-assign public IPv4 | Enabled | Disabled |
| Dedicated route table | Verified | Verified |

## 3. Network Resources

| Resource | Observed Configuration | Result |
|---|---|---|
| VPC | 10.0.0.0/16 | PASS |
| Internet Gateway | Attached to VPC | PASS |
| Public route table | 0.0.0.0/0 -> Internet Gateway | PASS |
| Public subnet route | 10.0.0.0/16 -> local | PASS |
| Private route table | 10.0.0.0/16 -> local only | PASS |
| Private default internet route | Absent | PASS |
| Public subnet route-table association | Explicit association | PASS |
| Private subnet route-table association | Explicit association | PASS |

## 4. EC2 Instance Verification

- Instance ID: i-0af75ebe2dd97021c
- Operating System: Ubuntu 24.04 LTS
- Instance Type: t3.micro
- Private IPv4: 10.0.1.48
- Public IPv4 at time of testing: 13.235.128.151
- Security Group: sg-0b106e335649a2278
- Observed instance state: running

## 5. Connectivity Test Results

| Test | Method | Result |
|---|---|---|
| EC2 instance state | AWS CLI describe-instances | PASS |
| SSH access to public EC2 | SSH using project key pair | PASS |
| Nginx service | systemctl is-active nginx | PASS |
| Local Nginx HTTP response | curl -I http://localhost on EC2 | PASS - HTTP 200 OK |
| Public HTTP response | curl -I http://13.235.128.151 from the Ubuntu host | PASS - HTTP 200 OK |
| Custom webpage served by Nginx | HTTP response content inspection | PASS |
| Public-to-private application connectivity | Not tested | NOT TESTED |
| Private instance direct internet access | No private test instance created | NOT TESTED |
| Public EC2 outbound internet access | Not independently tested | NOT TESTED |

## 6. Security Group Verification

Inbound rules observed:

- TCP 22 (SSH): restricted to 106.192.13.71/32 at the time of inspection.
- TCP 80 (HTTP): allowed from 0.0.0.0/0 for public website access.

Outbound rule observed:

- All IPv4 traffic allowed to 0.0.0.0/0.

The administrator public IP may change. Review the SSH source CIDR before future access.

## 7. Test Evidence

The following evidence was observed during the lab:

- AWS CLI output confirmed the VPC, subnet, route-table and EC2 configurations.
- SSH login to the public EC2 instance succeeded.
- Nginx reported an active service state.
- Local HTTP testing returned HTTP 200 OK.
- HTTP testing from the Ubuntu host to the EC2 public IP returned HTTP 200 OK.
- The custom AWS VPC Connectivity Lab HTML page was served successfully.

AWS Console screenshots should be added to the repository separately.

## 8. Limitations

- A workload has not been launched in the private subnet.
- Public-to-private workload connectivity has not been tested.
- Private subnet internet isolation has been assessed from route configuration, not an end-to-end private instance test.
- HTTPS was configured using a self-signed certificate.
- Nginx configuration validation succeeded.
- TCP port 443 was verified as listening.
- Public HTTPS connectivity returned HTTP 200 OK using `curl -k`.
- Certificate trust validation was not performed.
- NAT Gateway has not been configured.

## 9. Conclusion

The VPC foundation and route-table configuration were verified using AWS CLI.
The public EC2 instance was reached successfully through SSH and HTTP.
Nginx served the custom project webpage and returned HTTP 200 OK.

Private subnet workload connectivity remains untested. The report distinguishes
verified configuration from tests that have not yet been performed.
