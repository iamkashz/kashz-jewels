# office document analysis

Any file with extension `.docm, .xlsm` etc is a macro embedded file

* [zeltser.com/analyzing-malicious-documents/](https://zeltser.com/analyzing-malicious-documents/)

## .xlsm

Using oletools, we can extract macro.

```bash
python3 -m pip3 install oletools
olevba FILE.xlsm
```