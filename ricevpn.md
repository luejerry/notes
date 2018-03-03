# Connecting to Rice VPN on Linux

1. Download RiceNet.pcf file from KB
2. Make sure `vpnc` is installed on Linux
3. Use `pcf2vpnc` to convert the file:

```
pcf2vpnc RiceNet.pcf /etc/vpnc/RiceNet.conf
```

4. Run `vpnc` and login using netID

```
vpnc RiceNet
```
