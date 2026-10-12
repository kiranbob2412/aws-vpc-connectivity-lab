# AWS VPC Traffic Flow

## Internet to a Public Instance

1. The VPC has an attached Internet Gateway.
2. The public route table contains 0.0.0.0/0 pointing to the IGW.
3. The instance needs a public IPv4 address for direct public IPv4
   connectivity through the IGW.
4. Security groups, network ACLs, and host firewalls must permit traffic.

A public route alone does not make an instance internet-accessible.

## Public Subnet to Private Subnet

Resources in the same VPC can communicate using the VPC local route
when security controls permit the required traffic.

## Private Subnet Internet Isolation

The private route table has no direct internet default route.
Internet egress would require a separately configured mechanism,
such as a NAT Gateway or suitable VPC endpoints.

## Verification

Inspect routes and security controls independently. A failed ping
alone does not prove subnet isolation. Record actual results after
deployment.
