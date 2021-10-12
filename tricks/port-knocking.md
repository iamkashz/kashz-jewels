# port knocking

## info

```bash
# service name
/usr/sbin/knockd

# config file
/etc/knockd.conf
```

## port knock

```bash
# knock tool
knock DOMAIN|IP PORT1 PORT2 PORT3 ...

# script
$ for i in PORT1 PORT2 PORT3; do
for> nmap -Pn --host-timeout 100 --max-retries 0 -p $i IP >/dev/null
for> done;
```
