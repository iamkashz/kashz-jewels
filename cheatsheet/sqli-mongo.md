# sqli mongo

**NOTE:** `mongo` and `mongosh` both are mongo shells. `mongo` has been deprecated.

## mongosh | mongo

```bash
# always use database if connection fails without it.
mongo[sh] -u USER -p PASS IP:PORT/[DATABASE]
mongo[sh] --host IP -u USER -p PASS [DATABASE]
```

## Interesting Paths

```bash
/opt/bitnami/mongodb/mongodb.conf
/etc/mongod.conf
```

## \[mongo | mongosh] client commands

```bash
# databases
show dbs
use <db>

# collections
show collections

# documents / records
db.<collection>.find({})

# insert record
db.<collection>.insertOne({key: "value"})
# deprecated method 
db.<collection>.insert({key: "value"})

# update record
db.users.updateOne({key1: 'value1'},{$set: {KEY-FOR-WHICH-VALUE-IS-TO-BE-UPDATED: 'NEW-VALUE FOR KEY'}})
# the record to be updated is found using this filter criteria {key1: 'value1'}
# the value is updated for the key specified {KEY-FOR-WHICH-VALUE-IS-TO-BE-UPDATED: 'NEW-VALUE FOR KEY'}
# deprecated method 
db.users.update({FILTER-CRITERIA},{$set:{UPDATE-KEY-VALUE}})
```

## login-brute

* [an0nlk/Nosql-MongoDB-injection-username-password-enumeration](https://github.com/an0nlk/Nosql-MongoDB-injection-username-password-enumeration)

```bash
python nosqli-user-pass-enum.py -u http://IP/ -up username -pp password -ep [username|password] -op login:login -m POST
```

* [Hacktricks/nosql-injection#brute-force-login-usernames-and-passwords-from-post-login](https://book.hacktricks.xyz/pentesting-web/nosql-injection#brute-force-login-usernames-and-passwords-from-post-login)

```bash
# modify code
url = ""
headers = {}
cookies = {}
python exploit.py
```

## Additional Reading

* [Hacktricks.xyz/nosql-injection](https://book.hacktricks.xyz/pentesting-web/nosql-injection)
