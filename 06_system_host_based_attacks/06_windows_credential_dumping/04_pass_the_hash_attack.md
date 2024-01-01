# Pass-The-Hash Attacks

- Pass-the-hash is an exploitation technique that involves capturing or harvesting NTLM hashes or clear-text passwords and utilizing them to authenticate with the target legitimately.

- We can use multiple tools to facilitate a Pass-The-Hash attack:
    + Metasploit PsExec module
    + Crackmapexec

- This technique will allow us to obtain access to the target system via legitimate credentials as opposed to obtaining access via service exploitation.

**Note**: In Windows Environments, having a hash is just as useful as having a plain text password.

**Note**: There's a reason why is important to harvest hashes as you exploit vulnerabilities to gain privileged access and is that you need to assure yourself some persistance when attacking a target. This is because the target could patch the recently exploited vulnerability or add rules to the firewall to manage access to certain ports.

## Laboratory

### Initial Access

We will use the same laboratory we used in the mimikatz lesson.

- Start up postgresql and msfconsole, and then exploit BadBlue to get initial access.

- You will get priveleged access exploiting BadBlue as Administrator, migrate to lsass process and you should have now NT AUTHORITY/SYSTEM privilege.

- load Kiwi and dump the hashes and save them in your local machine.

### Using psexec Metasploit Module

To use the psexec module, you will need to get the LM hash in addition to the NT hash you already have. 

- To get the hashes we will use the kiwi extension to run `hashdump` to get the the full hash of every user.

**Note**: You will notice that the LM hash is the same for all users.

- In msfconsole we will use the `exploit/windows/smb/psexec` module. Remeber to change the LPORT if you left the previous meterpreter session running. And for this module you will need to set RHOSTS, SMBUser and SMBPass. In the SMBPass you will set the LM + NT hashes.

**Note**: if you use only one hash instead of the combination, you could get errors and can be quite problematic.

**Note**: In the description of the module you will notice that it is an authenticated code execution, so you need to autheticate to the target machine legitimately to use it.

**Note**: It might fail to establish a connection using the meterpreter payload is target is not set properly (default to Automatic), you could try with other options like Command or PowerShell, or use the Native\ upload to upload the actual meterpreter payload.

### Crackmapexec

- Using crackmapexec you just need to run `crackmapexec $PROTOCOL x.x.x.x -u $USERNAME -H "$NT_HASH" -x "$COMMAND"`, in this case the protocol is smb.

**Note**: You could execute any command using crackmapexec, even changing the password running `net user administrator $NEWPASSWORD`.

**Note**: This is a vulnerability attackers take advantage often and it exists inside windows even in newer versions of windows.

**Note**: Another tool that can be used to perform a pass the hash attack is evilwinrm.