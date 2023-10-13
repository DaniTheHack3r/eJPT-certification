# HTTP Apache

1. Which web server software is running on the target server and also find out the version using nmap.

The web ser application is apache and it is running the version 2.4.18 for ubuntu.

2. Which web server software is running on the target server and also find out the version using suitable metasploit module.

To answer this question we will use the auxiliary module `scanner/http/http_version`. It responded Apache 2.4.18 for ubuntu.

3. Check what web app is hosted on the web server using curl command.

Using curl we get a full website running in the webserver.

4. Check what web app is hosted on the web server using wget command.

Using wget will download a file, we can try with the index file of the site like this: `wget "http://x.x.x.x/index` and we get the same html as before.

5. Check what web app is hosted on the web server using browsh CLI based browser.

It is the default webpage of apache for ubuntu.

6. Check what web app is hosted on the web server using lynx CLI based browser.

It is the default webpage of apache for ubuntu.

**Note**: Lynx differs from browsh in that Lynx will only parse the text in a readable web for the shell, on the other hand, browsh tries to render the whole page with higher fidelity to colors and position.

7. Perform bruteforce on webserver directories and list the names of directories found. Use brute_dirs metasploit module.

For this task we will use the auxiliary module `scanner/http/brute_dirs`. It will use a wordlist that comes with metasploit framework and will return matching directories.

Found directories: 

[+] Found http://192.21.78.3:80/dir/ 200
[+] Found http://192.21.78.3:80/src/ 200

8. Use the directory buster (dirb) with tool/usr/share/metasploit-framework/data/wordlists/directory.txt dictionary to check if any directory is present in the root folder of the web server. List the names of found directories.

With dirb we can do it like this: `dirb http://x.x.x.x /path/to/wordlist`. 

Found directories:

+ http://192.21.78.3//data (CODE:301|SIZE:309)                              
+ http://192.21.78.3//dir (CODE:301|SIZE:308)

9. Which bot is specifically banned from accessing a specific directory?

To check robots.txt we only need to go to the following route in any url: `/robots.txt`. It is going to tell us all those directories the site doesn't want bots to read them.

In this case, we will use metasploit framework, just to keep it up. And we will use the auxiliary module `scanner/http/robots.txt`.

The bot that is banned is: BadBot.
