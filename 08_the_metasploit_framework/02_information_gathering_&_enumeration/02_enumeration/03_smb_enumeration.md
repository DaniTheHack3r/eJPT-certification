# SMB Enumeration

+ SMB (Server Message Block) is a network file sharing protocol that is used to facilitate the sharing of files and peripherals between computers on a local network (LAN).

+ SMB uses port 445 (TCP). However, originally, SMB ran on top of NetBIOS using port 139.

+ SAMBA is the Linux implementation of SMB, and allows Windows systems to access Linux shares and devices.

+ We can utilize auxiliary modules to enumerate the SMB version, shares, users and perform a brute-force attack in order to identify users and passwords.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it SMB_ENUM for this example.

- Set globally the target IP with `setg RHOSTS $TARGET_IP`.

- Start by search smb auxiliary modules by running `search type:auxiliary name:smb`.

- We will start by detecting the smb version with `auxiliary/scanner/smb/smb_version`.

- Now we will perform user enumeration with `auxiliary/scanner/smb/smb_enumusers`. Save the users you get from the output.

**Note**: Apart from options, you can type the `info` command to get more information about the module.

- Now we will perform share enumeration with `auxiliary/scanner/smb/smb_enumshares`. We can set the option `ShowFiles` to true if needed. Save the output for later.

- Now we will perform a bruteforce on smb with `auxiliary/scanner/smb/smb_login`. We can use the list `/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt` and the user to admin. We can change the option stop on success if needed. Save the output. 

- For the next step, we are going to exit the msfconsole and use `smbclient -L  \\\\$TARGET_IP\\ -U admin` and it will prompt you with the password. To access a share we can use `smbclient -L  \\\\$TARGET_IP\\$SHARE_NAME -U admin`. We can steal the flag from one of the shares.

**Note**: The smb laboratory was already complete on another lesson. So no flag was retrieved in order to proceed.
