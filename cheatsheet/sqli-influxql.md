# sqli influxql

**influxDB** (written in Go) is an open source **time-series database** that is _used for storage and retrieval of time
series data_.

## Connect

InfluxDB supports both **password and JWT based authentication**. JWT is an authentication method that is based on a
**"shared secret"**, which is known to both parties. If an external party knows the **"secret"**, it can create valid
tokens and authenticate with them.

## influxql commands

```bash
# list all dbs
SHOW DATABASES;
USE db;

# list all users
SHOW USERS;

# list measurements
SHOW MEASUREMENTS;

# read value from a measurement_var
SELECT * from "MEASUREMENT_VAR";

# list series
SHOW SERIES;

# list tag keys
SHOW TAG KEYS;
```

* [gist.github.com/tomazursic/6cc217e2644c619ceceefb8ce824925b](https://gist.github.com/tomazursic/6cc217e2644c619ceceefb8ce824925b)
* [songrgg.github.io/influxdb-command-cheatsheet/](https://songrgg.github.io/operation/influxdb-command-cheatsheet/)

## References

* [komodosec.com/when-all-else-fails-find-a-0-day](https://www.komodosec.com/post/when-all-else-fails-find-a-0-day)