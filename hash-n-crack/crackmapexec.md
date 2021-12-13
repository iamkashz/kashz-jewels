# crackmapexec

Supports smb, ldap, ssh, winrm, mssql

```bash
crackmapexec PROTOCOL IP[/CIDR] [--port PORT] [-d DOMAIN] -u USER|USER.txt -p PASS|PASS.txt [-H HASH|HASH.txt]
--share SHARE
--local-auth: authenticate locally to each target
--continue-on-success
```

## Credential Gathering flags

* dumps SAM: `--sam`
* dumps LSA secrets: `--lsa`
* dumps NTDS.dit: `--ntds`

## Enumeration

* get all shares: `--shares`
* get sessions: `--sessions`
* get logged-on users: `--loggedon-users`
* get domain users: `--users`
* get domain groups: `--groups`

## File commands

* upload: `--put-file FILE TARGET_PATH_FILE`
* download: `--put-file TARGET_PATH_FILE FILE`

## Command Execution

* method of commmand execution: `--exec-method [smbexec|atexec|mmcexec|wmiexec]`
* specific command for cmd: `-x COMMAND`
* specific command for powershell: `-X COMMAND`

## SMB

```bash
# to get password policy
crackmapexec smb IP -u '' -p '' --pass-pol
```