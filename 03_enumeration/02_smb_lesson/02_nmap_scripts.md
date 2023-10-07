# SMB: Nmap Scripts

## How to enumerate SMB

To enumerate more information from SMB we can try running scripts directly with nmap. These scripts are available for reading in the documentation. These are some examples:

- `nmap -p445 --script smb-protocols x.x.x.x`: We can get some more information about the protocol version.
- `nmap -p445 --script smb-security-mode x.x.x.x`: We get more information about how security is set up for the service.

**Note**: Default configuration usually gets people in trouble.

- `nmap -p445 --script smb-enum-sessions x.x.x.x`: It will try to login to the smb server, weather it is a guest session (no username and password) or you pass along some combination of username and passwd, and it will get the other active sessions in the server. You can pass script arguments like this: `nmap -p445 --script smb-enum-sessions --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

- `nmap -p445 --script smb-enum-shares x.x.x.x`: It will login and enumerate access to shared information. We see here how smb is configured. It can receive the same arguments smb-enum-sessions receives, like this: `nmap -p445 --script smb-enum-shares --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

**Note**: Sometimes we can find something called null session labeled as IPC. This null session works as an anonymous session and can be very useful to access some information.
**Note**: Smb also handles printer information. It is the channel printers use to print from and to and scan to different machines on the network.

- `nmap -p445 --script smb-enum-users x.x.x.x`: It will enumerate the users. It is recommended to use administrator privileges for this script if at hand: `nmap -p445 --script smb-enum-users --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

- `nmap -p445 --script smb-server-stats x.x.x.x`: It will print server statistics, as the previous script it is better to add privileged access: `nmap -p445 --script smb-server-stats --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

- `nmap -p445 --script smb-enum-domains x.x.x.x`: It will enumerate domains of the smb server, including interesting information like password policies and properties which is good to know if you want to perform password attacks. It is better if we pass along privileged access as well: `nmap -p445 --script smb-enum-domains --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

- `nmap -p445 --script smb-enum-groups x.x.x.x`: It enumerate groups and can be useful to break up users into different levels. Pass along credentials for privileged access to get better information: `nmap -p445 --script smb-enum-groups --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

- `nmap -p445 --script smb-enum-services x.x.x.x`: It will enumerate services which the smb has access to even if they are not specific to that service, we can get a lot of information with this script. Pass along credentials for privileged access to get better information: `nmap -p445 --script smb-enum-services --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

- `nmap -p445 --script smb-enum-shares,smb-ls x.x.x.x`: Just like just running smb-enum-shares, it will also run a list command inside each share, pretty useful to get some info about what's inside those shares. Pass along privileged access for better results: `nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=<username>,smbpassword=<password> x.x.x.x`.

**Note**: In the enumeration phase it is important to gather as much information as you can. You never know what is going to be useful or what won't be useful in the future. You can come back later to figure that out.