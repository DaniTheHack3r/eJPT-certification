# Installing & Configuring the Metasploit Framework

+ The MSF is distributed by Rapid7 and can be downloaded and installed as a standalone package on both Windows & Linux.

+ In this course we will be utilizing the Metasploit Framework on Linux and our preferred distribution of choice is Kali Linux.

+ MSF and its required dependencies come pre-packaged with Kali Linux which saves us from the tedious process of installing MSF manually.

## The Metasploit Framework Database

+ The Metasploit Framework Database (msfdb) is an integral part of the Metasploit Framework and is used to keep track of all your assessments, host data scans etc.

+ The Metasploit Framework uses PostgreSQL as the primary database server, as a result, we will also need to ensure that the PostgreSQL
database service is running and configured correctly.

+ The Metasploit Framework Database also facilitates the importation and storage of scan results from various third party tools like Nmap and Nessus.

## Installation Steps

+ Update our repositories and upgrade our Metasploit Framework to the latest version.

+ Start and enable the PostgreSQL database service.

**Note**: Run `sudo systemctl start postgresql` to start postgreSQL service in kali.

+ Initialize the Metasploit Framework Database (msfdb).

**Note**: To initialize the database, just run `sudo msfdb init`.

+ Launch MSFconsole!

**Note**: msfconsole requires sudo permissions to perform some actions, so it is recommended to run it as sudo.

**Note**: You could also run db commands from the msf console to check for status. For example: `db_status` will print you if it connected to the db.
