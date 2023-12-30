# Alternate Data Streams

- Alternate Data Streams (ADS) is an NTFS (New Technology File System) file attribute and was designed to provide compatibility with the MacOS HFS (Hierarchical File System).

- Any file created on an NTFS formatted drive will have two different forks/streams:
    + Data stream - Default stream that contains the data of the file.
    + Resource stream - Typically contains the metadata of the file.

- Attackers can use ADS to hide malicious code or executables in legitimate files in order to evade detection.

- This can be done by storing the malicious code or executables in the file attribute resource stream (metadata) of a legitimate file.

- This technique is usually used to evade basic signature based AVs and static scanning tools.

**Note**: ADS could be useful not only to bypass basic static scanning tools, but also to properly bypass human based detection and administrators.

## Laboratory

Before you start, know that this can be done from any windows seven environment, there is no need to have a lab and a penetration test, you only need a command shell to exploit to this vulnerability.

- Start a cmd shell and go to the Temp directory in Windows and create a file with notepad using the following command: `notepad test.txt:secret.txt`, notice the `:` symbol between the two file names. What it means is that you redirect the data stream to the alternate stream. A notepad will open showing the contents of the secret.txt file. Edit the file with any text and save it.

- Go to the directory you created the file at and open the `test.txt` file and notice it is empty. That is because the hidden file containing the information is in the resource stream and can be accessed again using `notepad test.txt:secret.txt`. When the test.txt is deleted, the secret.txt file is deleted as well.

- Now we can do the same with a .exe file. For example, we can use winpeas64.exe, an enumeration tool to scan windows for vulnerabilities. We can hide it behind a txt file like this: `type winpeas64.exe > windowslog.txt:winpeas.exe`, it will cat the binary content of the .exe file and write it into the winpeas.exe hidden inside windowslog.txt. And to run it, you can run it directly using `start windowslog.txt:winpeas.exe` or make a symbolic link.

- Go to the system32 directory and create a symbolic link pointing to the secret file. Like this: `mklink wupdate.exe C:\Temp\windowslog.txt:winpeas.exe`. After creating the link, it can be just run from a privileged cmd shell.

**Note**: it is commonly used to hide malicious payloads, like a meterpreter session created with msfvenom, but it could also store any type of data in the alternate stream.