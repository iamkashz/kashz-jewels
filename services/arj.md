# arj

## help

```bash
$ /usr/bin/arj
ARJ32 v 3.10, Copyright (c) 1998-2004, ARJ Software Russia.

List of frequently used commands and switches.  Type ARJ -? for more help.
Usage:     ARJ <command> [-<sw> [-<sw>...]] <archive_name> [<file_names>...]
Examples:  ARJ a -e archive, ARJ e archive, ARJ l archive *.doc
<Commands>
 ac: Add Chapter to chapter archive     l: List contents of archive
  a: Add files to archive               m: Move files to archive
  c: Comment archive files              t: Test integrity of archive
  d: Delete files from archive          u: Update files to archive
  e: Extract files from archive         v: Verbosely list contents of archive
  f: Freshen files in archive           x: eXtract files with full pathname
<Switches>
  c: skip time-stamp Check              r: Recurse subdirectories
  e: Exclude paths from names           u: Update files (new and newer)
  f: Freshen existing files             v: enable multiple Volumes
  g: Garble with password               w: assign Work directory
  i: with no progress Indicator         x: eXclude selected files
  m: with Method 0, 1, 2, 3, 4          y: assume Yes on all queries
  n: only New files (not exist)        hk: enable ARJ-PROTECT damage protection
```

## SUID exploit

```bash
# create archive
arj a <file.arj-to-create> <file-to-add-to-archive>

# test archive
arj l <file.arj>

# extract archive
# will extract in current dir
arj e <file.arj>
# extract in specified dir
arj x <file.arj> <path-to-extract-to>
```
