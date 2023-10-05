# Scan the server 3

In this lab there are only two machines, one is yours (x.x.x.2) and the other one is the target (x.x.x.3). We can start by sending ICMP requests to the target to see if it is available.

In this case, starting with a regular nmap scan is a good options, but if nothing pops up, try a UDP scan on the most commonly used 1000 ports.

If you find something during the UDP scan, it's time for trying an agressive scan in that port.