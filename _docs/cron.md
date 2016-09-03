---
layout: docs
title: Cron
permalink: /docs/cron/
---

This [site](http://crontab.guru/) has easy to use interface for scheduling cron job.

Edit cron job
    
    crontab -e

Run `cmd` every `5 min`

    */5 * * * * python watch.py

Time tuples `minute` `hour` `date` `month` `weekday`

Cron job log
    
    less +F /var/log/syslog

Run curl every `10 min`

    */10 * * * * curl --request POST "url?text=$(hostname -I)" -d ""

Run after 5 sec of `reboot`

    @reboot sleep 5; python report.py

