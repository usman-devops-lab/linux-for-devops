# Phase 4: Linux Networking Commands for DevOps

This phase documents my learning of **Linux Networking Commands** for DevOps.

In this phase, I studied and practiced important Linux networking commands that are used to troubleshoot network issues, check server connectivity, inspect IP addresses, verify DNS resolution, check open ports, trace packet routes, scan networks, download files, monitor command output, and manage firewall rules.

Networking is a core skill for DevOps because servers, cloud instances, containers, APIs, websites, databases, CI/CD pipelines, and monitoring tools all depend on network communication.

---

## Learning Source

This phase is based on the course:

**Linux For DevOps In One Shot | Complete Beginners to Advanced Linux Hindi**

I am learning Linux step by step and documenting important concepts, commands, notes, errors, fixes, and hands-on practice that are useful for DevOps, cloud infrastructure, automation, and server management.

---

## Phase 4 Focus

The main focus of this phase is Linux networking.

I covered commands related to:

- Connectivity checking
- IP address and network interface checking
- Routing table checking
- DNS troubleshooting
- Port and service checking
- Local network inspection
- Domain information lookup
- Network scanning
- File downloading
- HTTP and API testing
- Live monitoring
- Firewall rule management
- Beginner DevOps network troubleshooting flow

---

## Why Linux Networking Is Important for DevOps

Linux networking is very important for DevOps engineers because most production systems run on Linux servers and communicate over networks.

A DevOps engineer should know how to check:

- Whether a server is reachable
- Whether internet is working
- Whether DNS is resolving correctly
- Which IP address is assigned to a server
- Which network interface is active
- Which route or gateway is being used
- Which ports are open
- Which services are listening
- Whether firewall rules are allowing or blocking traffic
- Whether a website or API is responding
- Whether packets are being dropped
- Where network delay is happening

These skills are useful in cloud servers, Linux administration, Docker, Kubernetes, CI/CD troubleshooting, monitoring, and production support.

---

# Commands Covered

## 1. Connectivity Checking Commands

| Command | Purpose |
|---|---|
| `ping` | Checks whether a host, server, website, or IP address is reachable |
| `traceroute` | Shows the network path packets take to reach a destination |
| `tracepath` | Simple route checking command |
| `mtr` | Combines ping and traceroute for live packet loss and latency checking |

---

## 2. Network Interface and IP Commands

| Command | Purpose |
|---|---|
| `ip` | Modern command to check IP addresses, routes, links, and neighbour entries |
| `ifconfig` | Old command to check network interface information |
| `hostname` | Shows or changes the system hostname |
| `iwconfig` | Shows wireless network interface information |

---

## 3. Ports and Services Commands

| Command | Purpose |
|---|---|
| `ss` | Shows socket statistics, listening ports, and active connections |
| `netstat` | Old command to show network connections and ports |
| `nc` / `netcat` | Tests TCP or UDP port connectivity |
| `telnet` | Old command mostly used today for simple port testing |

---

## 4. DNS Troubleshooting Commands

| Command | Purpose |
|---|---|
| `nslookup` | Basic DNS lookup command |
| `dig` | Advanced DNS troubleshooting command |

---

## 5. Local Network Commands

| Command | Purpose |
|---|---|
| `arp` | Shows IP-to-MAC address mapping |
| `ifplugstatus` | Checks whether a network cable/link is connected |

---

## 6. Domain Information Command

| Command | Purpose |
|---|---|
| `whois` | Shows domain registration and ownership information |

---

## 7. Routing and Scanning Commands

| Command | Purpose |
|---|---|
| `route` | Views or manages the system routing table |
| `nmap` | Scans hosts, ports, and services |

---

## 8. File Download and HTTP Commands

| Command | Purpose |
|---|---|
| `wget` | Downloads files from URLs |
| `curl` | Tests APIs, HTTP requests, headers, and URL responses |

---

## 9. Monitoring and Firewall Commands

| Command | Purpose |
|---|---|
| `watch` | Runs a command repeatedly and shows live output |
| `iptables` | Manages Linux firewall rules |

---

# Detailed Notes

## ping

The `ping` command checks whether another server, website, or IP address is reachable.

### Syntax

```bash
ping domain-or-ip
```

### Examples

```bash
ping google.com
```

```bash
ping -c 4 google.com
```

```bash
ping -c 4 8.8.8.8
```

### Useful Options

| Option | Meaning |
|---|---|
| `-c 4` | Sends only 4 packets |
| `-i 2` | Waits 2 seconds between packets |
| `-W 3` | Waits 3 seconds for a reply |

### DevOps Use

`ping` is usually the first command used to check internet or server connectivity.

If this works:

```bash
ping -c 4 8.8.8.8
```

but this fails:

```bash
ping -c 4 google.com
```

then internet may be working, but DNS may have a problem.

---

## traceroute

The `traceroute` command shows the path packets take from your system to a destination.

### Syntax

```bash
traceroute domain-or-ip
```

### Examples

```bash
traceroute google.com
```

```bash
traceroute 8.8.8.8
```

### Install If Missing

```bash
sudo apt update
sudo apt install traceroute
```

### DevOps Use

`traceroute` is used when a website or server is slow or unreachable. It helps find where the network problem is happening.

---

## tracepath

The `tracepath` command is similar to `traceroute`, but simpler.

### Syntax

```bash
tracepath domain-or-ip
```

### Example

```bash
tracepath google.com
```

### DevOps Use

`tracepath` is useful for simple route checking and can also help detect MTU issues.

---

## traceroute vs tracepath

| Command | Use | Beginner Note |
|---|---|---|
| `traceroute` | Detailed route checking | More options |
| `tracepath` | Simple route checking | Easier and usually no root permission needed |

---

## mtr

The `mtr` command combines `ping` and `traceroute`.

It continuously checks each network hop and shows packet loss and latency.

### Syntax

```bash
mtr domain-or-ip
```

### Examples

```bash
mtr google.com
```

```bash
mtr -c 10 google.com
```

```bash
mtr -r google.com
```

### Useful Options

| Option | Meaning |
|---|---|
| `-c 10` | Sends only 10 packets |
| `-r` | Runs in report mode |

### Install If Missing

```bash
sudo apt update
sudo apt install mtr
```

### DevOps Use

`mtr` is useful for checking:

- Network delay
- Packet loss
- Unstable connections
- Slow network paths

---

## ip

The `ip` command is the modern Linux command used to check and manage network interfaces, IP addresses, routes, and neighbour entries.

### Check IP Address

```bash
ip addr
```

Short form:

```bash
ip a
```

### Check Network Interfaces

```bash
ip link
```

### Check Routing Table

```bash
ip route
```

### Check ARP/Neighbour Table

```bash
ip neigh
```

### DevOps Use

The `ip` command is one of the most important networking commands in Linux.

It is used to check:

- IP address
- Network interface status
- Routing table
- Default gateway
- ARP/neighbour entries

---

## ifconfig

The `ifconfig` command shows network interface information.

### Syntax

```bash
ifconfig
```

### Check Specific Interface

```bash
ifconfig eth0
```

### Install If Missing

```bash
sudo apt update
sudo apt install net-tools
```

### Modern Replacement

```bash
ip addr
```

### DevOps Note

`ifconfig` is an old command. In modern Linux and professional DevOps work, the `ip` command is used more often.

---

## hostname

The `hostname` command shows or changes the system hostname.

### Show Hostname

```bash
hostname
```

### Show System IP Address

```bash
hostname -I
```

### Change Hostname

```bash
sudo hostnamectl set-hostname web-server-01
```

### DevOps Use

`hostname` is useful for identifying servers in:

- Logs
- Monitoring systems
- Cloud servers
- Kubernetes nodes
- Server clusters

---

## iwconfig

The `iwconfig` command shows wireless network interface information.

### Syntax

```bash
iwconfig
```

### Check Wireless Interface

```bash
iwconfig wlan0
```

### DevOps Use

`iwconfig` is useful for:

- Laptops
- Raspberry Pi
- Wireless servers
- Edge devices
- Wi-Fi troubleshooting

### Note

On many cloud servers, wireless interfaces are not available, so `iwconfig` may not show useful output.

---

## ss

The `ss` command shows socket information, listening ports, and active network connections.

### Show Listening TCP and UDP Ports

```bash
ss -tuln
```

### Show Process Name and PID

```bash
sudo ss -tulnp
```

### Useful Options

| Option | Meaning |
|---|---|
| `-t` | TCP connections |
| `-u` | UDP connections |
| `-l` | Listening ports |
| `-n` | Shows numeric ports |
| `-p` | Shows process name and PID |

### DevOps Use

DevOps engineers use `ss` to check whether services are running on correct ports.

Examples:

| Port | Service |
|---|---|
| `22` | SSH |
| `80` | HTTP |
| `443` | HTTPS |
| `3306` | MySQL |
| `5432` | PostgreSQL |
| `6379` | Redis |

---

## netstat

The `netstat` command shows network connections, listening ports, routing tables, and network statistics.

### Show Listening Ports

```bash
netstat -tulnp
```

### Show Routing Table

```bash
netstat -rn
```

### Install If Missing

```bash
sudo apt update
sudo apt install net-tools
```

### Modern Replacement

```bash
ss -tulnp
```

### DevOps Note

`netstat` is an older command. In modern Linux systems, `ss` is preferred.

---

## nc / netcat

The `nc` command is also called Netcat.

It is used to test TCP or UDP connections and check whether a port is open.

### Syntax

```bash
nc -zv host port
```

### Example

```bash
nc -zv google.com 443
```

This checks whether port `443` is open on `google.com`.

### Useful Options

| Option | Meaning |
|---|---|
| `-z` | Scan only, do not send data |
| `-v` | Verbose output |

### DevOps Use

DevOps engineers use `nc` to test:

- Service connectivity
- Firewall rules
- Open ports
- TCP connection issues

---

## telnet

The `telnet` command is an old command used to connect to remote systems.

Today, it is mostly used for simple port testing.

### Syntax

```bash
telnet host port
```

### Example

```bash
telnet google.com 80
```

### DevOps Note

Do not use Telnet for secure remote login because it is not encrypted.

Use SSH for login:

```bash
ssh user@server-ip
```

For port testing, `nc` is usually better:

```bash
nc -zv google.com 80
```

---

## nslookup

The `nslookup` command checks DNS records of a domain.

### Syntax

```bash
nslookup domain
```

### Example

```bash
nslookup google.com
```

### Install If Missing

```bash
sudo apt update
sudo apt install dnsutils
```

### DevOps Use

`nslookup` is used to check whether DNS is resolving correctly.

---

## dig

The `dig` command is an advanced DNS lookup command.

### Check Default DNS Record

```bash
dig google.com
```

### Short Output

```bash
dig google.com +short
```

### Check A Record

```bash
dig google.com A
```

### Check MX Record

```bash
dig google.com MX
```

### Check NS Record

```bash
dig google.com NS
```

### Reverse DNS Lookup

```bash
dig -x 8.8.8.8
```

### DevOps Use

`dig` is used for serious DNS troubleshooting.

It helps check:

- A records
- MX records
- NS records
- Reverse DNS
- DNS response details

---

## nslookup vs dig

| Command | Use | Beginner Note |
|---|---|---|
| `nslookup` | Basic DNS checking | Simple |
| `dig` | Detailed DNS checking | More professional |

---

## arp

ARP means **Address Resolution Protocol**.

It maps IP addresses to MAC addresses in the local network.

### Show ARP Table

```bash
arp -a
```

### Install If Missing

```bash
sudo apt update
sudo apt install net-tools
```

### Modern Replacement

```bash
ip neigh
```

### DevOps Use

`arp` is used when troubleshooting local network issues.

---

## ifplugstatus

The `ifplugstatus` command checks whether a network cable is plugged in.

### Syntax

```bash
ifplugstatus
```

### Check Specific Interface

```bash
ifplugstatus eth0
```

### Example Output

```text
eth0: link beat detected
```

This means the cable/link is connected.

```text
eth0: unplugged
```

This means the cable/link is disconnected.

### Install If Missing

```bash
sudo apt update
sudo apt install ifplugd
```

### DevOps Use

`ifplugstatus` is useful for checking physical Ethernet connection.

---

## whois

The `whois` command shows domain registration information.

### Syntax

```bash
whois domain
```

### Example

```bash
whois example.com
```

### Install If Missing

```bash
sudo apt update
sudo apt install whois
```

### DevOps Use

`whois` is used to check:

- Domain ownership
- Registrar
- Expiry date
- Name servers
- Registration details

---

## route

The `route` command is used to view or manage the system routing table.

### Show Routing Table

```bash
route
```

### Show Numeric Output

```bash
route -n
```

### Add Default Gateway

```bash
sudo route add default gw 192.168.1.1
```

### Modern Replacement

```bash
ip route
```

### DevOps Use

`route` is used to check:

- Default gateway
- Routing issues
- Network path problems

---

## nmap

The `nmap` command is used for network scanning.

It checks open ports, services, and live hosts.

### Install nmap

```bash
sudo apt update
sudo apt install nmap
```

### Scan One Host

```bash
nmap 192.168.1.1
```

### Scan Localhost

```bash
nmap localhost
```

### Detect Service Versions

```bash
nmap -sV 192.168.1.1
```

### Scan Specific Ports

```bash
nmap -p 22,80,443 192.168.1.1
```

### Find Live Devices in Network

```bash
nmap -sn 192.168.1.0/24
```

### DevOps Use

`nmap` is used to check whether server ports are open.

Common ports:

| Port | Service |
|---|---|
| `22` | SSH |
| `80` | HTTP |
| `443` | HTTPS |

---

## wget

The `wget` command is used to download files from the internet.

### Syntax

```bash
wget URL
```

### Download File

```bash
wget https://example.com/file.zip
```

### Save With New Name

```bash
wget -O newfile.zip https://example.com/file.zip
```

### Resume Incomplete Download

```bash
wget -c https://example.com/file.zip
```

### DevOps Use

`wget` is used to download:

- Packages
- Scripts
- Backups
- Installation files
- Server files

---

## curl

The `curl` command is used to transfer data from URLs.

It is very useful for testing APIs and HTTP requests.

### Show Page or API Response

```bash
curl https://example.com
```

### Show Only Headers

```bash
curl -I https://example.com
```

### Send GET Request

```bash
curl -X GET https://api.example.com
```

### Send POST Request

```bash
curl -X POST -d "name=ali" https://example.com/api
```

### Download File

```bash
curl -O https://example.com/file.zip
```

### DevOps Use

`curl` is used for:

- API testing
- HTTP request testing
- Website health checks
- Header checking
- Automation scripts

---

## curl vs wget

Both `curl` and `wget` are used to transfer data from URLs, but they are used differently.

| Command | Main Use |
|---|---|
| `curl` | Testing APIs, HTTP requests, and headers |
| `wget` | Downloading files |

### curl Examples

```bash
curl https://example.com
```

```bash
curl -I https://example.com
```

```bash
curl -X GET https://api.example.com
```

```bash
curl -X POST -d "name=ali" https://example.com/api
```

### wget Examples

```bash
wget https://example.com/file.zip
```

```bash
wget -c https://example.com/file.zip
```

### Beginner Memory

```text
curl = API and HTTP testing
wget = File downloading
```

---

## watch

The `watch` command runs another command repeatedly and shows live output.

### Syntax

```bash
watch command
```

### Examples

```bash
watch date
```

Monitor disk space:

```bash
watch df -h
```

Monitor memory:

```bash
watch free -m
```

Run command every 1 second:

```bash
watch -n 1 uptime
```

Monitor open ports:

```bash
watch ss -tuln
```

### DevOps Use

`watch` is used to monitor server resources live.

It is useful for checking:

- Disk usage
- Memory usage
- Uptime
- Open ports
- Running command output

---

## iptables

The `iptables` command is used to manage Linux firewall rules.

### List Firewall Rules

```bash
sudo iptables -L
```

### List Rules With Numeric Output

```bash
sudo iptables -L -n -v
```

### Allow SSH Port 22

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

### Allow HTTP Port 80

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

### Allow HTTPS Port 443

```bash
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

### Block Port 8080

```bash
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
```

### DevOps Use

`iptables` is used to allow or block server traffic using firewall rules.

### Important Warning

Be careful while using `iptables` on a remote server.

Wrong firewall rules can block SSH access and disconnect you from the server.

Before changing firewall rules on a remote server, make sure SSH is allowed:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

---

# Old Commands and Modern Replacements

| Old Command | Modern Command | Purpose |
|---|---|---|
| `ifconfig` | `ip addr` | Check IP address and interfaces |
| `route` | `ip route` | Check routing table |
| `arp` | `ip neigh` | Check ARP/neighbour table |
| `netstat` | `ss` | Check ports and sockets |
| `nslookup` | `dig` | DNS troubleshooting |
| `telnet` | `nc` | Port testing |

---

# Important Ports for DevOps

| Port | Service |
|---|---|
| `22` | SSH |
| `53` | DNS |
| `80` | HTTP |
| `443` | HTTPS |
| `3306` | MySQL |
| `5432` | PostgreSQL |
| `6379` | Redis |
| `8080` | Common application port |

---

# Beginner DevOps Network Troubleshooting Flow

When a network is not working, I can follow this order:

## Step 1: Check Server Name

```bash
hostname
```

Purpose:

```text
Check which server I am working on.
```

---

## Step 2: Check IP Address

```bash
ip addr
```

Purpose:

```text
Check whether the server has an IP address.
```

---

## Step 3: Check Route and Default Gateway

```bash
ip route
```

Purpose:

```text
Check whether the server has a route to send traffic outside.
```

---

## Step 4: Check Internet by IP

```bash
ping -c 4 8.8.8.8
```

Purpose:

```text
Check whether internet is working without DNS.
```

---

## Step 5: Check Internet by Domain

```bash
ping -c 4 google.com
```

Purpose:

```text
Check whether internet and DNS are both working.
```

---

## Step 6: Check DNS Details

```bash
dig google.com
```

Purpose:

```text
Check DNS resolution details.
```

---

## Step 7: Check Listening Services

```bash
ss -tulnp
```

Purpose:

```text
Check which ports and services are running.
```

---

## Step 8: Test Specific Port

```bash
nc -zv server.com 443
```

Purpose:

```text
Check whether a specific TCP port is open.
```

---

## Step 9: Check Network Path

```bash
traceroute google.com
```

Purpose:

```text
Check the route packets take to reach destination.
```

---

## Step 10: Check Packet Loss and Latency

```bash
mtr google.com
```

Purpose:

```text
Check network delay, packet loss, and unstable connections.
```

---

# Simple Memory Trick

```text
IP → Ping → DNS → Port → Path
```

| Step | Command Example | Question |
|---|---|---|
| IP | `ip addr` | Do I have an IP? |
| Ping | `ping 8.8.8.8` | Can I reach the internet? |
| DNS | `dig google.com` | Is DNS working? |
| Port | `ss -tulnp` / `nc -zv` | Is the port open? |
| Path | `traceroute` / `mtr` | Where is the network problem? |

---

# Practice Tasks

## Task 1: Check Basic Network Information

```bash
hostname
ip addr
ip route
```

## Task 2: Check Connectivity

```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
```

## Task 3: Check DNS

```bash
nslookup google.com
dig google.com
dig google.com +short
```

## Task 4: Check Ports and Services

```bash
ss -tuln
sudo ss -tulnp
netstat -tulnp
```

## Task 5: Test Port Connectivity

```bash
nc -zv google.com 443
telnet google.com 80
```

## Task 6: Check Network Path

```bash
traceroute google.com
tracepath google.com
mtr google.com
```

## Task 7: Check Local Network

```bash
arp -a
ip neigh
ifplugstatus eth0
```

## Task 8: Scan Network

```bash
nmap localhost
nmap -p 22,80,443 localhost
```

## Task 9: Download Files

```bash
wget https://example.com/file.zip
curl -O https://example.com/file.zip
```

## Task 10: Monitor Live Output

```bash
watch date
watch df -h
watch free -m
watch ss -tuln
```

## Task 11: Check Firewall Rules

```bash
sudo iptables -L
sudo iptables -L -n -v
```

---

# Common Errors and Fixes

## ifconfig, netstat, route, or arp command not found

```bash
sudo apt update
sudo apt install net-tools
```

Modern alternatives:

```bash
ip addr
ip route
ip neigh
ss -tulnp
```

---

## traceroute command not found

```bash
sudo apt update
sudo apt install traceroute
```

---

## tracepath command not found

```bash
sudo apt update
sudo apt install iputils-tracepath
```

---

## mtr command not found

```bash
sudo apt update
sudo apt install mtr
```

---

## nslookup or dig command not found

```bash
sudo apt update
sudo apt install dnsutils
```

---

## nc command not found

```bash
sudo apt update
sudo apt install netcat-openbsd
```

---

## telnet command not found

```bash
sudo apt update
sudo apt install telnet
```

---

## whois command not found

```bash
sudo apt update
sudo apt install whois
```

---

## nmap command not found

```bash
sudo apt update
sudo apt install nmap
```

---

## wget command not found

```bash
sudo apt update
sudo apt install wget
```

---

## curl command not found

```bash
sudo apt update
sudo apt install curl
```

---

## watch command not found

```bash
sudo apt update
sudo apt install procps
```

---

## iptables command not found

```bash
sudo apt update
sudo apt install iptables
```

---

## ifplugstatus command not found

```bash
sudo apt update
sudo apt install ifplugd
```

---

## ping works with IP but not with domain

If this works:

```bash
ping -c 4 8.8.8.8
```

but this fails:

```bash
ping -c 4 google.com
```

then DNS may not be working.

Check DNS:

```bash
cat /etc/resolv.conf
nslookup google.com
dig google.com
```

---

## Permission denied while using iptables

Use `sudo`:

```bash
sudo iptables -L
```

---

## nmap says host seems down

Try:

```bash
nmap -Pn target-ip
```

---

## curl SSL certificate problem

Install certificates:

```bash
sudo apt update
sudo apt install ca-certificates
sudo update-ca-certificates
```

Temporary testing only:

```bash
curl -k https://example.com
```

Avoid `-k` in production because it ignores SSL certificate verification.

---

# Useful Package Installation Command

Install common networking tools:

```bash
sudo apt update
sudo apt install net-tools dnsutils traceroute mtr netcat-openbsd telnet whois nmap wget curl procps iptables ifplugd
```

---

# Files in This Phase

| File | Description |
|---|---|
| `README.md` | Complete detailed overview of Phase 4 |
| `commands.md` | Command practice notes |
| `errors-and-fixes.md` | Errors and fixes during practice |
| `resources.md` | Useful resources and practice commands |
| `handwritten-notes/` | My handwritten Day 4 notes |

---

# What I Learned

In this phase, I learned how to:

- Check network connectivity using `ping`
- Trace network paths using `traceroute`, `tracepath`, and `mtr`
- Check IP addresses using `ip` and `ifconfig`
- Check hostname using `hostname`
- Check wireless interfaces using `iwconfig`
- Check open ports using `ss` and `netstat`
- Test port connectivity using `nc` and `telnet`
- Troubleshoot DNS using `nslookup` and `dig`
- Check local ARP table using `arp` and `ip neigh`
- Check network cable status using `ifplugstatus`
- Check domain registration using `whois`
- Check routing table using `route` and `ip route`
- Scan networks and ports using `nmap`
- Download files using `wget`
- Test APIs and HTTP requests using `curl`
- Monitor commands live using `watch`
- Manage firewall rules using `iptables`

---

# Status

Completed
