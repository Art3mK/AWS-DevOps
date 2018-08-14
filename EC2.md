# Elastic Compute Cloud

VM in Cloud.

### EC2 pricing options
- on demand, by the hour (or by the second, linux only)
    * low cost adn flexibility without up-front payments
    * app with short term, spiky workloads
    * developing/testing apps
- reserved (1-3 year contracts, платить заранее)
    * steady state or predictable usage
    * app requires reserved capacity
    * upfront payments to reduce costs
        * Standard RI's (up to 75% off on demand)
        * Convertible RI's (up to 54% off on demand)
            * ability to change attributes of the RI
            * `>=` instance size
        * scheduled RI's (recurring load)
- spot instances
    * apps with flexible start and end times
    * apps that are only feasible at very low compute prices
    * urgent computing needs for large amounts of additional capacity
    * you terminate - you pay for the hour
    * AWS terminates - you get the hour it was terminated in for free
- dedicated hosts - physical EC2 servers (For licenses)
    * regulatory requirements
    * licensing without multi-tenancy support or cloud deployments
    * available on-demand (hourly)
    * 70% off with reserved instance

### DR MC GIFT PiX

![alt](./images/instance_types.png)

- D - (DENSE) dense storage
- R - (RAM) memory optimized
- M - (MAIN) general purpose
- C - (CPU) compute optimized
- G - (Graphics) graphics optimized
- I - (IOPS) high speed storage
- F - (FPGA)
- T - lowest cost, general purpose
- P - (PICS) - graphics/general purpose GPU
- X - Extreme RAM - memory optimized

## Types

- HVM
- PV

## Security groups

Security groups are stateful.
- all inbound is blocked by default
- all outbound is allowed by default
- changes take effect immediately
- any number of EC2 instances within a security group
- multiple groups per EC2 instance
- no block rules

## Metadata

http://169.254.169.254/latest/meta-data/
http://169.254.169.254/latest/user-data/

## Gothas

- default action is for the EBS to be deleted when the instance is terminated
- termination protection is off by default
- can't encrypt boot volume for standard AMIs
- one subnet - one AZ
- 20 on-demand instances across the instance family by default
- Nitro hypervisor (new, foc C5) vs Xen
- SRV-IO on HVM AMI with drivers, ENA elastic network adapter
- no additional fee for enhanced networking

## AMIs

- AMIs are regional
- can copy between regions (console, command line, API)

## Q. What is a cluster placement group?

A cluster placement group is a logical entity that enables creating a cluster of instances by launching instances as part of a group. The cluster of instances then provides low latency connectivity between instances in the group. Cluster placement groups are created through the Amazon EC2 API or AWS Management Console.
