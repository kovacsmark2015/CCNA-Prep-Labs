# Floating Static Routes Lab

## Task 1: Network Investigation

I tested and investigated the network to answer the lab's questions.

- Enterprise A is using **OSPF** as its IGP.

The route to R2's network on R1 was added by OSPF:

```
O       10.0.2.0/24 [110/2] via 10.0.0.2, 00:30:55, GigabitEthernet0/2/0
```

## Task 2: Floating Static Routes

I configured floating static routes on R1 and R2 through ISP A.

- I achieved this by setting the static routes' administrative distance higher than that of OSPF (110).
- This was done so that if the direct connection between the two routers in the enterprise fails, the routers will use the static routes as a backup route.

### Commands

```
R1(config)#ip route 10.0.2.0 255.255.255.0 203.0.113.0 111
R2(config)#ip route 10.0.1.0 255.255.255.0 203.0.113.5 111
```

### Result

- The new static routes only appear in the routing table after deliberately shutting down the interface between the routers.
- After this, the static routes get added to the routing tables and traffic is routed through the ISP.

> Lab file from Jeremy's IT Lab's Free CCNA Course.
