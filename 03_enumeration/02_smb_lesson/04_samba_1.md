# SMB: Samba 1

Now we will take a look a some use cases of smb for linux. Samba is an implementation of the smb protocol for linux environments.

**Note**: `--top-port` flag can be used to scan the top number ports based on the argument you pass along.

Usually ports 139 and 445 are open as well. But we can check for udp ports 137 and 138 as well.

Don't get confused when looking at Samba, if you attempt to use smb-os-discovery script, it could throw that it is a windows machine, even when samba is for linux machines. The samba version could tell the truth in the end.

**Note**: This is the first approach to the `metasploit framework (MSF)`, in this case we will perform the same enumeration for samba.

In this scenarion we will use the auxiliry package `scanner/smb/smb_version` to enumerate samba using MSF.

There is another tool called `nmblookup` that can perform the same type of enumeration. It utilize the netbios protocol to connect to smb. in the output we can see a number 20 "status", it means we can connect to it.

And in that case we can use `smbclient` to try to connect to the server. We can perform a connection with a null section to see if it exists. 

**Note**: If the output presents an IPC share, there's a chance we can actually connect to the smb server with a null session.

The last tool in this lab is rpcclient, if the null session is available, we can connect with it using `rpcclient -U "" -N x.x.x.x` and if no error is given, the null session exists and we succesfully connected, any action beyond that wouldn't be considered enumeration.