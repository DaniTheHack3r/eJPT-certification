# SSH Recon: Basic

Ssh stands for Secure SHell. It is a secure protocol to transfer shell I/O through a connection, commonly used for remote administration.

1. What is the version of SSH server.

The current version of ssh is OpenSSH 7.2p2 for Ubuntu.

2. Fetch the banner using netcat and check the version of SSH server.

**Note**: Rather than using the ssh tool, we use netcat to connect to the port 22 and will fetch the banner directly, without the need of using nmap for the task, this banner is useful for enumeration.

The banner is: SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.6

3. Fetch pre-login SSH banner.

The banner is: Welcome to attack defense ssh recon lab!!

4. How many “encryption_algorithms” are supported by the SSH server.

To enumerate all algorithms we use the nmap script `ssh2-enum-algos`. There are 29 encryption algorithms available.

5. What is the ssh-rsa host key being used by the SSH server.

To get the ssh-rsa host key, the one that ssh actually use for ecryption, we can use the nmap script `ssh-hostkey` passing the following arg `ssh_hostkey=full`.

The full key:

ssh-hostkey: 
|   ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC1fkJK7F8yxf3vewEcLYHljBnKTAiRqzFxkFo6lqyew73ATL2Abyh6at/oOmBSlPI90rtAMA6jQGJ+0HlHgf7mkjz5+CBo9j2VPu1bejYtcxpqpHcL5Bp12wgey1zup74fgd+yOzILjtgbnDOw1+HSkXqN79d+4BnK0QF6T9YnkHvBhZyjzIDmjonDy92yVBAIoB6Rdp0w7nzFz3aN9gzB5MW/nSmgc4qp7R6xtzGaqZKp1H3W3McZO3RELjGzvHOdRkAKL7n2kyVAraSUrR0Oo5m5e/sXrITYi9y0X6p2PTUfYiYvgkv/3xUF+5YDDA33AJvv8BblnRcRRZ74BxaD
|   ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBB0cJ/kSOXBWVIBA2QH4UB6r7nFL5l7FwHubbSZ9dIs2JSmn/oIgvvQvxmI5YJxkdxRkQlF01KLDmVgESYXyDT4=
|_  ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKuZlCFfTgeaMC79zla20ZM2q64mjqWhKPw/2UzyQ2W/

**Note**: These keys could be really useful later.

6. Which authentication method is being used by the SSH server for user “student”.

To get auth methods supported for a particular user with nmap, we use the script `ssh-auth-methods`, passing the --script-args like this: `--script-args="ssh.user=student"`.

For student there are none auth methods available, this could really dangerous.

7. Which authentication method is being used by the SSH server for user “admin”.

For admin we can run the same script as before, and we will get that the admin users has publickey and password authentication methods available.

8. Fetch the flag from /home/student/FLAG by using nmap ssh-run script.

**Note**: using the command scp it can be performed like this: `scp <username>@x.x.x.x:/path/to/remote/source /path/to/local/destination`. Source and destination can be remote or local.

Using the user student we got access. However, this user doesn't have any sort of control or limited control over the machine we connect to.