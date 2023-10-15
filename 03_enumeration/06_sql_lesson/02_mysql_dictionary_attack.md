# MySQL Dictionary Attack


1. Find the password of user “root” which is required to access the MySQL server. Use suitable metasploit module with password dictionary: /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

To achieve this we will use the auxiliary module `scanner/mysql/mysql_login`. Remember to setup a user file or a username.

result: root:catalina

2. Find the password of user “root” which is required to access the MySQL server. Use Hydra with password dictionary: /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

Just as a reminder, the hydra command would be: `hydra -l <username> -P /path/to/wordlist`. Remember that -P is for password wordlist and -p is for password word.

result: [3306][mysql] host: 192.162.202.3   login: root   password: catalina
