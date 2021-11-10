# rsync

rsync is a utility for efficiently transferring and synchronizing files between a computer and an external hard drive

## Enumerate file-shares

```bash
$ nmap -sV --script "rsync-list-modules" -p 873 IP
rsync IP::
```

## Interesting Paths

```bash
 /etc/rsyncd.conf
 /etc/rsyncd.secrets
```

## List Directories

```bash
rsync IP::<share>
rsync -r IP::<
```

## Download

```bash
# file
rsync IP::<share>/<file> .

# dir
rsync -r IP::<share>/<dir>
```

## Upload

```bash
# file
rsync ./<file> IP::<share>/<dir>/

# dir
rsync -r ./<folder> IP::<share>/<dir>
```

## Additional Reading

* [netspi.com/linux-hacking-case-studies-part-1-rsync/](https://www.netspi.com/blog/technical/network-penetration-testing/linux-hacking-case-studies-part-1-rsync/)
