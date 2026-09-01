# PVE1 Dell Optiplex 3070
Infrastructure and Management Services  

## ProxMox Virtual Environment
https://192.168.100.3:8006/

## NUT
[Network UPS Tools](https://networkupstools.org/)  

Running within ProxMox shell. Communicates directly with the UPS via a console cable and polls for information such as battery percentage, load, runtime, etc. Hosts a server 
on port 3493 that allows other systems to read and communicate with NUT for easy display, monitoring, and notifications for events. 

## Containers 

### Tailscale Subnet Router
LXC 100 tailscale-gateway-mgmt  

Running a [TailScale Subnet Router](https://tailscale.com/docs/features/subnet-routers) gateway for secure access to the entire internal homelab network. Allows for access to all services and hardware from outside the local 
network. 

### ADGuard DNS
LXC 101 adguard-dns http://192.168.100.5/  

Running a DNS sinkhole called [AdGuard](https://adguard.com/en/welcome.html?_plc=en). Acts as a local DNS server and filters DNS queries based on a filter list to reject 
advertisement and tracking domains before querying CloudFlare's DNS.

### Docker Infrastructure Stack
LXC 102 docker-infra http://192.168.100.6/
- **Homarr** - [link](https://homarr.dev/)  
  Dashboard that provides links, and monitoring/diagnostic data of services via APIs. Runs on port 7575.
- **PeaNUT** - [link](https://github.com/Brandawg93/PeaNUT)  
  Dashboard that monitors and tracks UPS diagnostic data via the NUT server. Runs on port 8080.
  
