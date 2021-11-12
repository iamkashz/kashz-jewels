# hashcat

* Path to rules: `/usr/share/hashcat/rules/*`
*

```bash
hashcat [-a <> ] -m MODE HASH.txt WORDLIST [-r RULE_FILE] [-w [1|2|3]] [-O]
# -w 3 gives a more tuned experience on your desktop, but it can also be slower.
#    1 to utilize more of your GPU.
#    2 Default
# -O: --optimized-kernel-enable, this limits the password length.
```

## Example Hashes

* [https://hashcat.net/wiki/doku.php?id=example:hashes](https://hashcat.net/wiki/doku.php?id=example:hashes)

```bash
hashcat --help | grep FORMAT
```