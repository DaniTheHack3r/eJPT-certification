# Host discovery with nmap

With nmap you can do a ping sweep against a local network in order to perform host discovery. First you will need to get your local ip address and with it the netmask and network address, you can use `ip a s` to get that information.

## NMAP probing

Nmap stands for networkmapper, it is used to quickly scan networks and target specific hosts to perform port scan. If you get your current network, you can perform a quick host discovery with the `-sn` flag like this: `sudo nmap -sn 192.168.0.0/24`. Nmap send ICMP packages (PING) to discover hosts in the network.

**Note**: Some hosts disable ICMP packages, so nmap won't guarantee that all hosts shown are all the hosts in the network, unless a deep scan is performed.

## Netdiscover

There is another tool called netdiscover, it comes prepackaged with kali linux, but if that's not the case you can still install it through **apt**. The main difference with nmap is that it uses a different technology to perform host discovery which is **ARP**.