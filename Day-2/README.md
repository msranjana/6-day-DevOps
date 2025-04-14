# DevOps Training - Day 2: AWS Account Creation & Basic Linux Commands

## Overview

Second day of the DevOps class focused on practical implementation, shifting from theory to hands-on experience. The main objectives were to set up a personal AWS account, launch a virtual server using EC2, and gain basic familiarity with the Linux commands.

---

## AWS Account Creation

We began the session by the process of creating an AWS account:

- Entered personal and contact information
- Added debit card details for billing verification
- Understood AWS pricing models:
  - **Free Tier**: Best for beginners and testing purposes
  - **Pay-As-You-Go**: Usage-based pricing suitable for scaling and production

---

## Launching an EC2 Instance on AWS

A step-by-step guide was followed to create and connect to a virtual machine:

1. Log in to the AWS Management Console
2. Navigate to the EC2 service
3. Click on "Launch Instance"
4. Set a name for the instance
5. Choose an instance type (e.g., `t2.micro` under free tier)
6. Select an OS (Amazon Linux in our case)
7. Create or select an existing key pair (for SSH access)
8. Set up a security group (allow SSH port 22)
9. Launch the instance
10. Wait for the instance to start
11. Copy the public IP address
12. Use PuTTY to connect:
    - Paste IP in "Host Name"
    - Load `.ppk` key under SSH > Auth
    - Click "Open"
    - Login as `ec2-user`

Once connected, we had access to a live Linux-based server.

---

## Introduction to Linux Basics

After connecting to the EC2 instance, we explored fundamental Linux commands and concepts. These are critical for system administration and cloud infrastructure tasks.

### Directory and File Management

| Command            | Description                             |
|--------------------|-----------------------------------------|
| `pwd`              | Show current directory                  |
| `ls`, `ls -l`, `ls -a` | List files in various formats         |
| `cd <dir>`         | Change directory                        |
| `cd ..`            | Go up one directory level               |
| `mkdir <folder>`   | Create new directory                    |
| `rmdir <folder>`   | Remove empty directory                  |
| `touch <file>`     | Create empty file                       |
| `rm <file>`        | Delete a file                           |
| `rm -r <folder>`   | Delete a directory and its contents     |
| `mv <src> <dest>`  | Move or rename a file or directory      |
| `cp <src> <dest>`  | Copy files or directories               |

### File Viewing and Editing

| Command               | Description                          |
|------------------------|--------------------------------------|
| `cat <file>`           | Display file contents                |
| `more`, `less`         | View large files page by page        |
| `head`, `tail`         | Show beginning or end of a file      |
| `nano`, `vi`           | Open file in text editors            |
| `echo "text" > file`   | Write to file (overwrite)            |
| `echo "text" >> file`  | Append to file                       |

### Package Management (Amazon Linux - YUM)

| Command                 | Description                         |
|--------------------------|-------------------------------------|
| `yum update`             | Update all packages                 |
| `yum install httpd`      | Install Apache HTTP server          |

YUM (Yellowdog Updater Modified) is the default package manager on Red Hat-based systems like Amazon Linux.

### Service Management

| Command                  | Description                         |
|--------------------------|-------------------------------------|
| `service httpd status`   | Check Apache server status          |
| `service httpd start`    | Start Apache server                 |

---

## Linux Distributions and Web Servers

| Linux Family  | Example OS           | Common Web Servers         |
|---------------|----------------------|-----------------------------|
| Red Hat       | Amazon Linux, RHEL   | httpd (Apache)             |
| Debian        | Ubuntu, Debian       | apache2, nginx             |

Different Linux families use different package names and service tools.

---

## Additional Linux Commands and Concepts

### System Monitoring

| Command           | Description                                |
|--------------------|--------------------------------------------|
| `clear`            | Clear terminal screen                      |
| `history`          | View command history                       |
| `whoami`           | Display current user                       |
| `uname -a`         | System information                         |
| `uptime`           | System uptime                              |
| `top`, `htop`      | Monitor running processes                  |
| `free -h`          | View memory usage                          |
| `df -h`            | Check disk space usage                     |

### Process Management

| Command          | Description                            |
|------------------|----------------------------------------|
| `ps aux`         | List all running processes             |
| `kill <PID>`     | Terminate process                      |
| `kill -9 <PID>`  | Force kill a process                   |
| `bg`, `fg`       | Manage background/foreground jobs      |

### User Management

| Command                | Description                         |
|-------------------------|-------------------------------------|
| `adduser <username>`    | Add new user                        |
| `passwd <username>`     | Set or change password              |
| `who`                   | Show logged-in users                |
| `su - <username>`       | Switch user                         |

### Debian-Based Package Management (APT)

| Command                      | Description                         |
|-------------------------------|-------------------------------------|
| `sudo apt update`            | Refresh package list                |
| `sudo apt upgrade`           | Upgrade installed packages          |
| `sudo apt install <pkg>`     | Install new package                 |
| `sudo apt remove <pkg>`      | Remove installed package            |

---
