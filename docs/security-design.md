# Security Design

## Network Isolation

The public subnet has a default route to the Internet Gateway.
The private subnet has only the VPC local route in the initial design.

## Inbound Access

Do not permit SSH (`TCP/22`) from `0.0.0.0/0`.

If SSH is needed for the lab, restrict the source to an approved
administrator IP address or use AWS Systems Manager Session Manager
with the required IAM permissions and instance configuration.

## Least Privilege

Use only the IAM permissions required to validate, deploy, inspect,
and delete this lab's resources.

Avoid broad administrator permissions for routine workloads.

## Credentials

- Never commit access keys, secret keys, session tokens, or MFA codes.
- Do not put credentials in CloudFormation templates or README files.
- Use approved AWS credential mechanisms and rotate exposed credentials.

## Verification

Review route tables, security groups, network ACLs, and host firewalls
separately when troubleshooting connectivity.

## Scope

This is a learning lab. It is not a complete production architecture.
Production use would require additional controls and review.
