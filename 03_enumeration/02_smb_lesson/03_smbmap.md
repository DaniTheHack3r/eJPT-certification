# SMB: SMBMap

For this lab we will learn how to use SMBMap, which is a program made in python for SMB enumeration, to enumerate SMB and we will have to find a flag that way.

steps:

- Run a nmap command to identify the windows machine running smb.
- Run a nmap command using the script smb-protocols to gather some info about smb.
- Run smbmap with the following syntax: `smbmap -u guest -p "" -d . -H x.x.x.x`.
- Run smbmap with privileged access and take a look at the differences with the previous guest enumeration attempt: `smbmap -u <privileged-access> -p <privileged-password> -d . -H x.x.x.x`.
- Now we will attempt to run commands during the enumeration to get further information inside the target like this: `smbmap -u <privileged-access> -p <privileged-password> -x 'ipconfig' -H x.x.x.x`. In this case ip information of the target machine would be displayed.
- Now we will perform enumeration again with -L flag to list mounted directories in smb: `smbmap -u <privileged-access> -p <privileged-password> -H x.x.x.x -L`.
- We will perform the reading of one share using the following command: `smbmap -u <privileged-access> -p <privileged-password> -H x.x.x.x -r 'C$'`.
- Now we will perform the write of that disk. We will upload a file called backdoor to test it out like this: `smbmap -H x.x.x.x -u <privileged-access> -p <privileged-password> --upload /path/to/file 'C$\path\to\file'`.
-finally we can download a file like this: `smbmap -H x.x.x.x -u <privileged-access> -p <privileged-password> --download 'C$\path\to\file'`.

We mananged to enumerate, access, execute commands, upload and download files using just smbmap.