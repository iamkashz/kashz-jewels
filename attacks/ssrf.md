---
description: Server Side Request Forgery
---

# SSRF

Vulnerability that allows a malicious user to cause the webserver to make an additional or edited HTTP request to the
resource of the attacker's choosing.

## Reflected SSRF Examples

### 1

Actual Request:`http://IP/cart?item=http://sub.domain.com/api/cart/item?id=123`

Attack: `http://IP/cart?item=http://sub.domain.com/api/user`

### 2

Actual Request:`http://IP/cart?item=/item?id=123`

Attack: `http://IP/cart?item=../../user`

### 3

Actual Request:`http://kashz.com/file?server=api&id=123` > `http://api.kashz.com/file?id=123`

Attack: `http://kashz.com/file?server=dev.kashz.com/api/user&x=&id=123`
This forces the server to make request like `http://dev.kashz.com/api/user&x=.kashz.com/file&id=123`

## Blind SSRF

Use [https://requestbin.com/](https://requestbin.com/)

## Protections

* Allow list
* Deny list