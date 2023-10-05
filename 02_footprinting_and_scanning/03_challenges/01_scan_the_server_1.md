# Scan the server 1

In this lab there are only two machines, one is yours (x.x.x.2) and the other one is the target (x.x.x.3). We can start by sending ICMP requests to the target to see if it is available and the perform a default nmap scan.

**Note**: When none of the 1000 most common ports is available, try scanning all ports or certain ranges to see if there are other ports open.

If there are some unusual ports open, nmap won't probably know what apps are running on those ports, proceed with a service enumeration scan to see what they are running.