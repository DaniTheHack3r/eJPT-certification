# Dumping Linux password Hashes

- Linux has multi-user support and as a result, multiple users can access the system simultaneously. This can be seen as both an advantage and disadvantage from a security perspective, in that, multiple accounts offer multiple access vectors for attackers and therefore increase the overall risk of the server.

- All of the information for all accounts on Linux is stored in the passwd file located in: /etc/passwd.

- We cannot view the passwords for the users in the passwd file because they are encrypted and the passwd file is readable by any user on the system.

- All the encrypted passwords for the users are stored in the shadow file. it can be found in the following directory: /etc/shadow.

- The shadow file can only be accessed and read by the root account, this is a very important security feature as it prevents other accounts on the system from accessing the hashed passwords.

- The passwd file gives us information in regards to the hashing algorithm that is being used and the password hash, this is very helpful as we are able to determine the type of hashing algorithm that is being used and its strength. We can determine this by looking at the number after the username encapsulated by the dollar symbol ($):
    + $1 -> MD5
    + $2 -> Blowfish
    + $5 -> SHA-256
    + $6 -> SHA-512

**Note**: Most modern linux distribution use the strongest hashing algorith which is SHA-512.

## Laboratory

In this laboratory you won't be provided with the target IP address, but you can take your own IP address in the subnet and use the machine in the next ip address. For example x.x.x.2 is your machine and x.x.x.3 is the target.

- Start by performing an nmap scan with service detection. You should see the ftp port 21 open and the ProFTPD version 1.3.3c running on that port. This version is indeed vulnerable and an exploit is available in metasploit. We can confirm this by performing a quick search in searchsploit.

- Now startup the msfconsole, and use the corresponding module to exploit ProFTPD 1.3.3c. This particular exploit should give us elevated privileges right away.

**Note**: In linux, if you active the shell from meterpreter or inject a backdoor that will get you a sh shell, remember to run `/bin/bash -i` to start a bash shell.

- Now put the session in the background by pression ctrl+z and you will see it in the msfconsole by running `sessions`. After that, you can upgrade the session to a meterpreter session by running `sessions -u $SESSION_ID`. Once created, move to the meterpreter session running `sessions $SESSION_ID`.

**Note**: you could get an error when upgrading to a meterpreter session, but it's fine if the session gets updated anyway.

**Note**: The session is not updated per se, msfconsole will just start up up another session running meterpreter.

- Once in meterpreter, check if you have privileged access by running `getuid`. UID 0 means you are the root user. After that, just cat the contents of the `/etc/shadow` file. You should see the root user and a bunch of service accounts.

**Note**: Service accounts don't have password hashes as they don't need them.

- Aside from just catting the contents of the shadow file, we can also use that hashdump module, which is a post exploitation module in msfconsole called `post/linux/gather/hashdump`.

**Note**: The module will directly unshadow the hash, that is, it will format the hash so ready to be cracked.

Cracked root password: password
