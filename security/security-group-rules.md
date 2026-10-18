# Security Group Configuration

## Project
AWS VPC Connectivity Lab

## VPC
- VPC ID: vpc-0caa65075d440bd58
- CIDR: 10.0.0.0/16
- Region: ap-south-1

## Security Group
- Name: vpc-connectivity-lab-sg
- ID: sg-0b106e335649a2278

## Inbound Rules

| Protocol | Port | Source | Justification |
|---|---|---|---|
| TCP | 22 | 27.59.62.249/32 | Restrict SSH to the current public IP |
| TCP | 22 | Other configured /32 addresses | Additional explicitly allowlisted SSH sources |
| TCP | 80 | 0.0.0.0/0 | Allow public HTTP access |
| TCP | 443 | 0.0.0.0/0 | Allow public HTTPS access when HTTPS is configured |

## Outbound Rules
- All outbound IPv4 traffic is currently allowed.

## Security Notes
- Restrict SSH to trusted IP addresses.
- Remove obsolete SSH allowlist entries.
- HTTPS requires a configured HTTPS server and valid TLS certificate.
- Review broad outbound permissions before production use.
