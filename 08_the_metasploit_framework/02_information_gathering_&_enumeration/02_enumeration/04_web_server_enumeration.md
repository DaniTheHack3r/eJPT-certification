# Web Server Enumeration

+ A web server is software that is used to serve website data on the web.

+ Web servers utilize HTTP (Hypertext Transfer Protocol) to facilitate the communication between clients and the web server.

+ HTTP is an application layer protocol that utilizes TCP port 80 for communication.

+ We can utilize auxiliary modules to enumerate the web server version, HTTP headers, brute-force directories and much more.

+ Examples of popular web servers are; Apache, Nginx and Microsoft IIS.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it Web_Enum for this example.

- Set globally the target IP with `setg RHOSTS $TARGET_IP`, do this for the RHOST option as well.

- Let's start by searching for http auxiliary moules `search type:auxiliary name:http`.

- Now we are going to get the web server version using `auxiliary/scanner/http/http_version`.

- Now we are going to bring up the http_header scanner `auxiliary/scanner/http/http_header`.

- Now we are going to perform some extra enumeration for paths we might not have access to in the web server. We are going to check the robots.txt with an auxiliary module called `auxiliary/scanner/http/robots_txt`.

**Note**: The robots.txt is a file that developers use to tell search engines and scrappers what they can access freely and what they should not access, this could be potentially interesting.

- With the output of the robots.txt we can go a little bit further and try to see if the path that are disallowed have directory listing enabled. We can use curl to test it out. One of the directories of the previous output should be behind a form that asks for user and password. Credentials for this kind of form could be brute forced with another module.

- For now we are going to perform directory brute force, this type of enumeration could bring information about directories that are hidden but are accessible when requested. The module is `auxiliary/http/dir_scanner`. A dictionary is already set up by default, but we can use another if we want to.

- We can also perform file brute forcing. This can be achieved with the module `auxiliary/scanner/http/files_dir`. This module will scan the files as the previous one scanned for directories. These files could give us an idea of attack vectors we could use to exploit the web server.

**Note**: Another good place to find wordlists in your local kali linux is `/usr/share/wordlists/`.

- Now we are going to try to perform a brute force attack over the protected directory we found when scanning the robots.txt. In this case is the `/secure` directory, and it asks for credentials in order to access it. For this task we are going to use the `auxiliary/scanner/http/http_login`. For this module remember to specify the AUTH_URI which is the path to the protected directory. This module comes with PASS_FILE, USER_FILE and USERPASS_FILE specified by default. In this case, we can unset the USERPASS_FILE as PASS_FILE and USER_FILE are already specified. We can unset options with the command `unset`.

- Sometimes we won't get any result with the default lists. In that case, we can change them to more robust lists. Recommeded lists would be: `/usr/share/metasploit-framework/data/wordlists/namelist.txt` and `/usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`.

**Note**: We can set VERBOSE to false if we don't want to see the whole list of tries in the terminal.

- If the previous attempt didn't have any success, we can still enumerate users from the web server in order to narrow down the bruteforce. This module is pertinent to apache called `apache_userdir_enum` and it could help you see if there are valid usernames on the web server. We can set the list of users to `/usr/share/metasploit-framework/data/wordlists/common_users.txt`.

- Now we can go back to http_login module in order to try to perform the brute force again with the user rooty. For this, we will need to create a custom USER_FILE. It is a plain text file with the name we want in there. That will narrow down the user to just one iteration.

**Note**: Even with the list narrowed down, you could potentially 
