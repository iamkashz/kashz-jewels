# subnet scan

## bash script

```bash
for i in {1..255}; do (ping -c 1 X.X.X.${i} | grep "bytes from" &); done
```

## nmap

```bash
nmap -sn X.X.X.1-255
nmap -sn X.X.X.0/24
```