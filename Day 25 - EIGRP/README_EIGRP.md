# EIGRP Lab: Dynamic Routing with Unequal-Cost Load Balancing

## Overview

This lab covers the following configuration steps:

-  Configured loopback addresses on all routers
-  Configured EIGRP dynamic routing
-  Configured unequal-cost load balancing

## Verification

### R1 Routing Table

```text
     1.0.0.0/32 is subnetted, 1 subnets
C       1.1.1.1 is directly connected, Loopback0
     2.0.0.0/32 is subnetted, 1 subnets
D       2.2.2.2 [90/130816] via 10.0.12.2, 00:00:06, GigabitEthernet0/0
     3.0.0.0/32 is subnetted, 1 subnets
D       3.3.3.3 [90/156160] via 10.0.13.2, 00:00:06, FastEthernet1/0
     4.0.0.0/32 is subnetted, 1 subnets
D       4.4.4.4 [90/156416] via 10.0.12.2, 00:00:06, GigabitEthernet0/0
                [90/158720] via 10.0.13.2, 00:00:06, FastEthernet1/0
     10.0.0.0/30 is subnetted, 4 subnets
C       10.0.12.0 is directly connected, GigabitEthernet0/0
C       10.0.13.0 is directly connected, FastEthernet1/0
D       10.0.24.0 [90/28416] via 10.0.12.2, 00:00:06, GigabitEthernet0/0
D       10.0.34.0 [90/30720] via 10.0.13.2, 00:00:06, FastEthernet1/0
D    192.168.4.0/24 [90/28672] via 10.0.12.2, 00:00:06, GigabitEthernet0/0
                    [90/30976] via 10.0.13.2, 00:00:06, FastEthernet1/0
```

## Analysis

The last EIGRP route (`192.168.4.0/24`) has two paths installed:

| Path      | Next hop    | Interface           | Metric  | Role      |
|-----------|-------------|---------------------|---------|-----------|
| Primary   | `10.0.12.2` | GigabitEthernet0/0  | `28672` | Preferred |
| Secondary | `10.0.13.2` | FastEthernet1/0     | `30976` | Backup    |

Because unequal-cost load balancing is enabled, EIGRP installs both routes and distributes traffic across them, even though `FastEthernet1/0` is the slower link.

> Lab file from Jeremy's IT Lab's Free CCNA Course.