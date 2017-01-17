# Netsh Commands for Windows Firewall with Advanced Security
- Not recommended as the `netsh advfirewall` context may be removed in the future.
- https://technet.microsoft.com/library/cc771920(v=ws.10)
```
netsh advfirewall firewall
```

# Background
[Windows Server 2012 R2: Windows Firewall with Advanced Security Overview](https://technet.microsoft.com/en-us/library/hh831365.aspx)

[Windows Firewall with Advanced Security Administration with Powershell](https://technet.microsoft.com/library/hh831755.aspx)

# Enable Windows Firewall
Powershell
```Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled True
```
Netsh
```netsh advfirewall set allprofiles state on
```

# Control Firewall behaviour
Powershell
```Set-NetFirewallProfile -DefaultInboundAction Block -DefaultOutboundAction Allow -NotifyOnListen True -AllowUnicastResponseToMulticast True -LogFileName %SystemRoot%\System32\LogFiles\Firewall\pfirewall.log
```
Netsh
```
netsh advfirewall set allprofiles firewallpolicy blockinbound,allowoutbound
netsh advfirewall set allprofiles settings inboundusernotification enable
netsh advfirewall set allprofiles settings unicastresponsetomulticast enable
netsh advfirewall set allprofiles logging filename %SystemRoot%\System32\LogFiles\Firewall\pfirewall.log
```

...
