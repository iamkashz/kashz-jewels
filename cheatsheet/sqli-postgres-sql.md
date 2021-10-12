# sqli postgres-sql

## Connect

```bash
psql -h IP -p PORT -U <user> [-c query-to-execute]
```

## Default creds

```
postgres:postgres
```

## Interesting Paths

```bash
/postgresql/data/postgresql.conf
```

## postgres commands

Cheatsheet: [http://pentestmonkey.net/cheat-sheet/sql-injection/postgres-sql-injection-cheat-sheet](http://pentestmonkey.net/cheat-sheet/sql-injection/postgres-sql-injection-cheat-sheet)

```bash
\x: pretty display

# comments
--
/* <blah> */

# hostname

# version
version()

# show config file
SHOW config_file

# read dir, files
SELECT pg_ls_dir('<dir-path>')
SELECT pg_read_file('<file>')
OR
CREATE TABLE <t-name> (out TEXT)
COPY <t-name> FROM '<file>'
# data is appended on multiple COPY
SELECT * FROM <t-name>
TRUNCATE <t-name> 

# users
\du;
SELECT user;
SELECT current_user;
SELECT session_user;
SELECT getpgusername();
| SELECT usename FROM pg_user;

# password (md5)
SELECT passwd FROM pg_shadow

# databases
current_database()
| SELECT datname FROM pg_database


# tables
\dt
\dt+
\d+ <table>

# cols

# nth row
```
