# FTP anonymous login

Anonymous FTP login is fairly common when trying to enumerate ftp protocol. In this lab we will try to recon ftp using an nmap script.

1. Find the version of vsftpd server.

- Version is: vsftpd 3.0.3.

2. Check whether anonymous login is allowed on the ftp server using nmap script.

- Using the script `ftp-anon`. If it is succesful, try connecting directly using username: anonymous and password: "".

3. Fetch the flag from FTP server.

- Flag: 4267bdfbff77d7c2635e4572519a8b9c.