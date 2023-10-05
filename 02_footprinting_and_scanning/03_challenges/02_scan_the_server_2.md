# Scan the server 2

In this lab there are only two machines, one is yours (x.x.x.2) and the other one is the target (x.x.x.3). We can start by sending ICMP requests to the target to see if it is available. In this case the target has some services running in the first 250 ports, but those services are not in their usual ports so further enumeration must be performed.

**Note**: Nmap by default executes a tcp scan. However, sometimes services might be using udp ports and in that case, check for some more open ports with UDP just to be sure.

**Note**: Take into consideration that UDP scans take much longer.

Sometimes, service enumeration using `-sV` is not enough and the port could be filtered that way. Try using `-sC` in the port to gain some more info about it. If needed, you can force only discovery scripts with `--script=discovery`.

**Note**: For this lab it was pretty difficult to get something from the port 134. The other two ports gave us good information, 177 was DNS and 234 was SNMP. We know that serving remaining is tfpt (this sort of information is not always known), as a last resort, we can try to establish a connection between your host and the server with the correspoding utility, in this case tftp from the terminal.