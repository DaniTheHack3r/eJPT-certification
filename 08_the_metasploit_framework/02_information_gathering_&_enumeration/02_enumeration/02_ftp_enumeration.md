# FTP Enumeration

+ FTP (File Transfer Protocol) is a protocol that uses TCP port 21 and is used to facilitate file sharing between a server and client/clients.

+ It is also frequently used as a means of transferring files to and from the directory of a web server.

+ We can use multiple auxiliary modules to enumerate information as well as perform brute-force attacks on targets running an FTP server.

+ FTP authentication utilizes a username and password combination, however, in some cases an improperly configured FTP server can be logged into anonymously.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it FTP_ENUM for this example.

- We will start by performing a simple port scan to see if the target is currently running ftp.

- To search for auxiliary modules for ftp enumeration, we will use the command `search type:auxiliary name:ftp`, note we are filtering by type and name in this case.

- We will start using the `auxiliary/scanner/ftp/ftp_version` module in ftp. The result should be ProFTPD 1.3.5a.

**Note**: We can try to look for exploits in ProFTPD 1.3.5a, but it doesn't have more than 1 exploit that could not work by the time this is being written.

- Next we are going to use the `auxiliary/scanner/ftp/ftp_login` auxiliary module in ftp. Depending on the information we have, we can pass many options: PASSWORD, PASS_FILE, USERNAME, USER_FILE, USERPASS_FILE. We can combine different options in order to test 1 password for many accounts or 1 account with many passwords. Besides that, we must set the RHOSTS, and we can change the bruteforce speed. The credentials obtained can be used to connect to the ftp server.

**Note**: Recommended lists are: `/usr/share/metasploit-framework/data/wordlists/common_users.txt` and `/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`.

**Note**: When performing a bruteforce attack, we could take down the server by accident, causing a DOS attack before even realizing.

- Now we are going to use the `auxiliary/scanner/ftp/anonymous` module in ftp. We only need to set the RHOSTS option and run it. If not output is present when the module completed execution, you are certain the anonymous connection is disabled on that server.

- Connect to FTP and inspect the secrets.

Flag: 260ca9dd8a4577fc00b7bd5810298076
