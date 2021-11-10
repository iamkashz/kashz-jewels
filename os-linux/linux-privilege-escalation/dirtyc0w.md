# dirtyc0w

Considering the number of boxes I've encountered that have used this, I've actually documented this.

```
# affects all versions since 2.6.22
# the vulnerability has been patched in kernel versions 4.8.3, 4.7.9, 4.4.26 and newer.
```

1. `/etc/passwd` based 
   1. Firefart: [FireFart/dirtycow/dirty.c](https://github.com/FireFart/dirtycow/blob/master/dirty.c)
   2. CPP: [gbonacini/CVE-2016-5195](https://github.com/gbonacini/CVE-2016-5195)
2. `SUID-based root`
   1. cowroot.c: [rverton/e9d4ff65d703a9084e85fa9df083c679](https://gist.github.com/rverton/e9d4ff65d703a9084e85fa9df083c679)

