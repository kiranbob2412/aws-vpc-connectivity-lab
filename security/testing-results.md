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
# Security and Connectivity Testing Results

## AWS Environment
- Region: ap-south-1
- VPC ID: vpc-0caa65075d440bd58
- Public Subnet: subnet-00beaa61e9f1ada32
- Private Subnet: subnet-0f6aea71cf8a9b070
- Custom Public NACL: acl-037d90c25614b3e78
- Security Group: sg-0b106e335649a2278

## Test Results

| Test | Result | Evidence |
|---|---|---|
| VPC and subnet configuration | PASS | AWS CLI verification |
| Public route through IGW | PASS | Route table verification |
| Private subnet route isolation | PASS | No default Internet Gateway route |
| SSH connectivity | PASS | Successful SSH login |
| HTTP connectivity | PASS | HTTP/1.1 200 OK |
| HTTPS connectivity | PASS | HTTP/1.1 200 OK using curl -k |
| Nginx configuration | PASS | nginx -t successful |
| Nginx HTTPS listener | PASS | Port 443 listening on IPv4 and IPv6 |
| NACL configuration and association | PASS | AWS CLI verification |
| NACL allow/deny behavior | PASS | HTTP blocked by NACL deny rule; restored allow rule and HTTP returned 200 OK |
| Private workload connectivity | NOT TESTED | No private workload test performed |

## HTTPS Test

Command:
curl -k -I https://13.201.67.75

Observed result:
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)

Status: PASS

Note:
The certificate is self-signed. The -k option skips certificate
verification for this connectivity test.

## Limitations
- Private subnet workload connectivity has not been tested.
- Public IP addresses can change after stopping and starting an instance.
- AWS resource costs must be reviewed before final cleanup.
## NACL Allow/Deny End-to-End Test

### Objective
Verify that the custom Network ACL can block and restore public HTTP traffic.

### Environment
- AWS Region: ap-south-1
- NACL ID: acl-037d90c25614b3e78
- Inbound Rule: 110
- Protocol: TCP
- Port: 80
- CIDR: 0.0.0.0/0

### Test Procedure and Results

1. Verified that public HTTP connectivity returned HTTP 200 OK.
2. Changed inbound NACL Rule 110 to deny TCP port 80.
3. Verified that the rule action was set to deny using AWS CLI.
4. Tested public HTTP connectivity; curl timed out after 5 seconds.
5. Restored inbound Rule 110 to allow TCP port 80.
6. Tested public HTTP connectivity again; HTTP returned 200 OK.

### Result
PASS — NACL deny behavior blocked public HTTP traffic, and
restoring the allow rule restored HTTP connectivity.

### Scope
This test validates inbound NACL behavior for HTTP traffic.
It does not validate every NACL rule or private subnet connectivity.
