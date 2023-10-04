# Subdomain enumeration with Sublist3r

Subdomain enumeration with Sublist3r is a passive technique to collect sub domain information from publicly available sources.

Sublist3r (https://github.com/aboul3la/Sublist3r) uses OSINT to enumerate all that information. It also includes Netcraft, Virustotal, ThreatCrowd, DNSdumpster and ReverseDNS.

It also integrates subbrute to increase the possibility of finding more subdomains using bruteforce with an improved wordlist. However, that would be not passive recon.

Sublist3r can fetch information from different sources, and it could get information from subdomains that were available and now they are not, or even subdomains that are not public anymore.

**Note**: it might not work sometimes, because some sources could be blocking your requests as they sometimes setup a request limit.
