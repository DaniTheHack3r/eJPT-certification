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