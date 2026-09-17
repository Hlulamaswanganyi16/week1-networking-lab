# Networking Fundamentals — Hands-On Log

Part of my self-directed Cloud Security Engineer study path.
Week 1 focus: core networking concepts, tested hands-on rather than just read.

## What I did

- Tested connectivity using `ping -c 4 8.8.8.8` (direct IP) and `ping -c 4 google.com` (domain name)
- Compared the two tests to understand the practical difference between reaching a device by IP versus by domain name, and where DNS fits in
- Studied and practiced explaining: switches, routers, ARP, DHCP, DNS, HTTP/HTTPS, NAT, VPNs, firewalls, encapsulation, and the OSI/TCP-IP models
- Set up a WSL2 (Ubuntu) Linux environment on Windows 11 as my hands-on lab, and diagnosed a real networking fault in the process

## What broke, and how I fixed it

**Problem — WSL2 had no internet access at all**
`sudo apt update` failed with "Network is unreachable," and `ping` to raw IP addresses showed 100% packet loss — even though Windows itself had full internet access.

**Diagnosis:** Used `Get-NetConnectionProfile` in PowerShell to confirm the real network adapter was healthy (`IPv4Connectivity: Internet`), which proved the fault was isolated to WSL's internal virtual network, not the actual internet connection.

**Fix:** Created a `.wslconfig` file in the Windows user folder with:
