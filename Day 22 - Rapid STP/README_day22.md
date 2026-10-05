# Spanning Tree Protocol Lab

This lab was about practicing everything I learned about Spanning Tree Protocol in the preceding videos:

- Classic STP
- STP Toolkit
- BPDU Guard and Filter
- Loop Guard
- Root Guard
- Rapid STP

## Task 1: Root Bridge Port Roles

The unusual thing here was that not all ports on the root bridge were designated. This was because the root bridge was connected to a hub. The link type on those ports was shared, and one of them became a backup port.

## Task 2: Port Roles and States

I determined the port role and state of every switch interface. I won't go into the reasoning in detail, only the solution.

**Root bridge:** SW1 (priority 32769, MAC 0005.5E4E.714B, the lowest MAC with all priorities equal)

### SW1 (Root Bridge)

| Interface | Connected to | Role | State |
|---|---|---|---|
| F0/1 | SW2 F0/1 | Designated | Forwarding |
| F0/2 | Hub1 | Designated | Forwarding |
| F0/3 | Hub1 | Backup | Discarding |
| F0/24 | Hub0 (PC1/PC2) | Designated | Forwarding |

### SW2

| Interface | Connected to | Role | State |
|---|---|---|---|
| F0/1 | SW1 F0/1 | Root | Forwarding |
| F0/2 | SW4 F0/2 | Designated | Forwarding |
| G0/1 | SW3 G0/1 | Alternate | Discarding |
| F0/23 | PC4 | Designated | Forwarding |
| F0/24 | PC5 | Designated | Forwarding |

### SW3

| Interface | Connected to | Role | State |
|---|---|---|---|
| F0/1 | SW4 F0/1 | Designated | Forwarding |
| F0/2 | Hub1 | Root | Forwarding |
| G0/1 | SW2 G0/1 | Designated | Forwarding |
| F0/24 | PC3 | Designated | Forwarding |

### SW4

| Interface | Connected to | Role | State |
|---|---|---|---|
| F0/1 | SW3 F0/1 | Root | Forwarding |
| F0/2 | SW2 F0/2 | Alternate | Discarding |
| F0/24 | PC6 | Designated | Forwarding |

## Task 3: RSTP Link Types

I manually configured the RSTP link types. Here is a summary of what I configured:

### SW1

| Interface | Connected to | Link Type | Reason |
|---|---|---|---|
| F0/1 | SW2 F0/1 | Point-to-point | Direct switch-to-switch link |
| F0/2 | Hub1 | Shared | Connected to a hub (shared medium) |
| F0/3 | Hub1 | Shared | Connected to a hub (shared medium) |
| F0/24 | Hub0 (PC1/PC2) | Shared | Connected to a hub with multiple devices |

### SW2

| Interface | Connected to | Link Type | Reason |
|---|---|---|---|
| F0/1 | SW1 F0/1 | Point-to-point | Direct switch-to-switch link |
| F0/2 | SW4 F0/2 | Point-to-point | Direct switch-to-switch link |
| G0/1 | SW3 G0/1 | Point-to-point | Direct switch-to-switch link |
| F0/23 | PC4 | Point-to-point | Single end device, full duplex |
| F0/24 | PC5 | Point-to-point | Single end device, full duplex |

### SW3

| Interface | Connected to | Link Type | Reason |
|---|---|---|---|
| F0/1 | SW4 F0/1 | Point-to-point | Direct switch-to-switch link |
| F0/2 | Hub1 | Shared | Connected to a hub (shared medium) |
| G0/1 | SW2 G0/1 | Point-to-point | Direct switch-to-switch link |
| F0/24 | PC3 | Point-to-point | Single end device, full duplex |

### SW4

| Interface | Connected to | Link Type | Reason |
|---|---|---|---|
| F0/1 | SW3 F0/1 | Point-to-point | Direct switch-to-switch link |
| F0/2 | SW2 F0/2 | Point-to-point | Direct switch-to-switch link |
| F0/24 | PC6 | Point-to-point | Single end device, full duplex |

> Lab file from Jeremy's IT Lab's Free CCNA Course.
