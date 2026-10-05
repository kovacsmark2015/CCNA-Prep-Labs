# Inter-VLAN Routing Lab: Layer 3 Switch with SVIs


## R1

1. Deleted the subinterfaces (i.e. `g0/0.10`, `g0/0.20`, ...).
2. Configured the `g0/0` interface with an IP address.

## SW2 (L3 Switch)

### Routed port

1. Reset the interface to its defaults:
   ```
   default interface g1/0/2
   ```
2. Configured the port as a routed port (`no switchport`) and gave it the correct IP address.
3. Turned on Layer 3 forwarding and set a default gateway:
   ```
   ip routing
   ```

### SVIs

1. Made sure the correct VLANs existed.
2. Created the SVIs.
3. Assigned the IP addresses.

Verification:

```
Interface              IP-Address      OK? Method Status                Protocol
Vlan10                 10.0.0.62       YES manual up                    up
Vlan20                 10.0.0.126      YES manual up                    up
Vlan30                 10.0.0.190      YES manual up                    up
```
> Lab file from Jeremy's IT Lab's Free CCNA Course.
