# AWS VPC Connectivity Lab 🚀

## Project Overview

This project builds an AWS VPC with public and private subnets using
AWS CloudFormation. It demonstrates subnet routing, Internet Gateway
configuration, and network connectivity verification.

## Architecture

| Component | CIDR |
|---|---|
| VPC | 10.0.0.0/16 |
| Public subnet | 10.0.1.0/24 |
| Private subnet | 10.0.2.0/24 |

The public subnet uses an Internet Gateway default route.
The private subnet has no direct internet default route.

## Technologies

- AWS VPC
- AWS CloudFormation
- AWS CLI v2
- cfn-lint
- Linux / Ubuntu
- Git and GitHub

## Repository Structure

- `templates/vpc-setup.yaml` — Infrastructure as Code
- `docs/traffic-flow.md` — Network traffic flow
- `docs/security-design.md` — Security design
- `docs/verification-report.md` — Verification results
- `docs/cleanup.md` — Resource cleanup instructions
- `diagrams/` — Architecture diagram
- `screenshots/` — AWS Console evidence
- `tests/` — Verification scripts

## Validation

The template passed local cfn-lint validation and AWS CloudFormation
template validation. Deployment and connectivity tests remain pending.

## Security

- Never commit AWS credentials or secrets.
- Avoid unrestricted SSH access.
- Apply least-privilege IAM permissions.
- Review costs before deployment.
- Clean up resources after testing.

## Author

Kiran Babu
