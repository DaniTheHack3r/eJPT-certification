# SMB: Samba 2

This is a continuation of the previous section.

In this case we will try to use rpcclient to inspect for a null session.

If the null session is logged in correctly, we can try to fetch server information using the command srvinfo in the open session.

Another tool we will look at is enum4linux. It is a powerful tool for this case. And we can try to fetch os system information using `-o` flag as well sid, session check and workgroup/domain.

We can try out the same using smbclient where we can compare the previous output from enum4linux. 

We can also use smb-protocols script from nmap for comparison and to get some information about the dialects that current smb server handles, in this case samba.

We can try to compare this information with the one output of msfconsole using the auxiliary tool scanner/smb/smb2.

**Note**: check options in msfconsole to know what you have at hand.

**Note**: If you don't understand the importance of something, don't worry, just enumerate it and then we will come back later to it to see if it is useful to find exploits.

We can enum users using the smb-enum-users script from nmap. They will be useful later if we try to connect to them later. But we can compare the output with enum4linux list user flag `-U` and we can do it another way using null session with rpcclient and running the command `enumdomusers` while connected to the smb server.

We can run the command `lookupnames <name>` to get some information about the specified name. In this case the ful SID is obtained from the current lab.