# Dumping Hashes With Mimikatz

## Mimikatz

**Note**: Mimikatz is the de facto standard when dumping hashes from windows.

- Mimikatz is a Windows post-exploitation tool written by Benjamin Delpy (@gentilkiwi). It allows for the extraction of clear-text passwords, hashes and Kerberos tickets from memory.

- The SAM (Security Account Manager) database, is a database file on Windows systems that stores hashed user passwords.

- Mimikatz can be used to extract hashes from the lsass.exe process memory where hashes are cached.

- We can utilize the pre-compiled mimikatz executable, alternatively, if we have access to a meterpreter session on a Windows target, we can utilize the inbuilt meterpreter extension Kiwi.

**Note**: Mimikatz will require elevated privileges in order to run correctly.

## Laboratory

- Start by a simple scan with Nmap.

- You will see in the scan the BadBlue server exposed on the target with version 2.7. You can use the msfconsole module to exploit badblue vulnerability at that version and establish a meterpreter session.

- Once you have the meterpreter session established, get some more information abouth the target, check if you have Administrative privileges and if that's the case, you can migrate to any other process.

- Look for the lsass process and migrate to it in the meterpreter session to get NT AUTHORITY\SYSTEM.

### Kiwi

- Now load kiwi using `load kiwi` in meterpreter and check the options. We will focusing in `lsa_dump_sam` to dump the whole SAM database and `creds_all` to dump credentials in memory.

- Run `creds_all` to check all credentials, you should get some NTLM hashes and passwords from memory.

**Note**: In windows versions later than 8, you should see that the plain text password is not available. That is because windows stop storing plain text password after that version.

- Now run `lsa_dump_sam` to get all the SAM database unparsed. You will notice that it comes with all NTLM hashes for all accounts in the local machine and a SysKey, which is retrieved by Mimikatz from memory and can be very useful later on.

- We will check also `lsa_dump_secrets` and we will get secrets that could provide us with clear text credentials in some cases.

**Note**: If you are working in a Active Directory environment, you could also dump kerberos tickets or create kerberos golden tickets which could come handy.

**Note**: We can also use the command `password_change` to change the password of an account, however, it is not recommended in a production environment for obvious reasons.

**Note**: Sometimes hashes are really important for one reason, and it is that most of the time we cannot really crack the hashes, fortunately, we can still use the hashes to authenticate in a active directory or windows environment.

### Mimikatz Standalone

- Now we will use Mimikatz standalone. Go to the root of the C drive and create a Temp folder and move to that folder. Fortunately, mimikatz executable come prepackaged with kali linux and can be loaded using the meterpreter session that you have running with high privileges with no extra steps using `upload /usr/share/windows-resources/mimikatz/x64/mimikatz.exe`.

- Now run a command shell session and start mimikatz by running `.\mimikatz.exe` and it will open the command line interface for mimikatz.

- Check for the right privileges using the command `privilege::debug` if the output is `Privelege '20' OK` then we are good to go.

- To replicate the commands we previously did using the mimikatz extension kiwi. If we want to dump the contents of the sam database we just need to run the command `lsadump::sam`. It will provide you with more information that kiwi. To dump lsa secrets we can use the command `lsadump::secrets`.

**Note**: you will see that the Administrator user has the RID 500 which will confirm that is indeed the Administrator.

- If the system is configured to store logon passwords in clear text, mimikatz can show you those passwords if you run `sekurlsa::logonpasswords`.

**Note**: if the logon passwords are not stored as plain text in memory, they will be presented as `(null)` in the password field of the sam database dump.

Flags:

Administrator User NTLM Hash: e3c61a68f1b89ee6c8ba9507378dc88d
Student User NTLM Hash: bd4ca1fbe028f3c5066467a7f6a73b0b
Syskey: 377af0de68bdc918d22c57a263d38326