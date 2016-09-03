---
layout: docs
title: Find
permalink: /docs/find/
---

##### Find


Find a folder name abc

    find . -type d -name abc

Find filename, exclude permission errors

    find / 2>/dev/null -name nginx.conf

Find with name pattern with time interval

    find . -name 'a.log.*' -mmin -100 -ls
    find . -name '*log*' -print

Find and copy

    sudo find . -name '*log*' -exec cp '{}' . \;

File created within last 5 min

    find . -mmin -5 -ls

Find sort by time

    find . -name "*log*" -printf "%T+\t%p\n" | sort