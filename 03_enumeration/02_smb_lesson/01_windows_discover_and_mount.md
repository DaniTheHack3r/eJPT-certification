# SMB: Windows discover and mount

## SMB windows discover

- SMB is the windows implementation of file share and it stands for Server Message Block.
- SMB originally ran on port 139, however, it now runs on port 445.

**Note**: Along 139 and 445, you will often find port 135 which runs windows implementation of RPC (remote procedure call). These three ports are commonly open in a windows machine. Port 3389 is the server port used for RPC.

We can follow the following steps for a regular scan against windows machines:

- Use `ipconfig` to get information about the network.
- Net scan using `nmap -T4 x.x.x.x/x --open`.
- Perform service enumeration on the target using `nmap x.x.x.x -sV -O`.
- Perform a default script based scan with `nmap x.x.x.x -sV -sC`.

## SMB usage

- You can set it up through the explorer in windows in the section network.
- However, you could use the following command to set it up: `net use <local-letter>: \\<remote-ip>\<remote-directory> <password> /user:<username>`
- And you can drop the connection like this: `net use * /delete`.

Those are the basics of SMB, and the idea is to take advantage of this protocol.