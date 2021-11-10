# hashcat

```bash
hashcat [-a <> ] -m <MODE> <hash-file> <dictionary-file> [-r <rule-file>] [-w <wordload_profile>] [-O]
# rule: /usr/share/hashcat/rules/
# -w: =3 gives a more tuned experience on your desktop, but it can also be slower. =1 to utilize more of your GPU. =2 Default
# -O: --optimized-kernel-enable, this limits the password length.

# ntlm hash, copy entire hash
hashcat -m 5600 hash /usr/share/wordlists/rockyou.txt
```

{% embed url="https://hashcat.net/wiki/doku.php?id=example:hashes" %}
