# Linux Networking Lab

This document describes the network configuration and connectivity tests performed on the Ubuntu Server virtual machine.

## Lab Environment

* Host operating system: Windows 11
* Virtualization platform: VirtualBox
* Guest operating system: Ubuntu Server 24.04 LTS
* VirtualBox network mode: Bridged Adapter
* Network interface: `enp0s3`
* Configuration method: DHCP

## Interface Configuration

The network interfaces were inspected with:

```bash
ip -br address
```

The relevant output was:

```text
lo       UNKNOWN   127.0.0.1/8 ::1/128
enp0s3   UP        <SERVER_IP>/24
```

### Loopback Interface

The `lo` interface is the local loopback interface.

* IPv4 loopback: `127.0.0.1`
* IPv6 loopback: `::1`
* Used by the system to communicate with itself

### Network Interface

The primary network interface is:

```text
enp0s3
```

Its current IPv4 configuration is:

```text
IP address: <SERVER_IP>
Prefix: /24
Subnet mask: 255.255.255.0
Network: 192.168.1.0/24
Broadcast: <BROADCAST_ADDRESS>
```

The interface status is `UP`, meaning that it is active.

## Routing Table

The IPv4 routing table was inspected with:

```bash
ip route
```

Relevant routes:

```text
default via <DEFAULT_GATEWAY> dev enp0s3
<LOCAL_SUBNET>dev enp0s3
```

The default gateway is:

```text
<DEFAULT_GATEWAY>
```

Traffic directed outside the local subnet is sent to this gateway.

Devices inside `192.168.1.0/24` can be reached directly through `enp0s3`.

## Local Network Connectivity

Connectivity to the default gateway was tested with:

```bash
ping -c 4 <DEFAULT_GATEWAY>
```

Result:

```text
4 packets transmitted
4 packets received
0% packet loss
```

This confirmed that:

* the network interface was active;
* the IPv4 address and subnet were valid;
* the virtual machine could communicate with the router;
* local network connectivity was working.

## Internet Connectivity

IPv4 Internet connectivity was tested using the Cloudflare DNS address:

```bash
ping -c 4 1.1.1.1
```

Result:

```text
4 packets transmitted
4 packets received
0% packet loss
```

This confirmed that the virtual machine could reach the Internet using IPv4.

## DNS Resolution

DNS resolution was tested with:

```bash
resolvectl query google.com
```

The resolver returned multiple IPv4 and IPv6 addresses.

This confirmed that DNS resolution was working correctly.

The active DNS server was inspected with:

```bash
resolvectl status
```

The current IPv4 DNS server was:

```text
<DEFAULT_GATEWAY>
```

The router therefore acts as the DNS resolver or forwards DNS requests to an upstream resolver.

## IPv4 Name Resolution Test

IPv4 connectivity using a domain name was tested with:

```bash
ping -4 -c 4 google.com
```

Result:

```text
4 packets transmitted
4 packets received
0% packet loss
```

This test confirmed that both IPv4 connectivity and DNS resolution were operational.

## IPv6 Configuration

The interface received:

* a global IPv6 address;
* a link-local IPv6 address;
* an IPv6 network prefix;
* a default IPv6 route.

The IPv6 routing table was inspected with:

```bash
ip -6 route
```

A default route was present through a link-local gateway on `enp0s3`.

The IPv6 gateway was successfully reached with:

```bash
ping -6 -c 4 <IPV6_GATEWAY>%enp0s3
```

Result:

```text
4 packets transmitted
4 packets received
0% packet loss
```

This confirmed that IPv6 communication between the virtual machine and the local router was working.

## IPv6 Internet Issue

External IPv6 connectivity was tested with:

```bash
ping -6 -c 4 google.com
```

and:

```bash
ping -6 -c 4 2606:4700:4700::1111
```

Both tests returned:

```text
100% packet loss
```

An HTTPS connection was also tested with:

```bash
curl -6 -I --connect-timeout 10 https://example.com
```

The connection timed out.

This indicates that:

* IPv6 is configured locally;
* the IPv6 gateway is reachable;
* DNS returns IPv6 records correctly;
* external IPv6 connectivity is not operational.

The issue is likely located beyond the virtual machine, such as in the router configuration, firewall rules or ISP IPv6 routing.

No network configuration was changed during this diagnostic phase.

## Troubleshooting Example

An initial gateway test was accidentally executed using:

```text
192.128.1.254
```

instead of:

```text
<DEFAULT_GATEWAY>
```

The incorrect address produced `100% packet loss`.

After correcting the address, the gateway responded successfully.

This demonstrates an important troubleshooting rule:

> Always verify addresses, commands and configuration values before investigating more complex causes.

## Final Status

```text
Network interface:       operational
IPv4 address:            operational
IPv4 default gateway:    operational
Local network:           operational
IPv4 Internet access:    operational
DNS resolution:          operational
IPv6 local gateway:      operational
IPv6 Internet access:    not operational
```

## Commands Practiced

```bash
ip -br address
ip route
ip -6 route
ping
ping -4
ping -6
resolvectl status
resolvectl query
curl
tracepath
```
