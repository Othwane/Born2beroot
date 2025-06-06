# Born2BeRoot - 42 System Administration Project

## Project Description
Born2BeRoot is a system administration project that teaches how to securely configure a Linux server. The project involves setting up a virtual machine with encrypted partitions, implementing strict security policies, and configuring essential services according to specific guidelines.

## Table of Contents
1. [Requirements](#requirements)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Verification](#verification)
5. [Submission](#submission)
6. [Bonus](#bonus)
7. [Resources](#resources)

## Requirements

### Mandatory
- Virtual Machine: Debian (recommended) or Rocky Linux without GUI
- Partitioning:
  - Minimum 2 encrypted LVM partitions
  - Example structure:
    ```
    /boot - 500MB (unencrypted)
    / - 10GB (encrypted LVM)
    /home - 7.5GB (encrypted LVM)
    swap - 2GB (encrypted LVM)
    ```
- Security:
  - SSH on port 4242 only
  - Root SSH login disabled
  - Firewall allowing only port 4242
  - SELinux (Rocky) or AppArmor (Debian) enabled

### Password Policy
- Minimum 10 characters (uppercase, lowercase, number)
- Expires after 30 days
- 2-day minimum between changes
- 7-day warning before expiration
- Maximum 3 consecutive identical characters

### Monitoring
- Bash script (`monitoring.sh`) displaying:
  - System architecture and kernel version
  - CPU and memory usage
  - Disk utilization
  - Network information
  - Sudo command count
- Runs every 10 minutes via cron

## Installation

1. Download Debian or Rocky Linux ISO
2. Create VM in VirtualBox/UTM with:
   - Minimum 20GB disk
   - 2GB RAM recommended
3. During installation:
   - Select manual partitioning
   - Set up encrypted LVM
   - Do not install graphical environment

## Configuration

### Partition Setup
```bash
lsblk  # Verify partition structure
cryptsetup luksDump /dev/sda5  # Check encryption
    

### User and Groups
