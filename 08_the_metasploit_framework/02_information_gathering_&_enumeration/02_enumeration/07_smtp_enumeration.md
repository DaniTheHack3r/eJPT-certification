# SMTP Enumeration

+ SMTP (Simple Mail Transfer Protocol) is a communication protocol that is used for the transmission of email.

+ SMTP uses TCP port 25 by default. It is can also be configured to run on TCP port 465 and 587.

+ We can utilize auxiliary modules to enumerate the version of SMTP as well as user accounts on the target system.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it SMTP_Enum for this example.

- Set globally the target IP with `setg RHOSTS $TARGET_IP`, do this for the RHOST option as well.

- We will perform version enumeration using the module `auxiliary/scanner/smtp/smtp_version`, the output will also include the domain of the mail server.

- Now we will perform user enumeration using the module `auxiliary/scanner/smtp/smtp_enum`.

**Note**: SMTP is a great way to narrow down brute force attacks on a server.
