# Network ACL Configuration

## Custom Public NACL
- NACL ID: acl-037d90c25614b3e78
- Name: vpc-connectivity-public-nacl
- Public Subnet: subnet-00beaa61e9f1ada32
- Public Subnet CIDR: 10.0.1.0/24

## Inbound Rules

| Rule | Protocol | Port | Source | Action |
|---|---|---|---|---|
| 100 | TCP | 22 | 27.59.62.249/32 | Allow |
| 110 | TCP | 80 | 0.0.0.0/0 | Allow |
| 120 | TCP | 443 | 0.0.0.0/0 | Allow |
| 130 | TCP | 1024-65535 | 0.0.0.0/0 | Allow |
| 140 | UDP | 1024-65535 | 0.0.0.0/0 | Allow |

## Outbound Rules

| Rule | Protocol | Port | Destination | Action |
|---|---|---|---|---|
| 100 | TCP | 80 | 0.0.0.0/0 | Allow |
| 110 | TCP | 443 | 0.0.0.0/0 | Allow |
| 120 | TCP | 1024-65535 | 0.0.0.0/0 | Allow |
| 130 | UDP | 53 | 0.0.0.0/0 | Allow |
| 140 | TCP | 53 | 0.0.0.0/0 | Allow |

## Private Subnet
- Subnet ID: subnet-0f6aea71cf8a9b070
- CIDR: 10.0.2.0/24
- The default NACL remains associated with this subnet.

## Security Notes
- Network ACLs are stateless.
- Review return-traffic requirements for each application.
- Broad ephemeral-port rules are for this lab and should be restricted where practical.
- Review DNS, ICMP, and other required protocols before production use.
