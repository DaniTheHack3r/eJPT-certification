# Nmap Host Discovery

We don't always have to use nmap to discover or probe hosts, we can start using ping or arp-scan, if no response is receive, we could try using nmap with `-Pn` to get some more information about the host.

After getting some information from the host, we can target specific hosts using the `-p` and enumerate more info with `-sV` and `-O` like this: `nmap 10.3.26.13 -Pn -p 80,135,139,445,3389,49154,49155 -sV -O`.