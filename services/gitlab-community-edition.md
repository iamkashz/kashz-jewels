# gitlab community edition

## Interesting Paths

```
# version of Gitlab Community Edition
IP/help

# login page
IP/users/sign_in

# config file
/opt/gitlab/embedded/service/gitlab-rails/config/secrets.yml
```

## Exploits

```
CE v11.4.7
https://www.exploit-db.com/exploits/49334

CE v12.9.0 and below
https://github.com/thewhiteh4t/cve-2020-10977
https://www.exploit-db.com/exploits/48431 (!)

CE v12.8.1
https://github.com/thewhiteh4t/cve-2020-10977
https://hackerone.com/reports/827052

RCE for old gitlab version <= 11.4.7 & 12.4.0-12.8.1
LFI for old gitlab versions 10.4 - 12.8.1
# make changes to code
https://github.com/dotPY-hax/gitlab_RCE
```
