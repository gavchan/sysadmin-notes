[Windows PowerShell cmdlets for Net TCP/IP](https://technet.microsoft.com/library/hh826150.aspx)

# View Network Configuration
```
Get-NetIPConfiguration
```
# View IP Addresses
```
Get-NetIPAddress
```

# Setting a static IP address
```
Get-NetIPInterface
```
- `ifIndex` displays value fo which you wish to set a static IP address.
```
New-NetIPAddress -InterfaceIndex 12 -IPAddress -192.0.2.2 - PrefixLength 24 -DefaultGateway -192.0.2.1
Set-DNSClientServerAddress -InterfaceIndex 12 -ServerAddresses 192.0.2.4,192.0.2.5
```

# Switching to use DHCP
```
Set-DnsClientServerAddress -InterfaceIndex 12 -ResetServerAddresses
```

# Determine current name of server
```
hostname
ipconfig
```

# Rename Server
```
Rename-Computer
```
