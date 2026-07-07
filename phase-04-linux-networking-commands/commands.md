# Phase 4 Commands Practice

This file contains the Linux networking commands I practiced in Phase 4.

---

## Connectivity Commands

```bash
ping google.com
ping -c 4 google.com
ping -c 4 8.8.8.8
traceroute google.com
tracepath google.com
mtr google.com
mtr -c 10 google.com
mtr -r google.com
```

---

## Network Interface and IP Commands

```bash
hostname
hostname -I
ip addr
ip a
ip link
ip route
ip neigh
ifconfig
ifconfig eth0
iwconfig
iwconfig wlan0
```

---

## Ports and Services Commands

```bash
ss -tuln
sudo ss -tulnp
netstat -tulnp
netstat -rn
nc -zv google.com 443
telnet google.com 80
```

---

## DNS Commands

```bash
nslookup google.com
dig google.com
dig google.com +short
dig google.com A
dig google.com MX
dig google.com NS
dig -x 8.8.8.8
```

---

## Local Network Commands

```bash
arp -a
ip neigh
ifplugstatus
ifplugstatus eth0
```

---

## Domain Information Command

```bash
whois example.com
```

---

## Routing and Network Scanning Commands

```bash
route
route -n
ip route
nmap localhost
nmap 192.168.1.1
nmap -sV 192.168.1.1
nmap -p 22,80,443 192.168.1.1
nmap -sn 192.168.1.0/24
```

---

## Download and HTTP Testing Commands

```bash
wget https://example.com/file.zip
wget -O newfile.zip https://example.com/file.zip
wget -c https://example.com/file.zip

curl https://example.com
curl -I https://example.com
curl -X GET https://api.example.com
curl -X POST -d "name=ali" https://example.com/api
curl -O https://example.com/file.zip
```

---

## Monitoring Commands

```bash
watch date
watch df -h
watch free -m
watch -n 1 uptime
watch ss -tuln
```

---

## Firewall Commands

```bash
sudo iptables -L
sudo iptables -L -n -v
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
```

---

## Beginner DevOps Troubleshooting Flow

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
```
