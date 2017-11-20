---
layout: single
title: Change ssh port of CentOS 7 
date: 2017-11-08 00:32:00 +0600
categories: 
    - Linux
excerpt: Change ssh port of CentOS 7 
tags:
    - CentOS 7
    - SSH
---
To change SSH port of CentOS 7 please follow those steps-

1. At first backup the default configuration file. It is always a best practice to backup files before modification, so that we can restore it if anything unwanted happends. 
```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```

2. Then open the `sshd_config` file -
```bash
sudo vi /etc/ssh/sshd_config
```
and change the port number(ex. 2122) -
```config
Port 2122
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
```
3. By default, SELinux only allows port 22 for SSH. What you need to do is enable the newly created port through SELinux. To do that, run the commands below
```bash
sudo semanage port -a -t ssh_port_t -p tcp 2122
```

4. Add the new port to the firewall to allow access
```bash
sudo firewall-cmd --permanent --zone=public --add-port=2122/tcp
```

5. Reload the firewall configuration file -
```bash
sudo firewall-cmd --reload
```

6. Now restart SSH service
```bash
sudo systemctl restart sshd.service
```

7. Now exit and try to connect to new port
```bash
ssh username@192.168.10.240 -p 2022
```

Enjoy