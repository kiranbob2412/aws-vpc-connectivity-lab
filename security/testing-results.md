# Security and Connectivity Testing Results

## AWS Environment
- Region: ap-south-1
- VPC ID: vpc-0caa65075d440bd58
- Public Subnet: subnet-00beaa61e9f1ada32
- Private Subnet: subnet-0f6aea71cf8a9b070
- Custom Public NACL: acl-037d90c25614b3e78
- Security Group: sg-0b106e335649a2278

## EC2 Instance
- Instance ID: i-0af75ebe2dd97021c
- Private IP: 10.0.1.48
- Public IP observed during testing: 13.207.198.131

## Test 1: HTTP Connectivity
Command:
curl -I --connect-timeout 5 http://13.207.198.131

Observed result:
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)

Status: PASS

Conclusion:
The EC2 instance returned a successful HTTP response from Nginx.

## Other Tests
- SSH connectivity: Not yet verified.
- HTTPS connectivity: Not yet verified.
- Unauthorized-source blocking: Not yet verified.
- NACL rule configuration and subnet association: Verified through AWS CLI.

## Notes
The observed public IP can change after stopping and starting an
instance unless an Elastic IP is configured. Verify the current IP
before repeating connectivity tests.
