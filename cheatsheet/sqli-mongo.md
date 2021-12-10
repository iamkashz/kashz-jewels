~~# sqli mongo

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
# databases (creates if not existing)
show dbs
use DATABASE

# collections
show collections
db.getCollectionNames()
db.createCollection("COLLECTION_NAME")

# documents / records
# operators: $eq $ne $gt $where $exists $regex
db.COLLECTION_NAME.find({})
db.COLLECTION_NAME.find({key:"VALUE"})
db.COLLECTION_NAME.find({key: {"OPERATOR": "VALUE"}})

# insert record
db.COLLECTION_NAME.insertOne({key: "value"})
# deprecated method 
db.COLLECTION_NAME.insert({key: "value"})

# update record
db.users.updateOne({key1: "old-VALUE"},{$set: {key1: "new-VALUE"}})
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

* [Hacktricks.xyz/nosql-injection](https://book.hacktricks.xyz/pentesting-web/nosql-injection)~~
