# Highly-Available-Web-Application
Designed and deployed a highly available, secure web application architecture on AWS using a custom VPC, Auto Scaling, a Bastion Host, and an Application Load Balancer — following AWS best practices for placing compute resources in private subnets while still allowing controlled access and public reachability.
'![Architecture Diagram](Architecture.png)'

## Problem Statement

A basic web app running on a single EC2 instance in a public subnet has three failure points: no redundancy if that instance or its AZ goes down, no isolation between public-facing and internal resources, and no way to handle traffic spikes.

## How This Architecture Solves It

- **Availability** → Multi-AZ Auto Scaling Group with 2+ EC2 instances behind an ALB. If one instance or AZ fails, the ALB routes around it and the ASG maintains the minimum healthy instance count.
- **Security** → EC2 instances live in private subnets with no public IP. The only way in is through a Bastion Host (SSH) or the ALB (HTTP) — nothing else is reachable from the internet.
- **Scalability** → The ALB distributes load evenly across instances, and the ASG scales out to handle increased traffic.
