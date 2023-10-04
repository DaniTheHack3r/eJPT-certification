# Port Scanning with nmap

For this lesson we are going to follow along a lab, notes and lessons learned will be displayed below.

**Note**: When a host is running windows, most probably is running windows firewall. This firewall has the configuration set to block all ICMP (ping) packets. In that case we can avoid the process ping using the flag `-Pn`.

**Note**: By the reading of the output of nmap alone we could determine what operative system or programs the target host is running. However, nmap can be used to detect operative systems as well.

**Note**: nmap is very versatile, and can be used to scan one single port, different ports at a time or a full range of ports. We can take advantage of this by using the flag `-p`.

**Note**: The state of the port could be open, close or filtered. Filtered is the most unreliable as it could mean it is behind a firewall or that the port is totally shut down.

**Note**: nmap scan can be narrowed down to only 100 of the most used ports with the flag `-F`.

**Note**: We can tell nmap to scan for udp ports using the flag `-sU` and tcp with `-sT`. It is usually recommended to perform a UDP scan as some services might be running in UDP like DNS.

**Note**: We can increase the verbosity of the scan by passing the flag -v to the nmap scan.

**Note**: Sometimes we want to perform a service version scan for each port, and can be done using the `-sV` flag. Service detection can increase the time nmap takes to perform the scan. This could be really important because we could try to look up for known vulnerabilities for current versions of any service exposed by the machine. To perform an Operative System detection we can use `-O` flag.

**Note**: We can enumerate more information about open ports using the default nmap script scan with the flag `-sC`. It will run a list of nmap scripts on the ports that are currently open. This type of scan can take some time to complete as it needs to run some more processes in the open ports before finishing.

**Note**: We can specify an agressive scan with nmap using `-A` that combines `-sC`, `-sV` and `-O` in one.

**Note**: nmap also provide some time templates, in order to slow down or speed up the scan. Using the flags from `-T0` to `-T5`. The higher the number, the faster the scan. In certain cases you will want to slow down the scan if there's a supect of a detection system in the network, or you might want to speed it up if you need it to be completed as fast as possible. Nmap will automatically choose a time template based on the network architecture present, but it can always be override.

**Note**: It is important to be careful with time templates as higher velocities could potentially lead to a denial of service in a production environment to routers and switches.

**Note**: You can write all your outputs of the scan in three different formats. You can use the normal format with `-oN` (as plain text) or to XML with `-oX`, that can be input in some frameworks like metasploit.

**Conclusion**: This type of scan is not always conclusive, we are just making some reconnaissance, we still need to clear things out during the enumeration phase that comes after the recon phase.