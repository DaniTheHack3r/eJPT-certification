# Enumeration Notes

**Note**: Remember to ALWAYS execute the commands that brings help every time you use a new tool.

- It is a good idea to follow tracks when enumerating. At the end, you will not always know how to hack a machine, so, open your mind and try to follow documentation, deprecated methods, hacktricks, exploit-db, and gather all the information you can to then connect the points.

- If you get inital access during your recon/enumeration phase, don't look anywhere else, try to gather all the information you could from the exposed machine, you can check other technical details later.

- Local enumeration of the process running on a certain port on a linux machine will require a bit of expertise. Best options are to run `netstat -ano` and `ss -tl` or `ss -tln`. `ps aux` will help you enumerate other processes as well.

**Note**: SQL always needs ; at the of queries.

- Consider always looking for default passwords and users for a certain technology. They could be left as is after installation. If you are still unsure, try the following:

```
admin:password
admin:admin
root:root
root:password
admin:admin1
admin:password1
Administrator:"" (note an empty string)
```

**Note**: Take into consideration that when the login is empty, hydra throws only the login user without password attached to it.

- There is something important to take into consideration when trying to use mssqlclient.py (example command ahead) `python3 mssqlclient.py -port 1433 ARCHETYPE/sql_svc@10.129.135.110 -windows-auth`, when we want to use windows authentication, domain name and user name can be usually found as `ARCHETYPE\sql_svc`, but when using the impacket classes we need to use forward slash `ARCHETYPE/sql_svc` as impacket loves their forward slashes even on windows where domain names and usernames are always normally separated by a backslash. This applies for every tool on impacket.

- We can use burp suite in order to spider a website. It won't really brute force the website, it will crawl every page you browse to and extract any information it can use to recreate a site map of the website.

**Note**: Burp suite works as a proxy that listens on your localhost on port 8080.

- We could try to bruteforce the ids and roles of a specific user. However, that requires too much time and effort. We can always try to start by performing a simple enumeration of queries, ids, requests sent, etc.

- We can speed up the scan using the command: `export ports=$(nmap -p- --min-rate=1000 -T4 --open $TARGET_IP | grep -e "^[0-9]" | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)` which will give you only the ports in the format `x,y,z` which can be passed as argument for a more complex scan: `nmap -sC -sV -p$ports $target_ip`.