# Cisco ASA 5506-X

This firewall connects to my home WiFi router (out of scope for this documentation) via a double NAT. For security and simplicity, this was the best implementation. ACL rules on the firewall isolate 
my home WiFi network from my Lab network with few exceptions such as DNS. Management is handled via a TailScale Subnet Router []. Connects to the TP-Link Switch [] for Layer 2 connectivity. 

## Interfaces

GE1/1  
"Outside"  
10.0.0.50 255.255.255.0  
Security Level 0  

GE1/2  
"Inside"  
192.168.100.1 255.255.255.0  
Security Level 100  

## ACLs

### DNS Allow
Only allow traffic from outside the firewall for DNS:  
```cisco
object network adguard-dns-udp
 host 192.168.100.5  
object network adguard-dnss-tcp  
 host 192.168.100.5  
access-list OUTSIDE_IN extended permit udp 10.0.0.0 255.255.255.0 host 192.168.100.5 eq domain  
access-list OUTSIDE_IN extended permit tcp 10.0.0.0 255.255.255.0 host 192.168.100.5 eq domain
```

## Routing (Network Isolation)
Static Route for routing internet traffic up to the WiFi router:  
```cisco
route outside 0.0.0.0 0.0.0.0 10.0.0.1 1
```

