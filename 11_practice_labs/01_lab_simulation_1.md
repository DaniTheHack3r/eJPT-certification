# Lab Simulation 1

Original source:

https://www.youtube.com/watch?v=l6tHH2qQmQ8

Author notes:

https://github.com/PakCyberbot/eJPTv2-Notes/

## Notes

### Port Scanning & Vulnerability Scanning

- Testing every port is very important. Try to use searchsploit in every service version you find, it could lead to a potential exploitation path.

### Web enumeration

- Apache has a very interesting route where we can find important or sensible information: `/phpinfo.php`.

- Use dirb to scan for directories and routes in the webpage and check all routes for something interesting: `dirb $URL`.

- If wordpress found, use `wpscan`:
    + `wpscan -url $URL -e u`: enumerate users.
    + `wpscan -url $URL --passwords $PASSWORD_LIST`: Brute force password list.

- Web versioning enumeration: `whatweb $URL`.

### MySQL Enumeration

- You can connect to mysql with no password using `mysql -u $USERNAME -p -h $TARGET_IP`.

- You can use `mysql_login` module of metasploit to brute force mysql.

### SMB enumeration

- You can start by using nmap scripts to enumerate all things you can from smb.

- You can try to perform some more enumeration using smbclient.

- We can perform some more enumeration using rpcclient `rpcclient -U "" $TARGET_IP`.

- We can perform a little bit more of enumeration using enum4linux `enum4linux $TARGET_IP -A`, even if the target is windows, it can still perform some more basic enumeration on smb.

- We can use smbmap to extract a little bit more of information about smb `smbmap -H $TARGET_IP -u "" -p ""`.

- If hydra fails at the moment of trying smb brute forcing, try to use metasploit.

- Use psexec in order to get a proper shell using SMB.

### Hydra brute force attacks

- Before trying brute forcing services, try to use default username and passwords por every service, this could lead to the right credentials.

- Brute forcing attacks with hydra.
    + Wordpress brute force: `hydra -l $USERNAME -P $PASSWORD_LIST $TARGET_IP http-post-form '/path-to-wordpress-root-directory/wp-login.php:log=^USER^&pwd=^PASS^:S=302`. Note that in wordpress, the names log for user and pwd for password come from the wordpress html login page. If the redirection does not work in wordpress for any reason, and it returns an error message, the `:S=302` part of the command should be replaced with `:F=$ERROR_MESSAGE_RETURNED`.
    
    + Ssh brute force: `hydra -l $USERNAME -P $PASSWORD_LIST ssh://$TARGET_IP`. Consider that ssh could block you after a few tries if such policy is enabled.

    + Mysql brute force: `hydra -l $USERNAME -P $PASSWORD_LIST mysql://$TARGET_IP`.

- When trying to brute force a service, if the service is behind an IPS, it is probable that you are going to be considered an attack at some point. You could delay the hydra tasks or test with a short amount of credentials every time.

- Common wordlists:
    + `/usr/share/metasploit-framework/data/wordlists/unix_users.txt`
    + `/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`
    + `/usr/share/wordlists/rockyou.txt`

- When performing brute force, it is a good practice to wait for the brute force to end, as at any point it could give you a match. This could take a long time, so don't worry. However, try to enumerate all users first in order to narrow down the list.

### Local Enumeration in Linux (Post exploitation)

- Common enumeration commands:
    + `cat /etc/passwd`
    + `cat /etc/shadow`
    + `cat /etc/*issue`
    + `cat /etc/*release`
    + `uname -r`, `uname -a`
    + `whoami`
    + `crontab -l`
    + Check for binaries that can be executed using USID.
    + `sudo -l`
    + `ip a s` or `ifconfig` Consider checking for different segments of the network.

- Standard users usually have attached to them a regular `/bin/bash` shell in the `/etc/passwd` file.

- Web servers usually have their information at `/var/www/html/`.

### Local enumeration in Windows (Post exploitation)

- Common enumeration commands:
    + `net users`
    + `whoami /priv`
    + `query user`
    + `net user $USERNAME`
    + `net localgroup`
    + `net localgroup $GROUPNAME`
    + `hostname`
    + `systeminfo`. Useful to get some info about patches and hotfixes, and version of the system.
    + `ipconfig` Consider checking for different segments of the network.
    + `arp -a`

- When using meterpreter, is a good idea to migrate to lsass process and then trying to execute `hashdump`.


### Hashcat password cracking

- To run hashcat to crack a hash you need to know what mode to use, usually, the mode can be guessed from the first three characters of the hash, for example: $P$ will use the mode 400. MD5 will use the mode 0, and so on. Run `hashcat --example-hashes` to see examples of certain hashes and the mode.

### Pivoting (Post exploitation)

- From meterpreter you can run `run autoroute -s $OTHER_NETWORK_ADDRESS`.

- For port forwarding run from meterpreter `portfwd add -l $LOCAL_PORT -p $REMOTE_PORT -r $REMOTE_HOST`, with `portfwd list` you can see listed forwards.

### Bringing exploits from searchsploit

- When you find the desired exploit look at the right side of the table and take note of the number at the end of the path. Then run `searchsploit -m $NUMBER` and it will copy the exploit to the directory you are currently at.