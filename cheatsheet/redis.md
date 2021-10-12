# redis

## [HackTricks Redis](https://book.hacktricks.xyz/pentesting/6379-pentesting-redis)

## Connecting to redis

```
$ redis-cli -h <IP> [--user <USER>] [--pass <PASS>]
[OR]
nmap --script redis-info -sV -p 6379 <IP>

$ nc -vn <IP> 6379
AUTH <username> <password>
+OK (if working)
```

## Interesting Paths

```
/etc/redis/redis.conf
```

## Commands

```
> info
> info [server | keyspace | ...]

# get all keys in memory
> keys *

# select database
> select <number>

# retrieve specific key
> get <key>

# config get dir
> config get [*  | dir]
```
