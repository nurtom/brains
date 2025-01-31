## find a process having a port open

```powershell
Get-Process -Id (Get-NetTCPConnection -LocalPort YourPortNumberHere).OwningProcess
```

## Kill process with given pid

```powershell
taskkill.exe /PID 5988 /F
```