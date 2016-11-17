# PPTP Tunnel VPS and Ubuntu

E.g. AlienVPS.com

## Install PPTP Package

```
apt-get install pptpd
```

## Add <server ip>

File: `/etc/pptpd.conf`  
Example: `localip 192.168.1.100`

## Change the DNS Servers to Google 

File: `/etc/ppp/pptpd-options`  
Add Google DNS servers:

```
ms-dns 8.8.8.8
ms-dns 8.8.4.4
```

## Configure User Data 

File: `/etc/ppp/chap-secrets`

```
username pptpd password <password>
```

## Activate IP Forwarding

File: `/etc/sysctl.conf`  
Uncomment: `net.ipv4.ip_forward=1`

### Edit rc.local

File: `/etc/rc.local`

```
iptables -t nat -F POSTROUTING
iptables -t nat -A POSTROUTING -j SNAT –to-source <local server IP>
exit 0
```