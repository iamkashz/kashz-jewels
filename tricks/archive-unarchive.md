# archive, unarchive

## archive

```bash
zip FILE.zip FILE1 FIL2

tar -zcvf FILE.tar.gz DIR/
# -z: gzip file
# -v: verbose
# -c: create
# -f: file
```

## unarchive

```bash
unzip FILE.zip

gzip -d FILE.gz
gunzip FILE.gz

tar -zvxf FILE.tar.gz
# -z: gzip file
# -v: verbose
# -x: extract
# -f: file

7z x FILE
# x: extract
```
