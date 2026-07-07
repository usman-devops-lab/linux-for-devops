# Phase 4: Linux Networking Commands for DevOps

This phase documents my learning of important Linux networking commands used in DevOps, cloud, server management, troubleshooting, and system administration.

In this phase, I practiced commands that help check network connectivity, IP addresses, routing tables, DNS resolution, open ports, services, firewall rules, domain information, packet routes, and file downloads from the internet.

## Topics Covered

- Linux networking basics
- Connectivity checking commands
- Network interface and IP address commands
- Routing table commands
- Port and service checking commands
- DNS troubleshooting commands
- Local network checking commands
- Domain information commands
- File download commands
- Firewall rule commands
- Network scanning commands
- Live monitoring commands
- curl vs wget difference
- Beginner DevOps network troubleshooting flow

## Commands Practiced

### Connectivity Commands

- `ping`
- `traceroute`
- `tracepath`
- `mtr`

### Network Interface and IP Commands

- `ip`
- `ifconfig`
- `hostname`
- `iwconfig`

### Ports and Services Commands

- `ss`
- `netstat`
- `nc`
- `telnet`

### DNS Troubleshooting Commands

- `nslookup`
- `dig`

### Local Network Commands

- `arp`
- `ifplugstatus`

### Domain Information Command

- `whois`

### Routing and Scanning Commands

- `route`
- `nmap`

### File Download and HTTP Commands

- `wget`
- `curl`

### Monitoring and Firewall Commands

- `watch`
- `iptables`

## Why This Phase Is Important for DevOps

Networking is one of the most important parts of DevOps because servers, cloud instances, containers, applications, databases, CI/CD tools, and websites all communicate through networks.

A DevOps engineer should know how to:

- Check whether a server is reachable
- Check whether internet is working
- Check whether DNS is resolving correctly
- Check IP addresses and network interfaces
- Check open ports and running services
- Troubleshoot slow or unreachable websites
- Check routing and gateway issues
- Test TCP and UDP ports
- Download files from URLs
- Check firewall rules
- Scan hosts and ports
- Monitor command output live

## Beginner DevOps Network Troubleshooting Flow

When a network is not working, I can follow this order:

```bash
hostname
ip addr
ip route
ping -c 4 8.8.8.8
ping -c 4 google.com
dig google.com
ss -tulnp
nc -zv server.com 443
traceroute google.com
mtr google.com
