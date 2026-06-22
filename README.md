# AWS VPC with Public and Private Subnets

## Project Overview

This project demonstrates the creation and configuration of a custom Virtual Private Cloud (VPC) in AWS with public and private subnets, Internet Gateway, NAT Gateway, and Route Tables to implement a secure multi-tier network architecture.

## Objective

* Create a custom VPC.
* Configure public and private subnets across multiple Availability Zones.
* Enable internet access for public resources.
* Provide secure outbound internet access for private resources using a NAT Gateway.
* Implement network segmentation for Web, Application, and Database tiers.

## Environment

| Parameter      | Value                                 |
| -------------- | ------------------------------------- |
| Cloud Provider | AWS                                   |
| Region         | Asia Pacific (Hyderabad) - ap-south-2 |
| VPC Name       | custom-vpc-yt                         |
| CIDR Block     | 192.168.0.0/16                        |

---

## Architecture

```text
Internet
    |
    v
Internet Gateway
    |
+------------------+
|   Public Subnets |
+------------------+
       |
       v
   NAT Gateway
       |
+------------------+
| Private Subnets  |
|  (App Tier)      |
+------------------+
       |
       v
+------------------+
| Private Subnets  |
|   (DB Tier)      |
+------------------+
```

---

## VPC Configuration

| Parameter          | Value                    |
| ------------------ | ------------------------ |
| VPC Name           | custom-vpc-yt            |
| VPC CIDR           | 192.168.0.0/16           |
| Subnets            | 6                        |
| Availability Zones | ap-south-2a, ap-south-2b |

---

## Subnet Configuration

### Public Subnets

| Subnet Name       | CIDR Block      | AZ          |
| ----------------- | --------------- | ----------- |
| cvpc-yt-public-2A | 192.168.0.0/26  | ap-south-2a |
| cvpc-yt-public-2B | 192.168.0.64/26 | ap-south-2b |

### Private Application Subnets

| Subnet Name    | CIDR Block       | AZ          |
| -------------- | ---------------- | ----------- |
| cvpc-yt-app-2A | 192.168.1.0/25   | ap-south-2a |
| cvpc-yt-app-2B | 192.168.1.128/25 | ap-south-2b |

### Private Database Subnets

| Subnet Name   | CIDR Block       | AZ          |
| ------------- | ---------------- | ----------- |
| cvpc-yt-db-2A | 192.168.2.0/25   | ap-south-2a |
| cvpc-yt-db-2B | 192.168.2.128/25 | ap-south-2b |

---

## Internet Gateway Configuration

* Internet Gateway Name: `cvpc-IGW`
* Attached to VPC: `custom-vpc-yt`
* Status: Attached

Purpose:

* Provides internet connectivity for public subnets.

---

## Route Tables

### Public Route Table

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

Associated with:

* Public Subnet 2A
* Public Subnet 2B

### Private Route Table

| Destination      | Target |
| ---------------- | ------ |
| Local VPC Routes | Local  |

Associated with:

* App Subnet 2A
* App Subnet 2B
* DB Subnet 2A
* DB Subnet 2B

---

## NAT Gateway Configuration

| Parameter         | Value     |
| ----------------- | --------- |
| NAT Gateway Name  | MyNatGw   |
| Connectivity Type | Public    |
| State             | Available |

Purpose:

* Allows private instances to access the internet for updates and package downloads without exposing them publicly.

---

## Security Features

* Network segmentation using separate subnet tiers.
* Public-facing resources isolated from private workloads.
* Database subnets remain private and inaccessible from the internet.
* NAT Gateway used for secure outbound connectivity.

---

## Verification

* Successfully created VPC and subnets.
* Internet Gateway attached and configured.
* Public subnets can access the internet.
* Private subnets remain isolated.
* NAT Gateway operational for outbound traffic.

---

## Learning Outcomes

Through this project, I learned:

* AWS VPC architecture design.
* CIDR block planning and subnetting.
* Public and private subnet implementation.
* Internet Gateway and NAT Gateway configuration.
* Route Table association and traffic routing.
* Secure multi-tier cloud networking design.

---

## Screenshots

Add screenshots for:

* VPC Dashboard
* Subnet Configuration
* Internet Gateway
* Route Tables
* NAT Gateway
* Network Architecture Diagram
