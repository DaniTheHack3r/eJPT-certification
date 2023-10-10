# SMB: Samba 3

In this lab we will list all available shares using nmap, smb_enumshares metasploit module, enum4linux and smbclient. We will find domain groups that exist on the samba server using enum4Linux and rpcclient. We will figure out if the samba server is configured for printing and how many directories are present inside share "public". Finally we will fetch our flag from the server.

1. List all available shares on the samba server using Nmap script.

- to enum shares we use the script smb-enum-shares.

**Note**: The shares and the users that have access to those shares are important, we can utilize that to get something interesting.

2. List all available shares on the samba server using smb_enumshares Metasploit module.

- We use the auxiliary module `scanner/smb/smb_enumshares`.

**Note**: most modules come with default configurations that are pretty good. You can trust those configs unless someone advise you otherwise.

3. List all available shares on the samba server using enum4Linux.

- We can enumerate shares with enum4linux using `enum4linux -S x.x.x.x`.

**Note**: It is of our best interest to take a look a different tools and use the ones we are comfortable with. Using different tools can make a big difference as well as you can compare and contrast different outputs. Then you will figure out which one you like the most.

4. List all available shares on the samba server using smbclient.

- For smbclient we use `smbclient -L x.x.x.x -N`.

5. Find domain groups that exist on the samba server by using enum4Linux.

- In enum for linux to enumerate groups we use `enum4linux -G x.x.x.x`.

**Note**: Some groups can give special permissions or tell useful information about the roles and responsabilities shared by different users. Even if we don't understand the names of the groups we can still write them down and figure out later.

6. Find domain groups that exist on the samba server by using rpcclient.

- With rpcclient we use `rpcclient -U "" -N x.x.x.x` and with the connection established we use `enumdomgroups` to enumerate groups.

**Note**: This is the manual way of enumerating things from the smb server, other programs are just script that do it automatically.

7. Is samba server configured for printing?

- To figure out if the server is configured for printers, we use enum4linux command: `enum4linux -i x.x.x.x`.

8. How many directories are present inside share “public”?

- Just access the smb server in Public using smbclient. There are 2 directories present.

9. Fetch the flag from samba server.

- To download the file use the `get` command while connected to the server using smbclient.