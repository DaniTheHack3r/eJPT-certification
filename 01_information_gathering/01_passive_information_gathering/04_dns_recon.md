# DNS Recon

This kind of recon usually targets websites where DNS always come to play. During this recon we want to identify A records, CNAME, TXT records, ip addresses, mail servers, etc.

## Tools

One of the first utilities that comes handy is **DNSRecon** (https://github.com/darkoperator/dnsrecon) utility for Kali Linux. It is a python script that the ability to check all records for zone transfers. Enumerate General DNS Records for a given Domain (MX, SOA, NS, A, AAAA, SPF and TXT). Perofrm common SRV Record Enumeration. Top Level Domain (TLD) expansion.

It comes packaged with kali linux so we don't need to install it.

**Note**: Cloudflare doesn't hide MX record very well, so it could be something we could exploit.

Another recommended tool is **DNSDumpster** (https://dnsdumpster.com) it is a website that can be used to perform dns recon and research, find and lookup dns records. It is pretty similar to what dnsrecon does but it arrange information in a more readable way, including ordered information by sections and graphs.