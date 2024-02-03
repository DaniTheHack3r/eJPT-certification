# SSH Enumeration

+ SSH (Secure Shell) is a remote administration protocol that offers encryption and is the successor to Telnet.

+ It is typically used for remote access to servers and systems.

+ SSH uses TCP port 22 by default, however, like other services, it can be configured to use any other open TCP port.

+ We can utilize auxiliary modules to enumerate the version of SSH running on the target as well as perform brute-force attacks to identify passwords that can consequently provide us remote access to a target.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it SSH_Enum for this example.

- Set globally the target IP with `setg RHOSTS $TARGET_IP`, do this for the RHOST option as well.

- We will start by performing ssh version enumeration with `auxiliary/scanner/ssh/ssh_version`.

- Now we will try to perform some brute force attack using the module `auxiliary/scanner/ssh/ssh_login`. Recommended lists are `/usr/share/metasploit-framework/data/wordlists/common_users.txt` and `/usr/share/metasploit-framework/data/wordlists/common_passwords.txt`.

**Note**: If the ssh server is configure to work with public key, we could use the module `auxiliary/scanner/ssh/ssh_login_pubkey`.

**Note**: Ssh logs are usually sent to a syslog server, so trying to brute force ssh could trigger some alarms, be careful when using ssh_login modules.

- After having brute forced your way into the ssh login, we will see that the module directly stablished a session. We could access it using `sessions` commands. This will save the credentials as well, could be useful in order to establish persistance.

- Now we can narrow down the brute force trying to enumerate users using the `auxiliary/scanner/ssh/ssh_enumusers`.
