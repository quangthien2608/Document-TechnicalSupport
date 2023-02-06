# Configure network windows with powershell

Gets IP network configuration.
```
Get-NetIPConfiguration
```

```diff
InterfaceAlias       : Wi-Fi
InterfaceIndex       : 3
InterfaceDescription : Qualcomm Atheros QCA9377 Wireless Network Adapter
NetProfile.Name      : LVS-3A 2
IPv4Address          : 192.168.64.193
IPv6DefaultGateway   :
IPv4DefaultGateway   : 192.168.64.1
DNSServer            : 1.1.1.1
                       8.8.8.8
```
---
Creates and configures an IP address. (with InterfaceIndex)
```
New-NetIPAddress -InterfaceIndex 3 -IPAddress 192.168.64.199 -AddressFamily IPv4 -PrefixLength 24 -DefaultGateway 192.168.64.1
```

Restart Adapter with name
```
Restart-NetAdapter -Name "Wi-Fi"
```
