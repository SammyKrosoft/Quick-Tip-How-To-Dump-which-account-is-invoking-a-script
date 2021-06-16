# Quick-Tip-How-To-Dump-which-account-is-invoking-a-script
Just a quick PowerShell tip to remember the different ways to dump the user running a specific script

To try it, write these lines on a ```c:\temp\test.ps1``` (choose the path and file name you want) quick script:

```powershell
Write-Host "Using .NET notation [Environment]::UserName" -ForegroundColor Yellow
([Environment]::UserDomainName + "\" + [Environment]::UserName) | out-host

Write-Host "Using Powershell $env system variable $env:username" -ForegroundColor magenta
"$env:userdomain\$env:username" | out-host

Write-Host "Using .NET notation with WindowsIdentity object [Security.Principal.WindowsIdentity]::GetCurrent().Name" -ForegroundColor green
[Security.Principal.WindowsIdentity]::GetCurrent().Name | out-host
```

And run it using the following from either a ```cmd.exe``` shell or a Powershell window:

```powershell
runas /user:ComputerName\UserName "powershell -noexit -command c:\temp\test.ps1"
```

![image](https://user-images.githubusercontent.com/33433229/122291820-423a6580-cec3-11eb-921b-f207fb47365d.png)

You'll have a new window opening that will look like this:

![image](https://user-images.githubusercontent.com/33433229/122291863-541c0880-cec3-11eb-9a29-0ae5fc93db93.png)



# Credits

Credits for this tip comes to the awesome [Manoj aka "manojlds"](https://stackoverflow.com/users/526535/manojlds) from StackOverflow, thank you so much for this Manoj :pray:

[Link to the original StackOverflow post](https://stackoverflow.com/questions/7505792/powershell-find-the-user-who-invoked-the-script/7506450#7506450?newreg=64c9cda5a69a4bc485645ca0880419ff)
