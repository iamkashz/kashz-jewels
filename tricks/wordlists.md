# wordlists

## DIR-ENUM | VHOST-ENUM

```bash
# dir
/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
/usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
/usr/share/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt
/usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt

# vhosts
/usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt
/usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt

# special-cases
/usr/share/seclists/Discovery/Web-Content/big.txt
/usr/share/seclists/Discovery/Web-Content/quickhits.txt
/usr/share/seclists/Discovery/Web-Content/PHP.fuzz.txt

# LFI
/usr/share/seclists/Fuzzing/LFI/LFI-LFISuite-pathtotest.txt
```

## PASSWORDS

```bash
/usr/share/john/password.lst
/usr/share/seclists/Discovery/Web-Content/raft-small-words.txt
/usr/share/wordlists/rockyou.txt

# cewl PAGE [-d x] [-m x] [-e] -w pass.txt
# -d depth; -m min_word_length; -e include email-addresses;
```

## USERNAMES

```bash
/usr/share/wordlists/metasploit/unix_users.txt
/usr/share/seclists/Usernames/Names/names.txt
```
