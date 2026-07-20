# Ubuntu Server Installation

This document describes the installation and initial configuration of the Ubuntu Server virtual machine used in this home lab.

## Objective

The objective of this lab was to create a clean Linux server environment for practicing:

* system administration;
* networking;
* remote access;
* service management;
* permissions;
* infrastructure troubleshooting.

## Lab Environment

### Host Machine

* Operating system: Windows 11
* Hypervisor: Oracle VirtualBox
* Terminal: Windows PowerShell
* Remote access client: OpenSSH client

### Virtual Machine

* Operating system: Ubuntu Server 24.04 LTS
* Virtualization platform: VirtualBox
* Initial network mode: NAT
* Current network mode: Bridged Adapter
* Remote administration: SSH

## Virtual Machine Creation

A new virtual machine was created in VirtualBox with resources suitable for a basic Linux server lab.

The virtual machine was configured without a graphical desktop environment because the objective was to practice server administration through the command line.

## Ubuntu Server Installation

Ubuntu Server was installed using the official installation image.

During the installation process:

1. the system language and keyboard layout were selected;
2. the virtual disk was configured;
3. a local administrative user was created;
4. the hostname was configured;
5. the base operating system was installed;
6. the machine was restarted;
7. the installation image was removed from the virtual drive.

## Initial Login

After installation, access to the server was performed using the local user account created during setup.

The current user can be verified with:

```bash
whoami
```

The hostname can be verified with:

```bash
hostname
```

The current working directory can be displayed with:

```bash
pwd
```

## System Updates

After the first login, the package information was refreshed:

```bash
sudo apt update
```

Available package upgrades were installed with:

```bash
sudo apt upgrade
```

The system initially reported a large number of available updates, including security updates.

## Repository Configuration

During the initial update process, the system attempted to use the Ubuntu installation media as a package source.

The obsolete CD-ROM repository entry was disabled so that packages could be downloaded from the configured online Ubuntu repositories.

The package information was then refreshed again:

```bash
sudo apt update
```

## OpenSSH Server Installation

OpenSSH Server was installed to allow remote administration:

```bash
sudo apt install openssh-server
```

The service status was checked using:

```bash
systemctl status ssh
```

The service was enabled so that it starts automatically when the server boots:

```bash
sudo systemctl enable ssh
```

The service can be started manually with:

```bash
sudo systemctl start ssh
```

## Network Verification

The server network interfaces and IP addresses were checked with:

```bash
ip address
```

or:

```bash
ip a
```

With VirtualBox configured in NAT mode, the virtual machine initially received an address similar to:

```text
10.0.2.15
```

The network mode was later changed to Bridged Adapter so that the server could receive an address from the local network.

After the change, the server received a local address similar to:

```text
192.168.1.22
```

## SSH Connection from Windows

From Windows PowerShell, the server was accessed with:

```powershell
ssh simone@192.168.1.22
```

The command includes:

* `ssh`: the remote access client;
* `simone`: the Linux user;
* `192.168.1.22`: the server IP address.

At the first connection, the server fingerprint was accepted and the Linux user password was entered.

The successful connection confirmed that:

* the virtual machine was reachable;
* the SSH service was running;
* port 22 was listening;
* the credentials were valid;
* the Windows host and Linux server could communicate.

## Service and Port Verification

Listening ports were checked with:

```bash
ss -tulpn
```

The SSH service was visible on port:

```text
22
```

The server also showed local DNS services managed by `systemd-resolved`.

## Commands Practiced

During this phase, the following commands were used:

```bash
whoami
hostname
pwd
ip a
sudo apt update
sudo apt upgrade
sudo apt install
systemctl status
systemctl enable
systemctl start
ss -tulpn
ssh
```

## Validation

The installation was considered successful after confirming that:

* Ubuntu Server booted correctly;
* the administrative user could log in;
* package repositories were working;
* system updates were installed;
* OpenSSH Server was installed;
* the SSH service was running;
* the server had a valid local IP address;
* remote access from Windows PowerShell worked correctly.

## Security Notes

No passwords, private keys or sensitive credentials are stored in this repository.

IP addresses shown in this documentation refer only to a private local network and may change depending on DHCP configuration.

## Current Status

The Ubuntu Server virtual machine is operational and ready for additional labs involving:

* users and groups;
* file permissions;
* services and processes;
* network troubleshooting;
* firewall configuration;
* web services;
* Docker;
* infrastructure automation.

