# subversion snv :3690

svn is a type of version control; used to maintain current and historical version of projects.

## SVN Commands

```bash
# list
svn ls svn://IP

# commit history
svn log svn://IP

# download repo
svn checkout svn://IP | svn co svn://IP

# checkout different revision
svn up -r REV#

# differences between repo version
svn diff -c COMMIT#
```
