# git shell

## info

```bash
https://linux.die.net/man/1/git-shell
# retricted to only perform git-related commands
only four commands are permitted: git-receive-pack git-upload-pack and git-upload-archive with a single required argument, or cvs server (to invoke git-cvsserver).
```

## git-shell commands using SSH

```bash
GIT_SSH_COMMAND='ssh -i id_rsa -o IdentitiesOnly=yes [-p PORT]' GIT COMMAND HERE

# git clone over ssh
GIT_SSH_COMMAND='ssh -i id_rsa -o IdentitiesOnly=yes [-p PORT]' git clone user@IP:/PATH-TO-GIT
```
