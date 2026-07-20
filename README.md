# Linux Home Lab

A practical home-lab project used to study Linux system administration, networking and IT infrastructure.

The lab is based on an **Ubuntu Server virtual machine** running in VirtualBox and managed remotely from a Windows host through SSH.

## Objectives

This repository documents my practical learning path toward junior roles in:

* IT infrastructure;
* Linux system administration;
* networking;
* cloud engineering;
* DevOps and automation.

## Lab Environment

### Host System

* Windows 11
* VirtualBox
* PowerShell
* Visual Studio Code
* Git and GitHub

### Virtual Machine

* Ubuntu Server 24.04 LTS
* OpenSSH Server
* NAT and Bridged networking
* Remote administration through SSH

## Topics Covered

* Ubuntu Server installation and initial configuration
* Package updates and repository management
* Linux users and groups
* File ownership and permissions
* SSH installation and remote access
* Processes and services
* Network interfaces and IP addressing
* Listening ports and active connections
* Basic troubleshooting

## Commands Practiced

```bash
ls
cd
pwd
mkdir
chmod
chown
ps
pstree
systemctl
ss
ip
ssh
```

## Current Lab Status

* Ubuntu Server installed successfully
* System packages updated
* OpenSSH Server installed and enabled
* SSH access tested from Windows PowerShell
* Network mode changed from NAT to Bridged
* Virtual machine reachable through the local network
* Basic users, permissions, services and networking commands tested

## Planned Improvements

* Document the complete Ubuntu Server installation
* Add networking and SSH configuration notes
* Create practical user and permission exercises
* Document services and process management
* Add firewall configuration with UFW
* Install and configure a web server
* Introduce Docker
* Add infrastructure troubleshooting scenarios

## Repository Structure

```text
linux-homelab/
├── README.md
└── docs/
    ├── installation.md
    ├── networking.md
    ├── ssh.md
    ├── users-and-permissions.md
    └── processes-and-services.md
```

The documentation will be expanded progressively as new labs and infrastructure topics are completed.
