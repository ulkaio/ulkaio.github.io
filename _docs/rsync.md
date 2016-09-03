---
layout: docs
title: Rsync
permalink: /docs/rsync/
---

This [site](http://www.tecmint.com/rsync-local-remote-file-synchronization-commands/) has more examples.

Copy `srcfile` to `destfile` with progress bar

    rsync -rv srcfile destfile --progress 

Rsync folder `srcdir` to `server` via `ssh`

    rsync -a srcdir server:

Rsync file with matching `pattern`

    rsync -t *.java server:~/dest/

Options:
`-t` pattern
`-z` compressed
`-v` verbose
`-a` archive
`-r` recursive


Install 3.1.2 on centos

```sh
sudo yum groupinstall 'Development Tools' -y
wget https://www.samba.org/ftp/rsync/src/rsync-3.1.2.tar.gz
tar -xvzf rsync-3.1.2.tar.gz
cd rsync-3.1.2
./configure --prefix=/usr --without-included-zlib
make
sudo make install
rsync -v
```