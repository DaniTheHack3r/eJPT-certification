# Port Scanning & Enumeration with Nmap

+ Nmap is a free and open-source network scanner that can be used to discover hosts on a network as well as scan targets for open ports.

+ It can also be used to enumerate the services running on open ports as well as the operating system running on the target system.

+ We can output the results of our Nmap scan in to a format that can be imported into MSF for vulnerability detection and exploitation.


**Note**: Refer to `01_information_gathering > 02_active_information_gathering` to get a brief on nmap.

**Note**: To properly import the scans in to msf, we need to export the output of nmap as xml with the flag `-oX` and then the name of the file.