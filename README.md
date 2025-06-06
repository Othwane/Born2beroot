# Born2beRoot

## Project Overview

Born2beRoot is a foundational system administration project focused on introducing virtualization and server setup concepts. The goal is to build and configure a secure Linux server from scratch using VirtualBox (or UTM), adhering to strict guidelines regarding services, permissions, users, and security policies.

## Table of Contents

- Project Overview
- Project Requirements
- System Setup
- Security Configuration
- Monitoring Script
- Bonus Features
- Submission Guidelines
- Evaluation Notes

## Project Requirements

- Virtualization: Use VirtualBox (or UTM if unavailable) to create a virtual machine.
- Operating System: Choose either:
  - Latest Debian Stable (Recommended for beginners)
  - Latest Rocky Linux Stable
- Graphical Interfaces: Not allowed (e.g., X.org, GNOME, KDE, etc.)
- Encrypted Partitions: Set up at least 2 encrypted LVM partitions.
- SSH:
  - Enabled on port 4242
  - Root login via SSH must be disabled
- Firewall:
  - Debian: Use UFW
  - Rocky: Use firewalld
  - Only port 4242 must be open
- Hostname:
  - Set to your login followed by 42 (e.g., wil42)
- Users:
  - Create a user with your login
  - This user must be part of user42 and sudo groups

## Security Configuration

### Password Policy

- Password must expire after 30 days
- Password cannot be changed within 2 days
- Show warning 7 days before expiry
- Requirements:
  - Min. 10 characters
  - At least 1 uppercase, 1 lowercase, and 1 digit
  - No more than 3 identical consecutive characters
  - Must not include username
  - Root password also must comply

### Sudo Rules

- Max 3 authentication attempts
- Show custom error message on incorrect password
- Log inputs and outputs of sudo commands to /var/log/sudo/
- Enable TTY mode
- Restrict PATH usage:
  /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin

## Monitoring Script

Create a monitoring.sh Bash script to output system statistics to all terminals every 10 minutes using wall.

### Required Metrics

- System architecture and kernel version
- Physical and virtual CPU count
- RAM usage and percentage
- Disk usage and percentage
- CPU load
- Last boot time
- LVM usage status
- Active TCP connections
- Logged-in users count
- IPv4 and MAC address
- Number of sudo commands run

The script must run silently and without errors. It should also be stoppable via cron.

## Bonus Features

The bonus part will only be evaluated if the mandatory part is 100 percent perfect.

Optional enhancements include:

- Advanced partitioning structure
- Setting up a full WordPress stack with:
  - lighttpd
  - MariaDB
  - PHP
- Implementing an additional useful service (excluding NGINX/Apache2)

Bonus services may require opening additional ports—firewall rules must be adjusted accordingly.

## Submission Guidelines

1. Only submit a signature.txt file at the root of your Git repository.
2. This file must contain the SHA1 signature of your VM disk:
   - For .vdi (VirtualBox):  
     - Linux: sha1sum your_vm.vdi
     - macOS: shasum your_vm.vdi
     - Windows: certUtil -hashfile your_vm.vdi sha1
   - For .qcow2 (UTM):  
     - shasum your_vm.utm/Images/disk-0.qcow2

Do not include the VM itself in your repository.

## Evaluation Notes

- Snapshots are strictly forbidden — their presence will result in a 0 grade.
- Be prepared to:
  - Change your hostname
  - Create and configure new users/groups during the defense
  - Demonstrate and explain your monitoring script
  - Answer theoretical questions about tools used (e.g., apt vs. aptitude, AppArmor, SELinux)

## Tools and Utilities

- LVM: Logical Volume Manager for encrypted partitions
- UFW / Firewalld: Firewall configuration
- SSH: Secure remote access
- sudo: Privileged command execution
- cron / wall: Scheduling and message broadcasting

## Learning Objectives

- Understand system installation and configuration at the OS level
- Learn virtualization and security best practices
- Automate monitoring with scripting
- Harden systems through policy enforcement