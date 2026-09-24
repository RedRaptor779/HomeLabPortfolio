# PVE2 Dell Optiplex 3060
Services and Media

## ProxMox Virtual Environment
https://192.168.100.4:8006/

## 6tb External SAS Drive
Connected via USB->SAS adapter and mounted in a drive tray 

## Containers 

### Docker Music Stack
LXC 100 music-stack http://192.168.100.7/
- **Navidrome** - [link](https://www.navidrome.org/)  
  Self hosted music streaming client. Supports Subsonic API as well as a native web interface. Runs on port 4533.  
- **Lidarr** - [link](https://lidarr.audio/)  
  Self hosted music management and automation tool. Runs on port 8686.  

### Invidious Docker
LXC 101 invidious http://192.168.100.8
- **Invidious** - [link](https://invidious.io/)
  Self hosted YouTube front-end with no ads or tracking. Runs on port 3000.
