# fudforum

## Interesting Paths

```bash
# login page
/fudfourm/index.php?t=login

# to update mysql pass, salt is needed; make new user and copy salt and pwdhash
update fud30_users set passwd=PWDHASH, salt=SALT where login='admin';
```

## File upload (authenticated)

v3.0.6

```
Logged in > Administration > Admin Control Panel > (top of General Management) > Files
# can upload php shells.
```
