# ansible-role-dnsmasq
Ansible role for dnsmasq, this role is intended to be used to configure and manage a dnsmasq installation

## Features
### Packages installed
This role install only the `dnsmasq` package

### Firewall 
This role open the port 53 both tpc and udp and the port 67/udp on the allowed networks, see [Allowed networks](#Allowed networks)

## Options
This role hase different options:

* enable/disable dhcp
* manage custom dns entry
* manage custom upstram servers
* manage listen address
* manage allowed networks
* manage dhcp options

### Enable disable option
This option can be managed:
```
dnsmasq_dhcp_enabled: "true"
```
### Manage custom dns entries
When the `dns_enties` is defined:
```
dns_etries:
  - { ip: "192.168.100.2", name : "test.test.net,wp.test.net" }
  - { ip: "192.168.100.3", name : "git.test.net" }
```

This role add a line to the file  `dnsmasq.conf`:
```
    host-record=test.test.net,wp.test.net,192.168.100.2
    host-record=git.test.net,192.168.100.3
```
If this variable is not set, dnsmasq will resolve the query using the defined dns server and the content of `/etc/hosts` file.

### Upstream Servers
The upstream dns servers can be managed using the variable:
```
upstream_dns_servers:
  - 208.67.220.220
  - 208.67.222.222
```

**NB:** /etc/resolv.conf is ignored

### Listen addresses
By default this role configure dnsmasq to listen only on locolhost, adding ip values to:
```
dnsmasq_listen_addr: "192.168.100.3"
```
It will listen on more intefaces.

### Allowed networks
It is possible to manage the Firewall using this congiuration
```
dnsmasq_networks:
  - { ip: "192.168.100.0", netmask: "255.255.255.0" }
```

By default if this conf is not specified, no rules are added.

### DHCP option
Available dhcp options:
```
dnsmasq_domain: "test.net"
dnsmasq_ip_range: "192.168.100.32,192.168.100.250,255.255.255.0,12h"
dnsmasq_ip_gw: "192.168.100.1"
dnsmasq_ip_dns: "192.168.100.2"
```




## References
* [dnsmasq man page](https://dnsmasq.org/docs/dnsmasq-man.html)
