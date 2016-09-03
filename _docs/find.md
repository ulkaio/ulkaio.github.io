---
layout: docs
title: Find
permalink: /docs/find/
---

##### Some common use case of find command

Find a folder name `project`

    find . -type d -name project

Find a file `nginx.conf`, exclude permission errors

    find / 2>/dev/null -name nginx.conf

Find with name pattern with time interval

    find . -name 'a.log.*' -mmin -100 -ls

Find a file in `srcdir` and copy them to `destdir`

    sudo find srcdir -name '*log*' -exec cp '{}' destdir \;

File created within `last 5 min`

    find . -mmin -5 -ls

Find and `sort` by time

    find . -name "*log*" -printf "%T+\t%p\n" | sort