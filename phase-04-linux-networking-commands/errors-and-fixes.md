# Phase 4 Errors and Fixes

This file contains common errors and fixes related to Linux networking commands.

---

## ifconfig: command not found

```bash
ifconfig: command not found
```

### Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Modern Alternative

```bash
ip addr
```

---

## netstat: command not found

```bash
netstat: command not found
```

### Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Modern Alternative

```bash
ss -tulnp
```

---

## route: command not found

```bash
route: command not found
```

### Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Modern Alternative

```bash
ip route
```

---

## arp: command not found

```bash
arp: command not found
```

### Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Modern Alternative

```bash
ip neigh
```

---

## traceroute: command not found

```bash
traceroute: command not found
```

### Fix

```bash
sudo apt update
sudo apt install traceroute
```

---

## tracepath: command not found

```bash
tracepath: command not found
```

### Fix

```bash
sudo apt update
sudo apt install iputils-tracepath
```

---

## mtr: command not found

```bash
mtr: command not found
```

### Fix

```bash
sudo apt update
sudo apt install mtr
```

---

## nslookup or dig: command not found

```bash
nslookup: command not found
dig: command not found
```

### Fix

```bash
sudo apt update
sudo apt install dnsutils
```

---

## nc: command not found

```bash
nc: command not found
```

### Fix

```bash
sudo apt update
sudo apt install netcat-openbsd
```

---

## telnet: command not found

```bash
telnet: command not found
```

### Fix

```bash
sudo apt update
sudo apt install telnet
```

---

## whois: command not found

```bash
whois: command not found
```

### Fix

```bash
sudo apt update
sudo apt install whois
```

---

## nmap: command not found

```bash
nmap: command not found
```

### Fix

```bash
sudo apt update
sudo apt install nmap
```

---

## wget: command not found

```bash
wget: command not found
```

### Fix

```bash
sudo apt update
sudo apt install wget
```

---

## curl: command not found

```bash
curl: command not found
```

### Fix

```bash
sudo apt update
sudo apt install curl
```

---

## watch: command not found

```bash
watch: command not found
```

### Fix

```bash
sudo apt update
sudo apt install procps
```

---

## iptables: command not found

```bash
iptables: command not found
```

### Fix

```bash
sudo apt update
sudo apt install iptables
```

---

## ifplugstatus: command not found

```bash
ifplugstatus: command not found
```

### Fix

```bash
sudo apt update
sudo apt install ifplugd
```

---

## ping works with IP but not domain

If this works:

```bash
ping -c 4 8.8.8.8
```

but this fails:

```bash
ping -c 4 google.com
```

then DNS may have a problem.

### Fix

```bash
cat /etc/resolv.conf
nslookup google.com
dig google.com
```

---

## Permission denied while using iptables

### Fix

```bash
sudo iptables -L
```

---

## SSH blocked by firewall

Before changing firewall rules on a remote server, allow SSH:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

Be careful with firewall commands on cloud servers and remote servers.
