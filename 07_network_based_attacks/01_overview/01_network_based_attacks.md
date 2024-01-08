# Network-Based Attacks

- As the name implies, it targets the network and the packages that travel through the network. Focuses on network protocols and services that are agnostic to the hosts operating system and how the could be exploited. For example:
    + ARP
    + DHCP
    + SMB
    + FTP
    + Telnet
    + SSH

- As we don't target the hosts directly, we usually focus on performing man in the middle attacks, also called on-path attacks. Where we eavesdrop a connection between two machines that are communicating with each other through a switch or hub. If we would be able to connect to a switch in a SPAN port, we could try to capture and analyze the whole traffic. However, that's not often the case, and the best option we have then, is to poison the target protocols and service.

## ARP Poisoning

- If we want to perform ARP poisoning, we will try to tell other machines that we are a certain MAC address, in other words, we will broadcast through ARP that we are a certain MAC address, spoofing it, so other machines will send us packages that are meant for another another host.

## Promiscous mode

- We could try to listen to all traffic in the network by setting the promiscous mode in a traffic packet analyzer in the case we are connected to a hub, so we can try to listen to the traffic that is not meant for us on the network.

## Technical DEMO

- In this case, the example takes place on kali environment where we are part of a network. We will start by performing a host discovery scan with nmap on the network we are connected to by running `nmap -sn $NETWORK_ADDRESS`.

- When we find the hosts, we can perform a regular service scan on the hosts we find.

- In one of the machines we can find a port 80 (http) open, so we can take a look at what it has exposed. We could also take a look at the port 443.

- For now, we will try to examine http and https traffic of the websites we found (in this case they are all bwasp). To examine the traffic we will fire up wireshark and listen to traffic. We can start by performing a nmap scan for host discovery and an agressive scan on each machine again and capture it with wireshark for analysis.

- We will stop the capture on wireshark and save it. So we can review it later. For now, let's play a bit with wireshark to get to know it.

**Note**: Check wireshark notes from previous courses on HTB so you can see all the functionalities associated with wireshark. I won't make annotations about how to use wireshark, as you should have learned how to use it.

**Note**: A nice trick is to put the source address and the source ip together, same for destination port, it is much more intuitive.

**Note**: There are more than 600.000 display filter expressions in wireshark. These templates help you build as quickly as possible display filters that will help you dive through any sort of network traffic.
