# centreon

## Default Credentials

```
root:centreon
admin:centreon
# brute force needs CRSF token
```

## Brute Force Login + RCE

v19.04.0

```
https://github.com/0xskunk/Centreon-v19.04-Brute-Forcer-RCE
[OR]
# brute force via intruder,
# need to use intruder (attack: pitchfork), recursive grep -> to fetch centreon_token and set resource-pool:1 (1 thread at a time).
```
