---
layout: docs
title: Systemd
permalink: /docs/systemd/
---

Listing running services

    systemctl

Service file location
    
    /etc/systemd/system

Sample script `vi` /etc/systemd/system/multi-user.target.wants/redis-server.service

```sh
[Unit]
Description=Advanced key-value store
After=network.target

[Service]
Type=forking
ExecStart=/usr/bin/redis-server /etc/redis/redis.conf
ExecStop=/usr/bin/redis-cli shutdown
Restart=always
User=redis
Group=redis

[Install]
WantedBy=multi-user.target
```

`vi` /etc/systemd/system/multi-user.target.wants/ssh.service

```
[Unit]
Description=OpenBSD Secure Shell server
After=network.target auditd.service
ConditionPathExists=!/etc/ssh/sshd_not_to_be_run

[Service]
EnvironmentFile=-/etc/default/ssh
ExecStart=/usr/sbin/sshd -D $SSHD_OPTS
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure

[Install]
WantedBy=multi-user.target
Alias=sshd.service
```


NAME        | DESCRIPTION
------------|------------
ExecStartPre| Commands that will run before ExecStart.
ExecStart   | Main commands to run for this unit.
ExecStartPost|Commands that will run after all ExecStart commands have completed.
ExecReload  | Commands that will run when this unit is reloaded via systemctl reload foo.service
ExecStop    | Commands that will run when this unit is considered failed or if it is stopped via systemctl stop foo.service
ExecStopPost| Commands that will run after ExecStop has completed.
RestartSec  | The amount of time to sleep before restarting a service. Useful to prevent your failed service from attempting to restart itself every 100ms.

##### Command examples

Basic
    
    systemd --version
    whereis systemd
    whereis systemctl

Analyze time taken by each process at boot

    systemd-analyze blame

List all the available units

    systemctl list-unit-files    

Manage life cycle of a service
    
    systemctl start httpd.service
    systemctl restart httpd.service
    systemctl stop httpd.service
    systemctl reload httpd.service
    systemctl status httpd.service
    systemctl kill httpd

List all system mount points
    
    systemctl list-unit-files --type=mount
    systemctl start tmp.mount
    systemctl stop tmp.mount
    systemctl restart tmp.mount
    systemctl reload tmp.mount
    systemctl status tmp.mount

List all available system sockets

    systemctl list-unit-files --type=socket

Reference  
* [coreos systemd](https://coreos.com/docs/launching-containers/launching/getting-started-with-systemd/)  
* [redhat systemd] (https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sect-Managing_Services_with_systemd-Unit_Files.html)  
* [Systemd tips](https://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks/)  