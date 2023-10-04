# DNS Zone Transfer

This is related to how dns and dns server works and how they can be abused.

## DNS

- Domain Name System (DNS) is a protocol that is used to resolve domain names/hostnames to IP addresses.
- During the early days of the internet, users would have to remember the IP addresses of the sites they wanted to visit, DNS resolves this issue by mapping domain names (easier to recall) to their respective IP addresses.
- A DNS server (nameserver) is like a telephone directory that contains domain names and their corresponding IP addresses.
- A plethora of public DNS servers have been set up by companies like Cloudflare (1.1.1.1) and Google (8.8.8.8). These DNS servers contain the records of almost all domains on the internet.

## DNS Records

- A => IPv4 addresses.
- AAAA => IPv6 addresses.
- NS => Reference to the domain's nameserver.
- MX => Resolves a domain to a mail server.
- CNAME => Used for domain aliases.
- TXT => Text record.
- HINFO => Host information.
- SOA => Domain authority.
- SRV => Service records.
- PTR => Resolves an IP address to a hostname.

## DNS Interrogation

DNS interrogation is an active Reconnaissance technique.

- DNS interrogation is the process of enumerating DNS records for a specific domain.
- The objective of DNS interrogation is to probe a DNS server to provide us with DNS records for a specific domain.
- This process can provide with important information like the IP address of a domain, subdomains, mail server addresses, etc.

The main difference with passive techniques, such as using dnsdumpster, is that we can find much more relevant information related to domain using DNS interrogation like records that we didn't have access previously.

## DNS Zone Transfer

- In certain cases DNS server admins may want to copy or transfer zone files from one DNS to another. This process is known as a zone transfer.
- If misconfigured and left unsecured, this funcitonality can be abused by attackers to copy the zone file from the primary DNS server to another DNS server.
- A DNS Zone transfer can provide penetration testers with a holistic view of an organization's network layout.
- Furthermore, in certain cases, internal network addresses may be found on an organization's DNS servers.

**Note**: Zone files are the files with all records of the domain in the nameserver.

**Note**: zonetransfer.me is a website specifically made to teach others about zone transfers.

**Note**: There is another dns enumeration tool which is **dnsenum**, this tool performs active reconnainssance so it is different from **dnsrecon** or **dnsdumpster**. It can also perform zone transfer automatically and dns bruteforce to find different records like subdomains.

**Note**: hosts file is the one responsible of storing locally mapped domain names. This is the first source of information the dns client will fetch in your computer.

**Note**: Performing a DNS zonetransfer.me with **dig** is a little bit easier and better in some cases, because dnsenum can't be controlled completely, and it will perform dns bruteforce every time you run it.

**Note**: there is another utility called **fierce**. This tool can be used to perform dns enumeration as well. It is a semi-lightweight scanner that helps locate non-contiguous IP space and hostnames against specified domains. It looks up for domains inside and outside corporate networks and it is meant as a precursos of **nmap**, **unicornscan**, **nessus**, **nikto**, etc.