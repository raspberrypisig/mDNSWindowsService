# mDNS Windows 10 Service

This simple Golang program is installed as a Windows 10 Service.

It's goal is to respond to mDNS queries for the Windows 10 machine. 

If the hostname of the Windows machine is ABC, then this will allow ABC.local to be resolved to the IP address of the machine.

# Build

```
go build .
```

# Install Service

Open CMD with admin privileges and run

```
mdnsmohanservice.exe -service install
```

# Uninstall Service

Open CMD with admin privileges and run

```
mdnsmohanservice.exe -service uninstall
```

# mDNS/avahi/bonjour/zeroconf

Windows 10 can be a pain to get mDNS working properly. Here are the steps I took, many of the steps
may not be necessary, but I put here for completeness.

1. Firewall
   mdns uses multicast address, so if you have firewall and switches, you need to enable multicast traffic through.

2. Turn off the Link Local Multicast Name Resolution (LLMNR)
   Windows 10 has another method for service discovery, but it interferes with mDNS, so it must be disabled. This can be done via group policy( Computer Configuration\Administrative Templates\Network\DNS Client\Turn off Multicast Name Resolution) or regedit(HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows NT\DNSClient\ set EnableMulticast to 0)

3. Install WinPCap (https://www.winpcap.org/install/default.htm). Without this steps, I wasn't able to
   get multicast traffic to appear on the machine.