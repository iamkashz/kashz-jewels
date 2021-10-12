# ffuf wfuzz feroxbuster gobuster

## gobuster

```bash
# directory mode
gobuster dir -u IP -w WORDLIST -x EXTENSION -t 70

# vhosts mode
gobuster vhost -u DOMAIN|IP -w WORDLIST -t 100
```

## wfuzz

```bash
# directory mode
wfuzz -c -t 60 -w WORDLIST -u IP/FUZZ [-b COOKIE] [-d POST-DATA] [-H HEADER] [-z TYPE,PAYLOAD]

# vhosts mode
wfuzz -c -w WORDLIST -u DOMAIN -H "HOST: FUZZ.DOMAIN" [--hh ignore-errors-chars]

-c: show output in color
--hc: status code to ignore
--hw: word length to ignore
--hh: char length to ignore
--hl: line length to ignore
-z: alias for -z file,WORDLIST; can do -z range,1-100
```

## ffuf

```bash
ffuf -ic -w WORDLIST -e EXTENSION -u IP/FUZZ
-e Comma separated list of extensions. Extends FUZZ keyword.
-H header

# will use POST request
-d  'data'
```

## feroxbuster

```bash
feroxbuster -u IP -t 90 -x EXTENSIONS -w WORDLIST
```

##
