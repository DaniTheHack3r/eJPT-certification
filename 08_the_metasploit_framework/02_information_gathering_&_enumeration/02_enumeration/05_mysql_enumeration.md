# MySQL Enumeration

+ MySQL is an open-source relational database management system based on SQL (Structured Query Language).

+ It is typically used to store records, customer data, and is most commonly deployed to store web application data.

+ MySQL utilizes TCP port 3306 by default, however, like any service it can be hosted on any open TCP port.

+ We can utilize auxiliary modules to enumerate the version of MySQL, perform brute-force attacks to identify passwords, execute SQL queries and much more.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it MySQL_ENUM for this example.

- Set globally the target IP with `setg RHOSTS $TARGET_IP`, do this for the RHOST option as well.

- We will start by scanning for the version using `auxiliary/scanner/mysql/mysql_version`. You can double check that the port in the options is correct by performing a simple tcp port scan on the target.

- Now we are going to perform a basic login brute force over mysql in order to get legitimate crendentials and get access to the database. Recommeded pass_file is `/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt` and username `root`.

**Note**: We know the server is running ubuntu, so we can directly target the root user to perform the brute force.

- Now we are going to perform some further enumeration, this kind of enumeration requires administrativa access to the service we want to scan. This administrativa condition can be guessed because the module has the name prefixed with `auxiliary/admin`. To enumerate mysql we are going to use `auxiliary/admin/mysql/mysql_enum`. The output will contain information about the database, the host system, and usernames, password hashes and privileges.

- Now we are going to use the module `auxiliary/admin/mysql/mysql_sql` to directly execute sql queries in order to interact with the database. Here are some test queries:

    + select version()
    + show databases;
    + use `<database>`;

- We can also extract the database schemas by running `auxiliary/scanner/mysql/mysql_schemadump`. This could help us figure out better queries in order to perform enumeration.

- We can list loot and credentials we have got when enumerating when running commands `loot` and `creds`.

- We can access the database directly using the mysql client. `mysql -h $REMOTE_HOST -u root -p`, it will prompt the password, and then you will have full access to the database.
