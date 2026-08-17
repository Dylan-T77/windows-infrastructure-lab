# Windows Command Reference

A practical quick-reference for Command Prompt (`cmd.exe`) and built-in Windows administration tools.

## System Information

```cmd
systeminfo
hostname
whoami
whoami /all
ver
```

## Network Configuration

```cmd
ipconfig
ipconfig /all
ipconfig /release
ipconfig /renew
ipconfig /flushdns
route print
arp -a
getmac
```

## Connectivity and DNS

```cmd
ping <host>
tracert <host>
pathping <host>
nslookup <hostname>
```

## Ports and Connections

```cmd
netstat -ano
netstat -ano | findstr :443
```

Map a PID to a process:

```cmd
tasklist /FI "PID eq <PID>"
```

## Processes and Services

```cmd
tasklist
taskkill /PID <PID> /F
sc query
sc query <service>
sc start <service>
sc stop <service>
```

## Files and Directories

```cmd
dir
cd <path>
mkdir <directory>
copy <source> <destination>
move <source> <destination>
del <file>
rmdir /s <directory>
```

## Users

```cmd
whoami
net user
net user <username>
net user <username> *
net localgroup
net localgroup <group>
```

## Windows Firewall

```cmd
netsh advfirewall show allprofiles
netsh advfirewall firewall show rule name=all
```

## Event Logs

```cmd
wevtutil el
wevtutil qe System /c:20 /f:text
wevtutil qe Application /c:20 /f:text
```

## Active Directory / Domain Troubleshooting

```cmd
whoami /fqdn
nltest /dsgetdc:<domain>
nltest /dclist:<domain>
gpupdate /force
gpresult /r
```

## System File Checks

```cmd
sfc /scannow
DISM /Online /Cleanup-Image /CheckHealth
DISM /Online /Cleanup-Image /ScanHealth
DISM /Online /Cleanup-Image /RestoreHealth
```

## Useful Diagnostics

```cmd
hostname
ipconfig /all
route print
nslookup <hostname>
ping <gateway>
ping <server>
tracert <host>
netstat -ano
```
