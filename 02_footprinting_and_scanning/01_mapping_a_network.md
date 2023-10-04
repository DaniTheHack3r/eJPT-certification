# Mapping a network

## Purpose

- Scope: You will define what will provide value to your clients without interfering with their production environment or their business.
- Discovery: The main idea in the end is to clear out war fog, define perimeters, zones, network layouts, targets, etc.

## Process

- Physical Acess: Sometimes you will need to get access to the premises so you will have to bypass Physical Security in order to get access to the network, or probably use OSINT to get some ip addresses or perform Social Engineering to make someone to tell you how to access.
- Sniffing: When having access to the network, you could perform some sniffing using tcpdump or wireshark to see the normal network traffic. See regular websites, server downloads/uploads, spot ip addresses, MAC addresses for further enumeration.
- ARP: We are going to take advantage of Address Resolution Protocol (RFC 826), it resolves ip to MAC addresses in a local network. ARP is usually enabled, and we can abuse ARP to find out all hosts on the network easily. It could still be disabled and everything setup manually which is really weird. In that case we could relay in ping or ICMP packages.
- ICMP: Internet Control Message Protocol (RFC 792) is a protocol for diagnosing network connectivity issues. For sending ICMP packages and understanding how the network is setup we have Traceroute and for check health or existance of a target we have the ping utility, however, ICMP replies might be disabled by default in some systems like windows hosts.

## Tools

- Wireshark
- ARP-Scan
- Ping
- Fping
- Nmap
- Zenmap
