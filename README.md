# Linux Home Lab

A hands-on environment for learning Linux system administration, networking and core IT infrastructure concepts.

The lab uses an **Ubuntu Server 24.04 LTS virtual machine** running in Oracle VirtualBox, administered from a Windows 11 host.

## Lab Environment

| Component | Configuration |
|---|---|
| Host operating system | Windows 11 |
| Virtualization | Oracle VirtualBox |
| Guest operating system | Ubuntu Server 24.04 LTS |
| Terminal | Windows PowerShell |
| Remote access | OpenSSH |
| Virtual network | NAT during initial setup, later Bridged Adapter |

## Documentation

The repository currently contains the following lab notes:

- [Ubuntu Server installation and initial setup](docs/installation.md)
- [Network configuration and connectivity troubleshooting](docs/networking.md)

These documents describe the setup and tests actually performed in the lab.

## Topics Practiced

The environment is used to practise and explore:

- Linux command-line navigation and file management;
- package management with APT;
- users, groups, ownership and permissions;
- SSH remote administration;
- processes and system services;
- network interfaces, IP addressing and routing;
- DNS resolution and connectivity troubleshooting.

Documentation will be added as each topic is developed and verified.

## Commands Practiced

Examples of commands used in the lab:

```bash
pwd
whoami
ls
cd
mkdir
chmod
chown
sudo apt update
sudo apt upgrade
systemctl
ps
ip
ss
ping
resolvectl
ssh
```

## Current Status

- Ubuntu Server 24.04 LTS installed in VirtualBox.
- Initial package updates completed.
- OpenSSH Server installed and tested.
- Remote SSH access tested from Windows PowerShell.
- VirtualBox networking changed from NAT to Bridged Adapter.
- IPv4 connectivity and DNS resolution tested.
- Local IPv6 connectivity tested; external IPv6 connectivity was not working during the documented test.

## Planned Work

- Add separate, verified notes for users, groups and permissions.
- Document SSH configuration and safe remote-access practices.
- Expand notes on processes and services.
- Practise firewall configuration with UFW.
- Deploy and configure a basic web server.
- Continue with additional networking and system-administration exercises.

## Repository Structure

```text
linux-homelab/
├── README.md
└── docs/
    ├── installation.md
    └── networking.md
```

## Purpose

This repository is a learning log. It records practical exercises, command-line work, configuration steps and troubleshooting results as the lab develops.

The notes are based on a local virtualized environment. Network addresses and results may differ on other systems.
