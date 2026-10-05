R1
Firstly I deleted the subinterfaces.(ie. g0/0.10, g0/0.20..)
Then I configured  g0/0 interface with an IP address

SW2(L3 SW)
I reset G1/0/2 (default int g1/0/2)
Configured the port to be a routed port (no switchport) and gave it the correct IP
Then I turned on layer 3 forwarding with "ip routing" and set a default gateway.
Configuring SVI-s:
I made sure the correct VLAN-s existed.
I created the SVI-s then assigned the IP-s.
*Vlan10                 10.0.0.62       YES manual up                    up
Vlan20                 10.0.0.126      YES manual up                    up
Vlan30                 10.0.0.190      YES manual up                    up*



Lab file from Jeremy's It Lab's Free CCNA Course

