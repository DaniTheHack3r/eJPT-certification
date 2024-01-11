# ARP Poisoning

- Let's start by scanning the network to find some hosts.

- Now we will open Wireshark to start listening in the current ethernet adapter. In this laboratory should be eth1.

- In this case we need to activate the ip_forward option in linux. For that, set to 1 the value of the file `/proc/sys/net/ipv4/ip_forward`.

- Now we will run arpspoof to pretend to be someone else and redirect that traffic to the original receiver of the traffic. That way we can listen to that traffic unnoticed `arpspoof -i eth1 -t x.x.x.37 -r x.x.x.36` In this case we are receiving packages from the .36 machine that are meant to be sent to the .37 machine for this laboratory.

- If we take a look at the packet capture, we can notice that there is some telnet traffic. We can listen to this telnet traffic without issue and should be sufficient to capture some information that could be privileged and useful for us.

**Note**: Take into consideration that in internal networks, many times the traffic runs unencrypted, which makes it easy to get plain text credential from that traffic.
