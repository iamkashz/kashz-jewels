# ffuf wfuzz feroxbuster gobuster

## gobuster

```bash
# directory mode
gobuster dir -u IP -w WORDLIST -x EXTENSION -t 70

# vhosts mode
gobuster vhost -u DOMAIN|IP -w WORDLIST -t 100 [-r]
# try -r if need to use wildcard

--proxy scheme://IP:PORT (ex. socks5://127.0.0.1:6900)
```

## wfuzz

```bash
# directory mode
wfuzz -c -t 60 -w WORDLIST -u IP/FUZZ [-b COOKIE] [-d POST-DATA] [-H HEADER] [-z TYPE,PAYLOAD]
-c: show output in color
-z: alias for -z file,WORDLIST; can do -z range,1-100

# vhosts mode
wfuzz -c -w WORDLIST -u DOMAIN -H "HOST: FUZZ.DOMAIN" [--hh ignore-errors-chars]

--hc: status code to ignore
--hw: word length to ignore
--hh: char length to ignore
--hl: line length to ignore
```

## ffuf

```bash
ffuf -ic -w WORDLIST -e EXTENSION -u IP/FUZZ
-ic ignore comments in wordlist
-e Comma separated list of extensions. Extends FUZZ keyword.
-H header
-mc match status code for all requests (show only these status codes)
-ml match lines
-mw match words
-ms match size

-fc filter status code from response
-fl filter lines
-fw filter words
-fs filter size

# can define multiple wordists and use incase of user:pass
ffuf -w WORDLIST_USEr:W1,WORDLIST_PASS:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/

# will use POST request
-d  'data'
```

## feroxbuster

```bash
feroxbuster -u IP -t 90 -x EXTENSIONS -w WORDLIST
```