# enumeration manual

## Path fix

```bash
export PATH=/bin:/usr/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/sbin:$PATH
```

## Basic checks

[Get process info using /proc](https://stackoverflow.com/questions/29105448/get-process-info-from-proc)

```bash
# all files in current dir (recursive)
find . -type f -ls

# OS name, version
cat /etc/issue
cat /etc/*-release
cat /proc/version
ldd --version

# username
cat /proc/self/environ

# IP address (without ifconfig)
cat /etc/sysconfig/network-scripts/<files> | grep IP

# internal ports
netstat -anot | netstat -alnp | netstat -antp | netstat -tulnp
netstat -anp tcp #freeBSD

# process running on port
lsof -i:PORT

# extended perms
getfacl [FILE | FOLDER]

# processes
ps fauxwww

# firewall enum
grep -Hs iptables /etc/*
```

## Search for text in files (and !)

```bash
# search keyword in all files recursive
grep -iR "<keyword>" <SEARCH-PATH> --color=alwauys 2>/dev/null
grep -Rnw <path-to-search> -ie "<keyword>" --color=always 2>/dev/null

# grep all files not containing certain text
grep -L "TEXT_FILE_SHOULD_NOT_CONTAIN" [files | *.extension]

# print file contents without comments (#) and removes the empty lines.
grep -v "^[#;]" FILE | grep -v "^$" 
```

## SUID file check

```bash
find / -perm /4000 -type f -exec ls -lda {} \; 2>/dev/null
find / -type f -a \( -perm -u+s -o -perm -g+s\) -exec ls -l {} \; 2> /dev/null
find / -perm -u=s -type f 2>/dev/null
```

## GUID file check

```bash
find / -group <> 2>/dev/null
```

## CAP file check

```bash
# capabilities
getcap -r / 2>/dev/null
```
