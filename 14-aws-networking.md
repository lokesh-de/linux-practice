# AWS Networking and EC2

## Introduction to AWS Networking

AWS networking allows users to create isolated virtual networks in the cloud, launch virtual machines, and control traffic using firewall rules. Understanding VPC, EC2, Security Groups, and Network ACLs is essential for deploying secure cloud infrastructure.

## Index of Concepts Covered

### VPC and Networking Setup
- `VPC` – Create isolated virtual network
- `CIDR Block` – Define IP address range
- `Subnet` – Public and Private network segmentation
- `Internet Gateway` – Enable internet access
- `Route Table` – Control traffic routing

### EC2 Instance Management
- Launch EC2 instance
- Select AMI (Amazon Linux / Ubuntu)
- Choose instance type (t2.micro)
- Attach key pair
- Access using Public IP

### Security Groups
- Instance-level firewall
- Inbound rules
- Outbound rules
- Port access configuration

### Network ACL (NACL)
- Subnet-level firewall
- Allow and Deny rules
- Stateless traffic filtering
- Rule number priority

### Connectivity Troubleshooting
- Port blocked in Security Group
- NACL blocking traffic
- Internet Gateway not attached
- Route table misconfiguration
- Instance not in public subnet

## VPC and Networking Setup

### Creating a VPC
To create a VPC:
- Go to AWS VPC Dashboard
- Click Create VPC
- Provide CIDR block (Example: 10.0.0.0/16)

Example CIDR:
```
10.0.0.0/16
```

### Creating a Public Subnet
Example subnet:
```
10.0.1.0/24
```

### Configuring Internet Gateway
Steps:
- Create Internet Gateway
- Attach it to your VPC

### Configuring Route Table
To allow internet access:
```
Destination: 0.0.0.0/0
Target: Internet Gateway
```

## EC2 Instance Management

### Launching an EC2 Instance
Steps:
- Go to EC2 Dashboard
- Click Launch Instance
- Select AMI (Amazon Linux / Ubuntu)
- Choose instance type (t2.micro)
- Select VPC and Subnet
- Attach Security Group
- Add Key Pair
- Launch

### Accessing EC2 via SSH
```bash
ssh -i mykey.pem ec2-user@<public-ip>
```
- Press Enter to connect
- Make sure port 22 is open in Security Group

## Security Groups

### Opening SSH Port
To allow SSH access:
```
Type: SSH
Protocol: TCP
Port: 22
Source: 0.0.0.0/0
```

### Opening HTTP Port
To allow web traffic:
```
Type: HTTP
Protocol: TCP
Port: 80
Source: 0.0.0.0/0
```

### Opening Custom Application Port
Example for port 3000:
```
Type: Custom TCP
Port: 3000
Source: 0.0.0.0/0
```

### Security Group Characteristics
- Stateful
- Only Allow rules supported
- Applied at instance level

## Network ACL (NACL)

### Example Allow Rule
```
Rule #100
Type: HTTP
Protocol: TCP
Port: 80
Source: 0.0.0.0/0
Action: ALLOW
```

### Example Deny Rule
```
Rule #200
Type: ALL Traffic
Source: 0.0.0.0/0
Action: DENY
```

### NACL Characteristics
- Stateless
- Supports Allow and Deny
- Rule order matters (lowest number first)
- Applied at subnet level

## Connectivity Troubleshooting

### Checking Security Group
Ensure required port is open:
```
Inbound Rule → Required Port → Source Allowed
```

### Checking Route Table
```
0.0.0.0/0 → Internet Gateway
```

### Checking Traffic Flow
```
User → Internet → Internet Gateway → Route Table → Subnet → NACL → Security Group → EC2
```

### If Traffic is Blocked
- Verify Security Group rules
- Verify NACL inbound and outbound rules
- Ensure Internet Gateway is attached
- Confirm instance has Public IP
- Ensure instance is in Public Subnet