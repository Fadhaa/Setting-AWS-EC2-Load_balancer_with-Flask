
# Step 1: Launch EC2 Instances inside Custom VPC (`myvpc1`)

This guide walks you through launching EC2 instances in your custom VPC (`myvpc1`) using the AWS Console.

---

## ✅ Prerequisites

Before launching EC2 instances, make sure you've already created:

- A **VPC** named `myvpc1`
- Two **public subnets**: `mysubnet1` and `mysubnet2` in different Availability Zones
- A **Route Table** named `mytable1` (associated with both subnets)
- An **Internet Gateway** named `myiqw1` (attached to `myvpc1`)

---
