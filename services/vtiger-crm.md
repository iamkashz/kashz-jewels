# vtiger crm

**NOTE: Possible has Elastix installed as well**

## Version

```bash
# bottom left, version is present
/vtigercrm
```

## Interesting Paths

```bash
# config
/etc/amportal.conf 

# if asterisk call manager is present on system
/etc/asterisk/manager.conf 
```

## VtigerCRM 5.1.0

```bash
# LFI
https://www.exploit-db.com/exploits/37637
https://www.exploit-db.com/exploits/18770

# Shell Upload as display picture
Settings > Under Communication Templates > Company Details > Edit
Upload Company Logo as PHP (if it allows)
```
