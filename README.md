# disable-defender
Disabling Windows Defender Permanently using Registry Keys


> [!NOTE]
> A system restore point is recommended before you run the script.


## Disable or Remove Windows Defender *Application Guard Policies* (advanced)

If you have any problems when opening an app (*extremely rare*) and get the message "The app can not run because Device Guard" or "Windows Defender Application Guard Blocked this app", you have to remove 4 files with the same name, from different locations.


- In EFI Partition

```PowerShell
Remove-Item -LiteralPath "$((Get-Partition | ? IsSystem).AccessPaths[0])Microsoft\Boot\WiSiPolicy.p7b"
```

- In Code Integrity Folder

```PowerShell
Remove-Item -LiteralPath "$env:windir\System32\CodeIntegrity\WiSiPolicy.p7b"
```

- In Windows Folder

```PowerShell
Remove-Item -LiteralPath "$env:windir\Boot\EFI\wisipolicy.p7b"
```

- In WinSxS Folder

```PowerShell
Remove-Item -Path "$env:windir\WinSxS" -Include *winsipolicy.p7b* -Recurse
```