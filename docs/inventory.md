## Server: zzaid351-X570

### Overview
 Static hostname: zzaid351-X570-AORUS-ELITE-WIFI
       Icon name: computer-desktop
         Chassis: desktop 🖥️
Operating System: Ubuntu 24.04.5 LTS
          Kernel: Linux 7.0.0-28-generic
    Architecture: x86-64
 Hardware Vendor: Gigabyte Technology Co., Ltd.
  Hardware Model: X570 AORUS ELITE WIFI
Firmware Version: F41c
   Firmware Date: Tue 2026-08-18
    Firmware Age: 1month 2w 5d

###Network Interfaces
| Interface |   Status |    IP   |  Description  |
lo               UNKNOWN        127.0.0.1/8 [Loopback]
enp5s0           UP             192.168.1.112/24 [Ethernet Port]
virbr0           DOWN           192.168.122.1/24 [Virtual bridge from libvirt/KVM]
br-851659e2c0b8  UP             172.18.0.1/16 [Docker Network: media containers, (internal)]
docker0          UP             172.17.0.1/16 [Docker default bridge]
br-c6e4eeaf525c  UP             172.19.0.1/16 [Docker Network: Wazuh container]

### Listening Services 
| Category | Service | Port(s) | Runs as | Why it's open |

| Admin | SSH | 22/tcp | systemd | Encrypted remote administration of the server |
| Admin | xrdp | 3389/tcp | systemd | Remote desktop for GUI access |
| Wazuh | Dashboard | 8443/tcp | Docker | Web UI for the SIEM, accessed from workstation |
| Wazuh | Agent enrollment / events | 1514, 1515/tcp | Docker | Receives events from enrolled agents |
| Wazuh | Manager API | 55000/tcp | Docker | Opened by default config; not needed on LAN, restriction pending |
| Wazuh | Indexer | 9200/tcp | Docker | Opened by default config; not needed on LAN, restriction pending |
| Wazuh | Syslog receiver | 514/udp | Docker | Receives logs from TP-Link router |
| File sharing | Samba | 139, 445/tcp | systemd | File sharing between server and LAN devices |
| Media | Plex | 32400/tcp | systemd | Media server |
| Media | Media automation stack | 6500, 6881, 7878, 8090, 8191, 8989, 9696/tcp; 6881/udp | Docker | Media library management and downloads |
| Home automation | Home automation stack (Home Assistant, MQTT, camera streams) | 1883, 8123, 9001, 18555, 34421, 35113/tcp | Docker (host network) | Smart home control, Zigbee devices, and camera feeds |
| Web | nginx | 80, 443/tcp | systemd | Legacy HTTPS proxy for AMP panel; unused, pending removal |
| Leftover | AMP | 8081, 2223/tcp; 12820/udp | systemd | Game servers retired; pending removal |

_Background/discovery listeners (UDP): mDNS 5353 (avahi), Plex discovery 1900 + 32410–32414, NetBIOS 137–138 (Samba)._
All listed services are reachable from the LAN (192.168.1.0/24) via a blanket ufw allow rule; Docker-published ports bypass ufw regardless. No services are reachable from the internet.


##Endpoint Device

###Overview
          Hostname: ZAID
              Role: Primary workstation, monitored endpoint
  Operating System: Windows 11 Pro
             Build: 10.0.26200
      Architecture: x86-64
               CPU: AMD Ryzen 7 7800X3D 8-Core
               RAM: 32 GB
   Hardware Vendor: Micro-Star International Co., Ltd. (MSI)
    Hardware Model: MS-7E62
  Firmware Version: 2.A48
     Firmware Date: 2025-09-08
            LAN IP: 192.168.1.14 (Ethernet 2, DHCP)
       Wazuh Agent: ZaidPC

### Network Interfaces
| Interface | Hardware | IP | Purpose |

| Ethernet 2 | Realtek PCIe Ethernet | 192.168.1.14/24 | Physical LAN connection |
| Wi-Fi 2, Wi-Fi 4, Wi-Fi 6 | Qualcomm FastConnect 7800 (Wi-Fi 7) | Not connected | Onboard Wi-Fi, one virtual interface per band (unused, wired instead) |
| NordLynx | NordLynx Tunnel | 10.5.0.2 | NordVPN tunnel (WireGuard-based) |
| OpenVPN Data Channel Offload | OpenVPN DCO | 10.100.0.2 | NordVPN tunnel (OpenVPN) |
| Local Area Connection 2 | TAP-NordVPN Adapter V9 | Not connected | NordVPN legacy OpenVPN adapter |

### Listening Services
| Category | Service | Port(s) | Reachable from LAN | Why it's open |
 Windows core | RPC, SMB, NetBIOS | 135, 139, 445/tcp | No (firewalled) | Default OS services |
| Windows core | Network discovery (UPnP / WSD) | 2869, 5357/tcp | Yes | Default on Private networks |
| Windows core | Connected Devices Platform | 5040/tcp | Yes | Phone Link / nearby sharing |
| Windows core | Dynamic RPC | 49664–49690/tcp | No (firewalled) | Core service communication |
| Remote access | Remote Desktop | 3389/tcp | No (firewalled) | |
| Legacy | Windows Media Player Network Sharing | 554, 10243, 11021/tcp | Yes (554, 10243) | Unused; pending disable |
| Apps | Syncthing | 22000/tcp | Yes | File sync with server |
| Apps | Steam | 27036/tcp | Yes | In-home streaming / LAN discovery |
| Apps | Spotify | 63267/tcp | Yes | Spotify Connect discovery |
| Apps | spacedesk | 28252/tcp | No (firewalled) | Tablet as extra display |
| Apps | Razer Synapse | 49681/tcp | No (firewalled) | Peripheral management service |
| Apps | Lian Li L-Connect | 1462/tcp | No (localhost-only) | Fan/RGB control |

_Firewall: enabled on all profiles, default inbound deny; network profile Private. Exposure verified by nmap scan from server (2026-10-06)._
