# Quick-Tip-How-To-Dump-which-account-is-invoking-a-script
Just a quick PowerShell tip to remember the different ways to dump the user running a specific script

To try it, write these lines on a ```test.ps1``` quick script:

```powershell
Write-Host "Using .NET notation [Environment]::UserName" -ForegroundColor Yellow
([Environment]::UserDomainName + "\" + [Environment]::UserName) | out-file test.txt

Write-Host "Using Powershell $env system variable $env:username" -ForegroundColor magenta
"$env:userdomain\$env:username" | out-file -append test.txt

Write-Host "Using .NET notation with WindowsIdentity object [Security.Principal.WindowsIdentity]::GetCurrent().Name" -ForegroundColor green
[Security.Principal.WindowsIdentity]::GetCurrent().Name | out-file -append test.txt
notepad test.txt
```

And run it using the following from a ```cmd.exe``` shell:

```powershell
runas /user:domain\user "powershell e:\test.ps1"
```

# Credits

Credits for this tip comes to the awesome [Manoj aka "manojlds"](https://stackoverflow.com/users/526535/manojlds) from StackOverflow

[Link to the original StackOverflow post](https://stackoverflow.com/questions/7505792/powershell-find-the-user-who-invoked-the-script/7506450#7506450?newreg=64c9cda5a69a4bc485645ca0880419ff)
