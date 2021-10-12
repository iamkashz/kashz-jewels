# file modification

## regex

[Cheatsheet](https://cheatography.com/davechild/cheat-sheets/regular-expressions/)

```bash
(\s){2,}: 2 or more spaces
```

## sed

```bash
sed -i '/<SEARCH>/<REPLACE>/g' file
# -i: make changes in file
# -e: show output in terminal
# SEARCH: escape using '\'
# REPLACE: no escape
```

## cut

```bash
# using cut
cut -d DELIMITER -f FIELD

# to remove first string from text
cut -c2-
```

## awk

```bash
# TODO
```
