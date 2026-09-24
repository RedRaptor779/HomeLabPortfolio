# Cisco ASA 5506-X

This firewall connects to my home WiFi router (out of scope for this documentation) via a double NAT. For security and simplicity, this was the best implementation. ACL rules on the firewall isolate 
my home WiFi network from my Lab network with few exceptions such as DNS. Management is handled via a [TailScale Subnet Router](https://github.com/RedRaptor779/HomeLabPortfolio/blob/main/Machines/PVE1.md#tailscale-subnet-router). Connects to the [TP-Link Switch](https://github.com/RedRaptor779/HomeLabPortfolio/blob/main/Network/TP-Link_TL-SG108E.md#tp-link-tl-sg108e-easy-smart-managed-switch) for Layer 2 connectivity. 

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
```ios
object network adguard-dns-udp
 host 192.168.100.5  
object network adguard-dnss-tcp  
 host 192.168.100.5

access-list OUTSIDE_IN extended permit udp 10.0.0.0 255.255.255.0 host 192.168.100.5 eq domain  
access-list OUTSIDE_IN extended permit tcp 10.0.0.0 255.255.255.0 host 192.168.100.5 eq domain
```

### Invidious Allow
```Cisco
object network obj-Invidious
 nat (inside,outside) static interface service tcp 3000 3000 

access-list OUTSIDE_IN line 3 extended permit tcp 10.0.0.0 255.255.255.0 host 192.168.100.8 eq 3000 (hitcnt=112) 0xd6028d32
```

## Routing (Network Isolation)
Static Route for routing internet traffic up to the WiFi router:  
```Cisco
route outside 0.0.0.0 0.0.0.0 10.0.0.1 1
```

