# git commands

NOTE: if the folder is a git-repo, there should be a `.git` folder present.

## Git Commands

```bash
# preset config
git config --global user.email "kashz@kashz.com"
git config --global user.name "kashz"

# check history of commit
git log

# # diff commit check
git diff COMMIT^!
git diff COMMIT1 COMMIT2
git diff-tree -p COMMIT

# adding file to repo
git add FILE

# add new commit
git commit -m MESSAGE

# push update to repo
git push -u origin
```

## git commands using SSH

```bash
GIT_SSH_COMMAND='ssh -i id_rsa -o IdentitiesOnly=yes [-p PORT]' GIT COMMAND HERE

# git clone over ssh
GIT_SSH_COMMAND='ssh -i id_rsa -o IdentitiesOnly=yes [-p PORT]' git clone user@IP:/PATH-TO-GIT
```

## git-shell info

* [https://linux.die.net/man/1/git-shell](https://linux.die.net/man/1/git-shell)
* Restricted to only perform git-related commands
* Only four commands are permitted
    * git-receive-pack
    * git-upload-pack
    * git-upload-archive with a single required argument
    * cvs server (to invoke git-cvsserver).