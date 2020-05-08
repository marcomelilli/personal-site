---
template: post
title: How to secure your VPS with Fail2ban
slug: how-to-install-and-configure-fail2ban
draft: false
date: 2020-05-08T16:13:27.609Z
description: >-
  How to install and configure Fail2ban on Centos and Debian to protect your
  virtual private server
category: VPS
tags:
  - security
  - debian
  - centos
  - ssh
---
When you configure a new server **Fail2ban** is a *must*-*have* tool to secure your [VPS](https://marcomelilli.com/category/vps/). 

Fail2Ban **scans log** files and **bans IPs** that show the malicious signs (e.g. too many password failures, seeking for exploits, etc..). This tool update your firewall rules to reject the IP addresses for a specified **amount of time**, although any arbitrary other **action** (e.g. sending an email) could also be configured.

## **How to install**

### Centos

* Update the system, install EPEL repository and Fail2Ban:

  ```shell
    yum update && yum install epel-release
    yum install fail2ban
  ```
### Debian

* Update the system and install Fail2Ban: 

   ```shell
   apt-get update && apt-get upgrade -y
   sudo apt-get install fail2ban
   ````

## Configure

Fail2ban reads `.conf`configuration files first, then `.local` files override any settings. So the best way is edit the local configuration to override the defailt settings.

* Create a new local config file starting from the default one:\
  `cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`
* If using **CentOS** change the **backend** option in `jail.local` from *auto* to *systemd*. This is not necessary on **Debian:**

  ```editorconfig
  # Available options are "pyinotify", "gamin", "polling", "systemd" and "auto".
  backend = systemd
  ```
* The most important info that you can configure are inside the section `sshd` :

   ```editorconfig
   [sshd] 
   enabled = true
   # "bantime" is the number of seconds that a host is banned.
   bantime = 3600
   # ssh port
   port = 22
   # "maxretry" is the number of failures before a host get banned.
   maxretry = 6
   ```

## Running Fail2Ban service

### Centos

   ```shell
   systemctl enable fail2ban
   systemctl start fail2ban
   ```

### Debian

   ```shell
   service fail2ban restart
   ```

## Check the Fail2Ban Status

To check the status of the Fail2Ban jails:

   ```shell
   fail2ban-client status
   ```

The result should be like this:

   ```editorconfig
   Status
   |- Number of jail: 1
   `- Jail list: sshd
   ```

If you want to see banned IPs in sshd jail:

   ```
   fail2ban-client status sshd
   ```

## Ban/Unban manually an IP address

In order to add/remove an IP address from the banned list use the following commands replacing IPADDRESS with the IP which needs unbanning, and the name "sshd" with name of the jail (in this case the "sshd" jail that we configured above):

   ```
   fail2ban-client set sshd banip IPADDRESS
   fail2ban-client set sshd unbanip IPADDRESS
   ```