# SMB Dictionary Attack

Sometimes, null (anonymous) sessions are ok when enumerating information out of a smb server. But sometimes we need to authenticate and we don't have any credentials and that's when dictionary attacks come to play. 

1. What is the password of user “jane” required to access share “jane”? Use smb_login metasploit module with password wordlist `/usr/share/wordlists/metasploit/unix_passwords.txt`

- for this task we will use `scanner/smb/smb_login` module to perform a dictionary attack. Set up the target smb server, the target username (previously enumerated) and a wordlist.
- Jane password is: `abc123`.

2. What is the password of user “admin” required to access share “admin”? Use hydra with password wordlist: /usr/share/wordlists/rockyou.txt

- Before using it, make sure rockyou.txt is decompressed.
- Hydra is a very powerful tool when performing dictionary attacks. Use the following syntax for this case: `hydra -l admin -P /path/to/wordlist x.x.x.x <protocol>`.

3. Which share is read only? Use smbmap with credentials obtained in question 2.

- We can do it just like this: `smbmap -H x.x.x.x -u admin -p password1`. The read only share is nancy.

4. Is share “jane” browseable? Use credentials obtained from the 1st question.

- To figure out if any of the share are browsable we can use smbclient like this: `smbclient -L x.x.x.x -U <user>`.
- It seems none of them are browsable by jane, even jane's share. However, try connecting using `smbclient //x.x.x.x/path/to/share -U <user>` because sometimes they are not visible even if they are accesible.
- Jane's share is accesible.

5. Fetch the flag from share “admin”

- Now let's try the same with the admin share.
- A tar.gz file with the flag is available. Fetch it.

6. List the named pipes available over SMB on the samba server? Use  pipe_auditor metasploit module with credentials obtained from question 2.

- SMB is a protocol that can be used by different services, and the way the connect to another is through pipes. Named pipes are pipes that are known. There's a chance to get other services and not only smb if we know the name of the pipes.
- Use the auxiliary module `scanner/smb/pipe_auditor` and set user, pass and target host.
- Available Pipes: \netlogon, \lsarpc, \samr, \eventlog, \InitShutdown, \ntsvcs, \srvsvc, \wkssvc.

**Note**: We don't have to know what the names of the pipes mean or how to use them, but enumerating them is very important so we could use them later.

7. List SID of Unix users shawn, jane, nancy and admin respectively by performing RID cycling  using enum4Linux with credentials obtained in question 2.

- To get SIDs we will use enum4linux like this: `enum4linux -r -u "admin" -p "password1" x.x.x.x`. `-r` ensures we are looking for users.
- the SIDs are:
S-1-22-1-1000 Unix User\shawn
S-1-22-1-1001 Unix User\jane
S-1-22-1-1002 Unix User\nancy
S-1-22-1-1003 Unix User\admin

**Note**: This could be handy later if we need to identify or spoof things later on.