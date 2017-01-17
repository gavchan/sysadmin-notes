# [Oracle Network Configuration](http://www.oracle.com/technetwork/articles/servers-storage-admin/s11-network-config-1632927.html)

- Oracle introduced `dladm` and `ipadm` to supersede `ifconfig`
- Changes made by `dladm` and `ipadm` persist across reboots.
- Also added automatic network configuration using network profiles.
- `netadm` and `netcfg` describe configuration of network related policies.
- `Automatic` NCP: uses DHCP to obtain basic network configuration
- `DefaultFixed` NCP: disables automatic network configuration and requires the network interfaces to be manually configured using `dladm` and `ipadm`.

- `dladm`: Data-link (layer 2) administration - links, VLANs, IP tunnels.

  - data-link names are given generic names and are no longer the same as physical interface.

- `ipadm`: Configures IP interfaces, IP addresses and TCP/IP properties.



# [Oracle Solaris 11.3 Network Documentation](http://docs.oracle.com/cd/E53394_01/index.html#group-4)

```
ifconfig -a
ifconfig net0
ifconfig net0 up
ifconfig net0 down

ping 192.168.x.x
ping -s 192.168.x.x

ping gateway_addr to check that network is working
traceroute url

netcfg
ifconfig
netadm
netdom
```
- Client, DHCP, IP/subnet/gateway, static IP
- Using traceroute;
- How to turn DHCP off?

```
ifconfig -a
ipadm         # Lists network cards, their class, state and address
netadm        # Enters interactive mode
netadm list   # Lists

netdom: command not found` # not a Solaris command.

netadm enable -p ncp Automatic          # Will enable DHCP
ipadm show-if                           # Display status of interface
ipadm show-addr                         # Display IP addresses of interfaces


# Configure a Static IP Address

netadm enable -p ncp DefaultFixed       # Will disable DHCP, allow manual config
dladm show-phys                         # Will display network devices
                                        # Status changed from up -> unknown
ipadm create-ip net0
ipadm show-if

# Add a persistent default route:
route -p add default 10.163.198.1       # Adds a default gateway
route -p show                           # Shows persistent route
```
# Name Service Configuration using SMF
# Use svc:/network/dns/client

https://docs.oracle.com/cd/E36784_01/html/E36831/dnsref-36.html
```
# svccfg -s system/name-service/switch
svc:/system/name-service/switch> setprop config/host = astring: "files dns"
svc:/system/name-service/switch:default> refresh
svc:/system/name-service/switch:default> quit
```
