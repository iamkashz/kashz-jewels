# rsync

rsync is a utility for efficiently transferring and synchronizing files between a computer and an external hard drive

## Enumerate file-shares

```
$ nmap -sV --script "rsync-list-modules" -p 873 IP
rsync IP::
```

## Interesting Paths

```
 /etc/rsyncd.conf
 /etc/rsyncd.secrets
```

## List Directories

```
rsync IP::<share>
rsync -r IP::<
```

## Download

```
# file
rsync IP::<share>/<file> .

# dir
rsync -r IP::<share>/<dir>
```

## Upload

```
# file
rsync ./<file> IP::<share>/<dir>/

# dir
rsync -r ./<folder> IP::<share>/<dir>
```

{% embed url="https://www.netspi.com/blog/technical/network-penetration-testing/linux-hacking-case-studies-part-1-rsync/" %}
