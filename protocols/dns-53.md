# dns :53

TCP is only used in DNS when the response size is greater than 512 bytes.

## DNS Version

```bash
$ dig version.bind CHAOS TXT @IP
$ nmap --script dns-nsid IP
```

## Domain Name Loopup

```bash
$ nslookup
> server IP
> IP
# should give you domain information

dig @IP -x IP
```

## Zone Transfer Check

Check for additional sub-domains

```bash
$ host -l <domain> <IP>
[OR]
$ dig axfr @<IP> <domain>

# find domains
wfuzz -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u "http://<DOMAIN>" -H "HOST: FUZZ.<DOMAIN>"
# when run you'll see a lot of page coming with a specified number of characters, to eliminate them add flag
--hh <character-value>
```

## Adding key to DNS using nsupdate

[see nsupdate.](../services/nsupdate.md)
