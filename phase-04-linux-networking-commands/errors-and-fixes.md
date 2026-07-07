# Phase 4 Errors and Fixes

This file contains common errors and fixes I faced while practicing Linux networking commands in Phase 4.

These errors are related to missing packages, old Linux networking commands, DNS issues, port testing, firewall commands, route tracing, and real terminal practice on an Ubuntu EC2 server.

---

## 1. netstat: command not found

### Error

```bash
Command 'netstat' not found
```

or:

```bash
netstat: command not found
```

### Reason

`netstat` is an older networking command and is part of the `net-tools` package. It may not be installed by default on modern Linux systems.

### Fix Used

```bash
sudo apt install net-tools
```

### Recommended Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Test After Installation

```bash
netstat
```

or:

```bash
netstat -tulnp
```

### Modern Alternative

```bash
ss -tulnp
```

### DevOps Note

`netstat` is old. In modern Linux systems, `ss` is preferred for checking sockets, ports, and active connections.

---

## 2. ifconfig: command not found

### Error

```bash
ifconfig: command not found
```

### Reason

`ifconfig` is also part of the old `net-tools` package.

### Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Test

```bash
ifconfig
```

### Modern Alternative

```bash
ip addr
```

or:

```bash
ip a
```

### DevOps Note

`ifconfig` is useful for learning, but professional DevOps work mostly uses the `ip` command.

---

## 3. route: command not found

### Error

```bash
route: command not found
```

### Reason

`route` is part of the old `net-tools` package.

### Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Test

```bash
route
route -n
```

### Modern Alternative

```bash
ip route
```

### DevOps Note

Use `ip route` to check the routing table and default gateway on modern Linux systems.

---

## 4. arp: command not found

### Error

```bash
arp: command not found
```

### Reason

`arp` is part of the old `net-tools` package.

### Fix

```bash
sudo apt update
sudo apt install net-tools
```

### Test

```bash
arp -a
```

### Modern Alternative

```bash
ip neigh
```

### DevOps Note

`arp` shows IP-to-MAC address mapping. In modern Linux, `ip neigh` is preferred.

---

## 5. traceroute: command not found

### Error

```bash
Command 'traceroute' not found
```

or:

```bash
traceroute: command not found
```

### Reason

`traceroute` was not installed by default on the server.

### Fix Used

```bash
sudo apt install inetutils-traceroute
```

### Other Possible Fix

```bash
sudo apt update
sudo apt install traceroute
```

### Test After Installation

```bash
traceroute youtube.com
```

or:

```bash
traceroute google.com
```

### DevOps Note

`traceroute` helps check the path packets take to reach a destination. It is useful when a website or server is slow or unreachable.

---

## 6. tracepath: command not found

### Error

```bash
tracepath: command not found
```

### Fix

```bash
sudo apt update
sudo apt install iputils-tracepath
```

### Test

```bash
tracepath google.com
```

### DevOps Note

`tracepath` is similar to `traceroute`, but simpler. It can also show MTU information.

---

## 7. tracepath shows no reply

### Example Output

```text
no reply
Too many hops
```

### Reason

Some routers, firewalls, or cloud networks do not respond to tracepath packets.

### Important Note

This does not always mean the website is down. It may only mean some intermediate routers are not replying.

### Check Again With

```bash
ping domain.com
traceroute domain.com
mtr domain.com
```

### DevOps Note

Always compare multiple tools before deciding the network is down.

---

## 8. ping works but tracepath shows no reply

### Example Situation

`ping` works:

```bash
ping domain.com
```

but `tracepath` shows:

```text
no reply
```

### Reason

Different networking tools use different packet types. A server may reply to ping, but some routers may ignore tracepath packets.

### Fix / Verification

Use multiple checks:

```bash
ping domain.com
traceroute domain.com
tracepath domain.com
mtr domain.com
```

### DevOps Note

Do not depend on only one command for network troubleshooting.

---

## 9. mtr: command not found

### Error

```bash
mtr: command not found
```

### Fix

```bash
sudo apt update
sudo apt install mtr
```

### Test

```bash
mtr google.com
```

or:

```bash
mtr trainwithshubham.com
```

### DevOps Note

`mtr` combines `ping` and `traceroute`. It is useful for checking packet loss, latency, and unstable network paths.

---

## 10. nslookup: command not found

### Error

```bash
nslookup: command not found
```

### Reason

`nslookup` is usually provided by the `dnsutils` package.

### Fix

```bash
sudo apt update
sudo apt install dnsutils
```

### Test

```bash
nslookup google.com
```

### DevOps Note

`nslookup` is used for basic DNS troubleshooting.

---

## 11. dig: command not found

### Error

```bash
dig: command not found
```

### Reason

`dig` is also provided by the `dnsutils` package.

### Fix

```bash
sudo apt update
sudo apt install dnsutils
```

### Test

```bash
dig google.com
```

or:

```bash
dig google.com +short
```

### DevOps Note

`dig` is more detailed and professional than `nslookup` for DNS troubleshooting.

---

## 12. ping works with IP but not domain

### Example

This works:

```bash
ping -c 4 8.8.8.8
```

but this fails:

```bash
ping -c 4 google.com
```

### Reason

The internet connection may be working, but DNS resolution may have a problem.

### Fix / Checks

Check DNS resolver file:

```bash
cat /etc/resolv.conf
```

Check DNS using `nslookup`:

```bash
nslookup google.com
```

Check DNS using `dig`:

```bash
dig google.com
```

### DevOps Note

If IP ping works but domain ping fails, always suspect DNS first.

---

## 13. telnet: command not found

### Error

```bash
telnet: command not found
```

### Fix

```bash
sudo apt update
sudo apt install telnet
```

### Test

```bash
telnet google.com 80
```

or:

```bash
telnet domain.com 443
```

### DevOps Note

Telnet is old and not secure for login, but it can still be used for simple port testing.

---

## 14. Telnet connection closed by foreign host

### Output

```text
Connected to trainwithshubham.com.
Connection closed by foreign host.
```

### Meaning

The TCP connection was successful, but the remote server closed the connection.

### Is This an Error?

Not always.

For port testing, this still proves the port is reachable.

### DevOps Note

If telnet shows `Connected`, the port is open/reachable. The remote server may close the session because no valid protocol request was sent.

---

## 15. nc command used without port

### Error

```bash
nc: missing port number
```

### Reason

`nc` needs a destination host and port.

Wrong:

```bash
nc trainwithshubham.com
```

Correct:

```bash
nc trainwithshubham.com 80
```

Better for port scanning:

```bash
nc -zv trainwithshubham.com 80
```

### DevOps Note

Use `nc -zv host port` to test whether a port is open.

---

## 16. nc: command not found

### Error

```bash
nc: command not found
```

### Fix

```bash
sudo apt update
sudo apt install netcat-openbsd
```

### Test

```bash
nc -zv google.com 443
```

### DevOps Note

`nc` is useful for checking TCP/UDP port connectivity and firewall rules.

---

## 17. nc temporary failure in name resolution

### Error

```bash
nc: getaddrinfo for host "trainwithshubham" port 80: Temporary failure in name resolution
```

### Reason

The hostname may be wrong or incomplete.

Example wrong hostname:

```bash
trainwithshubham
```

Correct domain:

```bash
trainwithshubham.com
```

### Fix

Use the full domain name:

```bash
nc -zv trainwithshubham.com 80
```

Check DNS:

```bash
nslookup trainwithshubham.com
dig trainwithshubham.com
```

### DevOps Note

Always confirm the correct domain name before testing ports.

---

## 18. whois: command not found

### Error

```bash
Command 'whois' not found
```

or:

```bash
whois: command not found
```

### Reason

The `whois` package was not installed.

### Fix Used

```bash
sudo apt install whois
```

### Recommended Fix

```bash
sudo apt update
sudo apt install whois
```

### Test

```bash
whois trainwithshubham.com
whois google.com
whois facebook.com
```

### DevOps Note

`whois` is useful for checking domain ownership, registrar, expiry date, name servers, and domain status.

---

## 19. nmap: command not found

### Error

```bash
nmap: command not found
```

### Fix

```bash
sudo apt update
sudo apt install nmap
```

### Test

```bash
nmap localhost
```

or:

```bash
nmap -p 22,80,443 localhost
```

### DevOps Note

`nmap` is used to scan hosts, ports, and services.

---

## 20. nmap shows host seems down

### Example

```text
Host seems down
```

### Possible Reasons

- Host is offline
- Firewall blocks ping
- Wrong IP address
- Network unreachable
- ICMP blocked

### Try

```bash
nmap -Pn target-ip
```

### DevOps Note

`-Pn` tells nmap to treat the host as online and continue scanning.

---

## 21. wget: command not found

### Error

```bash
wget: command not found
```

### Fix

```bash
sudo apt update
sudo apt install wget
```

### Test

```bash
wget https://example.com/file.zip
```

### DevOps Note

`wget` is useful for downloading files, scripts, packages, and backups on servers.

---

## 22. curl: command not found

### Error

```bash
curl: command not found
```

### Fix

```bash
sudo apt update
sudo apt install curl
```

### Test

```bash
curl -I https://google.com
```

### DevOps Note

`curl` is useful for API testing, HTTP testing, headers, and automation.

---

## 23. curl SSL certificate problem

### Error

```bash
SSL certificate problem
```

### Fix

```bash
sudo apt update
sudo apt install ca-certificates
sudo update-ca-certificates
```

### Temporary Testing Only

```bash
curl -k https://example.com
```

### Warning

Avoid `-k` in production because it ignores SSL certificate verification.

---

## 24. jq parse error after curl

### Error

```bash
jq: parse error: Invalid numeric literal
```

### Reason

The output received by `jq` may not be valid JSON.

Possible causes:

- API returned HTML instead of JSON
- Wrong URL
- API error page
- Redirect response
- Incomplete output
- Command syntax issue

### Check Raw Output First

```bash
curl -X GET https://dummy.restapiexample.com/api/v1/employees
```

### Then Pipe to jq

```bash
curl -s https://dummy.restapiexample.com/api/v1/employees | jq
```

### Install jq If Needed

```bash
sudo apt install jq
```

### DevOps Note

Before piping API output to `jq`, always confirm that the response is valid JSON.

---

## 25. watch: command not found

### Error

```bash
watch: command not found
```

### Fix

```bash
sudo apt update
sudo apt install procps
```

### Test

```bash
watch date
```

### DevOps Note

`watch` is used to run a command repeatedly and monitor live output.

---

## 26. watch command without target command

### Output

```bash
Usage:
 watch [options] command
```

### Reason

`watch` needs another command after it.

Wrong:

```bash
watch
```

Correct:

```bash
watch date
```

```bash
watch df -h
```

```bash
watch free -m
```

```bash
watch ss -tuln
```

### DevOps Note

Use `watch` when you want to repeatedly monitor a command.

---

## 27. top failed with watch because command was typed incorrectly

### Error

```text
top: failed tty get
```

### Reason

The command was not used correctly with `watch`.

Example wrong command:

```bash
watch | top
```

### Correct Usage

```bash
watch top
```

or better:

```bash
watch -n 5 top
```

### DevOps Note

Do not pipe `watch` into another command. Use the command after `watch`.

---

## 28. iptables command mistake

### Error

```bash
iptables v1.8.11 (nf_tables): no command specified
Try `iptables -h' or 'iptables --help' for more information.
```

### Reason

`iptables` needs an action or option.

Wrong:

```bash
iptables
```

Correct:

```bash
sudo iptables -L
```

### DevOps Note

Use `iptables -L` to list firewall rules.

---

## 29. aptables: command not found

### Error

```bash
sudo: aptables: command not found
```

### Reason

The command was typed incorrectly.

Wrong:

```bash
sudo aptables -L
```

Correct:

```bash
sudo iptables -L
```

### DevOps Note

Be careful with spelling in Linux commands.

---

## 30. iptables: command not found

### Error

```bash
iptables: command not found
```

### Fix

```bash
sudo apt update
sudo apt install iptables
```

### Test

```bash
sudo iptables -L
```

### DevOps Note

`iptables` is used to manage Linux firewall rules. Be careful when using it on remote servers.

---

## 31. Permission denied while using iptables

### Error

```bash
Permission denied
```

### Reason

Firewall commands require root privileges.

### Fix

```bash
sudo iptables -L
```

### DevOps Note

Most firewall commands need `sudo`.

---

## 32. SSH blocked by firewall

### Problem

Wrong firewall rules can block SSH access on a remote server.

### Safe Rule Before Firewall Changes

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

### DevOps Note

Be careful with firewall commands on cloud servers and remote servers. Wrong rules can disconnect your SSH session.

---

## 33. ifplugstatus: command not found

### Error

```bash
ifplugstatus: command not found
```

### Reason

`ifplugstatus` was not installed.

### Tried Fix

```bash
sudo apt install ifplugstatus
```

But the package was not found.

### Tried Another Package

```bash
sudo apt install ifplugd
```

On this system, this package was also not available.

### Alternative Checks

Check interface status using:

```bash
ip link
```

Check operational state:

```bash
cat /sys/class/net/ens5/operstate
```

Check carrier status:

```bash
cat /sys/class/net/ens5/carrier
```

Optional tool:

```bash
sudo apt install ethtool
sudo ethtool ens5
```

### DevOps Note

On cloud servers like EC2, physical cable tools may not be useful because the network is virtual.

---

## 34. Pending kernel upgrade message after package installation

### Message

```text
Pending kernel upgrade!
The currently running kernel version is not the expected kernel version.
Restarting the system to load the new kernel will not be handled automatically.
```

### Meaning

A newer kernel is available, but the server is still running the old kernel.

### Fix

Reboot the server during a safe maintenance time:

```bash
sudo reboot
```

### Important Note

Do not reboot production servers without planning.

---

## 35. Services restart being deferred

### Message

```text
Service restarts being deferred:
systemctl restart networkd-dispatcher.service
systemctl restart systemd-logind.service
systemctl restart unattended-upgrades.service
```

### Meaning

Some services need restart after package installation or system update.

### Fix

Usually safe to leave during practice.

For production servers, restart services during a maintenance window.

### Check Services

```bash
systemctl status networkd-dispatcher.service
systemctl status systemd-logind.service
systemctl status unattended-upgrades.service
```

---

# Summary

In this phase, I learned how to handle missing Linux networking tools, install required packages, and use modern alternatives.

Important packages used:

```bash
sudo apt install net-tools
sudo apt install inetutils-traceroute
sudo apt install whois
sudo apt install dnsutils
sudo apt install mtr
sudo apt install netcat-openbsd
sudo apt install telnet
sudo apt install nmap
sudo apt install wget
sudo apt install curl
sudo apt install procps
sudo apt install iptables
```

Important old commands and modern replacements:

| Old Command | Modern Replacement | Purpose |
|---|---|---|
| `ifconfig` | `ip addr` | Check IP address and interfaces |
| `netstat` | `ss` | Check ports and sockets |
| `route` | `ip route` | Check routing table |
| `arp` | `ip neigh` | Check neighbour table |
| `nslookup` | `dig` | DNS troubleshooting |
| `telnet` | `nc` | Port testing |

Important lesson:

Always read the error message carefully, install the correct package, and use modern Linux networking commands where possible.
