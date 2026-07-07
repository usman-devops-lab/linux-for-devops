# Phase 4 Commands Practice

This file contains the Linux networking commands I practiced in Phase 4.

---

## Connectivity Commands

```bash
ping trainwithshubham.com
ping -c 4 google.com
ping -c 4 8.8.8.8
traceroute youtube.com
tracepath trainwithshubham.com
tracepath facebook.com
mtr trainwithshubham.com
```

---

## Network Interface and Host Commands

```bash
hostname
hostname -I
hostnamectl
cat /etc/hosts
ip
ip addr
ip link
ip route
ifconfig
```

---

## Port and Socket Commands

```bash
netstat
ss -tulnp
telnet trainwithshubham.com 80
telnet trainwithshubham.com 443
```

---

## DNS and Domain Commands

```bash
nslookup trainwithshubham.com
nslookup google.com
dig trainwithshubham.com
whois trainwithshubham.com
whois google.com
whois facebook.com
```

---

## Installation Commands Used

```bash
sudo apt install net-tools
sudo apt install inetutils-traceroute
sudo apt install whois
```

---

## Useful Modern Alternatives

```bash
ip addr      # modern replacement for ifconfig
ss -tulnp    # modern replacement for netstat
ip route     # modern replacement for route
ip neigh     # modern replacement for arp
dig domain   # advanced DNS lookup
```

---

## Beginner DevOps Network Troubleshooting Flow

```bash
hostname
ip addr
ip route
ping -c 4 8.8.8.8
ping -c 4 google.com
nslookup google.com
dig google.com
ss -tulnp
telnet domain.com 80
telnet domain.com 443
traceroute domain.com
tracepath domain.com
mtr domain.com
```
