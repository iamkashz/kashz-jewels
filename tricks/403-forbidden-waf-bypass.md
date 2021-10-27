# 403 forbidden waf bypass

For pages that

* **Forbidden (403)**
* **requires request from localhost**
* **WAF in between**

```bash
# add HTTP Header
X-Forwarded-For: localhost
```
