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

#### Example taken from find (GNU findutils) 4.4.2

Find files named `core` in or below the directory `/tmp` and delete them. Note that this will work incorrectly if there are any filenames containing newlines, single or double quotes, or spaces.

    find /tmp -name core -type f -print | xargs /bin/rm -f

Runs `file` on every file in or below the current directory.  Notice that the braces are enclosed in single quote marks to protect them from interpretation  as shell script punctuation. The semicolon is similarly protected by the use of a backslash, though single quotes could have been used in that case also.

    find . -type f -exec file '{}' \;

All three of these commands do the same thing, but the first one uses the `octal` representation of the file mode, and the other two use the `symbolic`
form. These  commands all search for files which are writable by either their owner or their group. The files don't have to be writable by both
the owner and group to be matched; either will do.
    
    find . -perm /220
    find . -perm /u+w,g+w
    find . -perm /u=w,g=w
