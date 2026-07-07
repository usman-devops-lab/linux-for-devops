# Phase 4: Linux Networking Commands for DevOps

This phase documents my learning and hands-on practice of **Linux Networking Commands** for DevOps.

In this phase, I practiced important networking commands on an Ubuntu EC2 server. These commands are useful for checking connectivity, troubleshooting DNS, checking IP addresses, inspecting network interfaces, testing ports, checking running services, tracing packet routes, checking domain information, and understanding real server networking behavior.

---

## Learning Source

This phase is based on:

**Linux For DevOps In One Shot | Complete Beginners to Advanced Linux Hindi**

I am learning Linux step by step and documenting important concepts, commands, notes, errors, fixes, screenshots, and hands-on practice that are useful for DevOps, cloud infrastructure, automation, and server management.

---

## Phase 4 Focus

The focus of this phase is **Linux Networking Commands**.

I practiced commands related to:

- Network connectivity checking
- IP address checking
- Network interface inspection
- DNS troubleshooting
- Port and service testing
- Route and packet path tracing
- Domain information lookup
- Socket and connection checking
- Installing missing networking tools
- Understanding old networking commands and modern replacements

---

## Why Linux Networking Is Important for DevOps

Linux networking is one of the most important skills for DevOps engineers.

Most DevOps work happens on Linux servers, cloud instances, containers, CI/CD runners, APIs, databases, monitoring tools, and production applications. All of these depend on network communication.

A DevOps engineer should know how to check:

- Whether a server is reachable
- Whether internet connectivity is working
- Whether DNS resolution is working
- Which IP address is assigned to a server
- Which network interface is active
- Which ports are open
- Which services are listening
- Whether HTTP or HTTPS ports are reachable
- Where packet delay or packet loss is happening
- Whether a domain is registered and resolving correctly
- Which networking tools are old and which modern commands should be used

---

# Commands Practiced

## 1. Connectivity Commands

| Command | Purpose |
|---|---|
| `ping` | Checks whether a host, website, or IP address is reachable |
| `traceroute` | Shows the route packets take to reach a destination |
| `tracepath` | Shows packet path and MTU information |
| `mtr` | Combines ping and traceroute for live packet loss and latency checking |

---

## 2. Network Interface and IP Commands

| Command | Purpose |
|---|---|
| `ip` | Modern command to check IP addresses, routes, links, and neighbour table |
| `ifconfig` | Old command to check network interface details |
| `hostname` | Shows system hostname |
| `hostname -I` | Shows IP addresses assigned to the host |
| `hostnamectl` | Shows detailed system and hostname information |

---

## 3. Port and Socket Commands

| Command | Purpose |
|---|---|
| `netstat` | Shows active network connections and sockets |
| `ss` | Modern command to check listening ports and socket statistics |
| `telnet` | Tests connection to a specific host and port |

---

## 4. DNS and Domain Commands

| Command | Purpose |
|---|---|
| `nslookup` | Checks DNS resolution of a domain |
| `dig` | Shows detailed DNS query information |
| `whois` | Shows domain registration and ownership information |

---

# Hands-on Practice Summary

## 1. ping Practice

I used `ping` to test connectivity with:

```bash
ping trainwithshubham.com
```

The domain resolved successfully and replied from AWS Global Accelerator IP addresses.

Observed result:

```text
36 packets transmitted
36 received
0% packet loss
```

This means the EC2 server had successful connectivity to the domain.

### DevOps Use

`ping` is usually the first command used to check whether a server, website, or IP address is reachable.

---

## 2. netstat Practice

At first, `netstat` was not installed.

Error:

```bash
Command 'netstat' not found
```

I installed it using:

```bash
sudo apt install net-tools
```

After installation, I ran:

```bash
netstat
```

It showed active internet connections and UNIX domain sockets.

### DevOps Use

`netstat` helps check active network connections, sockets, and network activity on a server.

### Modern Replacement

```bash
ss
```

---

## 3. ifconfig Practice

I used:

```bash
ifconfig
```

The output showed network interfaces such as:

```text
docker0
ens5
lo
```

Important IP addresses observed:

```text
ens5    172.31.45.84
docker0 172.17.0.1
lo      127.0.0.1
```

### DevOps Use

`ifconfig` helps check IP addresses, MAC addresses, packet statistics, and network interface status.

### Modern Replacement

```bash
ip addr
```

---

## 4. traceroute Practice

At first, `traceroute` was not installed.

Error:

```bash
Command 'traceroute' not found
```

I installed it using:

```bash
sudo apt install inetutils-traceroute
```

Then I practiced:

```bash
traceroute youtube.com
```

The output showed packet hops from my EC2 server to YouTube.

### DevOps Use

`traceroute` is used when a website or server is slow or unreachable. It helps identify where the network path is breaking or slowing down.

---

## 5. tracepath Practice

I practiced:

```bash
tracepath trainwithshubham.com
tracepath facebook.com
```

The output showed path information and MTU details such as:

```text
pmtu 9001
pmtu 1500
no reply
Too many hops
```

### DevOps Use

`tracepath` helps check packet path and MTU-related issues.

---

## 6. mtr Practice

I practiced:

```bash
mtr trainwithshubham.com
```

The output showed live route statistics:

- Host
- Packet loss
- Sent packets
- Last ping
- Average ping
- Best ping
- Worst ping
- Standard deviation

Observed result:

```text
0.0% packet loss
```

### DevOps Use

`mtr` is very useful for checking packet loss, latency, unstable routes, and network delay.

---

## 7. nslookup Practice

I practiced:

```bash
nslookup trainwithshubham.com
nslookup google.com
```

The output showed DNS resolution using local DNS resolver:

```text
Server: 127.0.0.53
Address: 127.0.0.53#53
```

For `trainwithshubham.com`, DNS returned IP addresses:

```text
15.197.225.128
3.33.251.168
```

### DevOps Use

`nslookup` is used to check whether a domain is resolving correctly.

---

## 8. telnet Practice

I practiced port testing using:

```bash
telnet trainwithshubham.com 80
telnet trainwithshubham.com 443
```

The output showed:

```text
Connected to trainwithshubham.com
```

This means ports `80` and `443` were reachable.

### DevOps Use

`telnet` can be used for simple port connectivity testing.

### Important Note

Telnet should not be used for secure login because it is not encrypted. For secure remote login, use SSH.

---

## 9. hostname Practice

I practiced:

```bash
hostname
hostname -I
hostnamectl
cat /etc/hosts
```

Observed hostname:

```text
ip-172-31-45-84
```

Observed IP addresses:

```text
172.31.45.84
172.17.0.1
```

`hostnamectl` showed system information such as:

```text
Operating System: Ubuntu 26.04 LTS
Kernel: Linux 7.0.0-1006-aws
Hardware Vendor: Amazon EC2
Hardware Model: t3.micro
```

### DevOps Use

`hostname` and `hostnamectl` help identify servers in logs, monitoring systems, cloud instances, and clusters.

---

## 10. ip Command Practice

I practiced:

```bash
ip
ip addr
```

The output showed:

```text
lo
ens5
docker0
```

Important IP addresses observed:

```text
lo      127.0.0.1
ens5    172.31.45.84/20
docker0 172.17.0.1/16
```

### DevOps Use

`ip` is the modern and preferred Linux networking command.

Useful commands:

```bash
ip addr
ip link
ip route
ip neigh
```

---

## 11. ss Practice

I practiced:

```bash
ss -tulnp
```

The output showed listening TCP and UDP ports.

Important listening ports observed:

```text
127.0.0.53:53
0.0.0.0:22
[::]:22
```

This means:

- DNS resolver was listening on port `53`
- SSH was listening on port `22`

### DevOps Use

`ss` is used to check which services are listening on which ports.

### Modern Replacement For

```bash
netstat
```

---

## 12. dig Practice

I practiced:

```bash
dig trainwithshubham.com
```

The output showed DNS A records:

```text
3.33.251.168
15.197.225.128
```

### DevOps Use

`dig` is used for detailed DNS troubleshooting and is more professional than `nslookup`.

---

## 13. whois Practice

At first, `whois` was not installed.

Error:

```bash
Command 'whois' not found
```

I installed it using:

```bash
sudo apt install whois
```

Then I practiced:

```bash
whois trainwithshubham.com
whois google.com
whois facebook.com
```

The output showed domain registration details such as:

- Domain name
- Registrar
- Creation date
- Expiry date
- Name servers
- Domain status

### DevOps Use

`whois` is useful for checking domain registration, ownership, expiry date, registrar, and name servers.

---

# Old Commands and Modern Replacements

| Old Command | Modern Replacement | Purpose |
|---|---|---|
| `ifconfig` | `ip addr` | Check IP address and interfaces |
| `netstat` | `ss` | Check ports and sockets |
| `route` | `ip route` | Check routing table |
| `arp` | `ip neigh` | Check neighbour/ARP table |
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

When a network issue happens, I can follow this order:

## Step 1: Check hostname

```bash
hostname
```

## Step 2: Check IP address

```bash
ip addr
```

## Step 3: Check route

```bash
ip route
```

## Step 4: Check internet by IP

```bash
ping -c 4 8.8.8.8
```

## Step 5: Check internet by domain

```bash
ping -c 4 google.com
```

## Step 6: Check DNS

```bash
nslookup google.com
dig google.com
```

## Step 7: Check listening ports

```bash
ss -tulnp
```

## Step 8: Test website ports

```bash
telnet domain.com 80
telnet domain.com 443
```

## Step 9: Check route path

```bash
traceroute domain.com
tracepath domain.com
```

## Step 10: Check packet loss and latency

```bash
mtr domain.com
```

---

# Practice Evidence

I have added practical terminal screenshots for this phase inside:

```text
practice-screenshots/
```

These screenshots show my real command practice on an Ubuntu EC2 server.

The practice includes:

- `ping trainwithshubham.com`
- installing `net-tools`
- running `netstat`
- checking interfaces with `ifconfig`
- installing `inetutils-traceroute`
- running `traceroute`
- running `tracepath`
- running `mtr`
- using `nslookup`
- testing ports with `telnet`
- checking hostname and host file
- using `hostname -I`
- checking system details using `hostnamectl`
- checking IP addresses using `ip addr`
- checking sockets using `ss -tulnp`
- checking DNS using `dig`
- installing and using `whois`

---

# Files in This Phase

| File/Folder | Description |
|---|---|
| `README.md` | Complete Phase 4 overview and detailed practice notes |
| `commands.md` | Commands practiced in this phase |
| `errors-and-fixes.md` | Errors faced and fixes applied |
| `resources.md` | Useful resources and practice references |
| `handwritten-notes/` | My handwritten Day 4 notes |
| `practice-screenshots/` | Terminal screenshots of hands-on practice |

---

# What I Learned

In this phase, I learned how to:

- Check connectivity using `ping`
- Install missing networking tools
- Use `netstat` after installing `net-tools`
- Check interfaces using `ifconfig`
- Use `traceroute` to view packet paths
- Use `tracepath` to check route and MTU information
- Use `mtr` for live packet loss and latency analysis
- Use `nslookup` for DNS checking
- Use `telnet` for port testing
- Use `hostname` and `hostnamectl` for server identity
- Use `ip addr` for modern IP checking
- Use `ss` to check listening ports
- Use `dig` for detailed DNS lookup
- Use `whois` for domain information
- Understand old networking commands and their modern replacements

---

# Status

Completed
