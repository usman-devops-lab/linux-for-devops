# Phase 4 Resources

This file contains useful resources, command references, package installation commands, and practice commands for Phase 4: Linux Networking Commands for DevOps.

---

## Course Reference

Linux For DevOps In One Shot | Complete Beginners to Advanced Linux Hindi

---

## Official Manual Pages

Use the `man` command to read official Linux documentation.

```bash
man ping
man netstat
man ifconfig
man traceroute
man tracepath
man mtr
man nslookup
man telnet
man hostname
man hostnamectl
man ip
man ss
man dig
man whois
man nc
man arp
man route
man nmap
man wget
man curl
man watch
man iptables
```

---

## Help Commands

Use `--help`, `-h`, or command help output to quickly understand options.

```bash
ping --help
ip --help
ss --help
dig -h
traceroute --help
tracepath --help
mtr --help
nmap --help
wget --help
curl --help
watch --help
iptables --help
```

For `nc`:

```bash
nc -h
```

For `whois`:

```bash
whois --help
```

---

## Useful Package Installation Commands

Some networking commands are not installed by default on modern Linux systems.

### Update package list

```bash
sudo apt update
```

### Install old networking tools

```bash
sudo apt install net-tools
```

This package provides:

```text
ifconfig
netstat
route
arp
```

---

### Install DNS tools

```bash
sudo apt install dnsutils
```

This package provides:

```text
nslookup
dig
```

---

### Install traceroute

```bash
sudo apt install traceroute
```

or:

```bash
sudo apt install inetutils-traceroute
```

---

### Install mtr

```bash
sudo apt install mtr
```

---

### Install telnet

```bash
sudo apt install telnet
```

---

### Install netcat

```bash
sudo apt install netcat-openbsd
```

This provides:

```text
nc
```

---

### Install whois

```bash
sudo apt install whois
```

---

### Install nmap

```bash
sudo apt install nmap
```

---

### Install wget

```bash
sudo apt install wget
```

---

### Install curl

```bash
sudo apt install curl
```

---

### Install watch command package

```bash
sudo apt install procps
```

---

### Install iptables

```bash
sudo apt install iptables
```

---

## One Command to Install Common Networking Tools

```bash
sudo apt update
sudo apt install net-tools dnsutils traceroute mtr telnet netcat-openbsd whois nmap wget curl procps iptables
```

---

# Important Ports for DevOps

| Port | Service | Use |
|---|---|---|
| `22` | SSH | Remote server login |
| `53` | DNS | Domain name resolution |
| `80` | HTTP | Web traffic |
| `443` | HTTPS | Secure web traffic |
| `3306` | MySQL | MySQL database |
| `5432` | PostgreSQL | PostgreSQL database |
| `6379` | Redis | Redis cache |
| `8080` | Application Port | Common web application port |

---

# Old Commands and Modern Replacements

| Old Command | Modern Replacement | Purpose |
|---|---|---|
| `ifconfig` | `ip addr` | Check IP address and network interfaces |
| `netstat` | `ss` | Check ports, sockets, and connections |
| `route` | `ip route` | Check routing table |
| `arp` | `ip neigh` | Check neighbour/ARP table |
| `nslookup` | `dig` | DNS troubleshooting |
| `telnet` | `nc` | Port testing |

---

# Recommended Practice Commands

## Check server identity

```bash
hostname
hostname -I
hostnamectl
cat /etc/hosts
```

---

## Check IP address and network interfaces

```bash
ip addr
ip link
ifconfig
```

---

## Check routes

```bash
ip route
route -n
```

---

## Check internet connectivity

```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
ping trainwithshubham.com
```

---

## Check DNS resolution

```bash
nslookup google.com
nslookup trainwithshubham.com
dig google.com
dig trainwithshubham.com
dig google.com +short
```

---

## Check active ports and services

```bash
ss -tulnp
netstat -tulnp
```

---

## Test ports

```bash
telnet google.com 80
telnet google.com 443
nc -zv google.com 80
nc -zv google.com 443
```

---

## Trace packet path

```bash
traceroute google.com
traceroute youtube.com
tracepath google.com
tracepath facebook.com
mtr google.com
mtr trainwithshubham.com
```

---

## Check domain information

```bash
whois google.com
whois facebook.com
whois trainwithshubham.com
```

---

## Scan ports and hosts

```bash
nmap localhost
nmap 127.0.0.1
nmap -p 22,80,443 localhost
nmap -sV localhost
```

---

## Download files

```bash
wget https://example.com/file.zip
wget -O newfile.zip https://example.com/file.zip
curl -O https://example.com/file.zip
curl -I https://google.com
```

---

## Monitor live output

```bash
watch date
watch df -h
watch free -m
watch ss -tuln
watch -n 5 top
```

---

## Check firewall rules

```bash
sudo iptables -L
sudo iptables -L -n -v
```

---

# Beginner DevOps Network Troubleshooting Flow

When a network issue happens, follow this order:

```bash
hostname
ip addr
ip route
ping -c 4 8.8.8.8
ping -c 4 google.com
nslookup google.com
dig google.com
ss -tulnp
telnet google.com 80
telnet google.com 443
traceroute google.com
tracepath google.com
mtr google.com
```

---

# Simple Memory Trick

```text
IP → Ping → DNS → Port → Path
```

| Step | Command | Question |
|---|---|---|
| IP | `ip addr` | Does the server have an IP address? |
| Ping | `ping 8.8.8.8` | Is internet connectivity working? |
| DNS | `dig google.com` | Is DNS resolving correctly? |
| Port | `ss -tulnp` / `telnet` / `nc` | Is the service port reachable? |
| Path | `traceroute` / `tracepath` / `mtr` | Where is the network issue happening? |

---

# Notes

Linux networking commands are important for DevOps, cloud servers, Docker, Kubernetes, CI/CD troubleshooting, monitoring, production support, and server administration.
