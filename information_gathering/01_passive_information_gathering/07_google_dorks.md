# Google Dorks (Google Hacking)

It's a technique to use google filtering in order to get relevant information about a target.

## Operators

There are a good amount of operators that can be used when searching in google to filter what we want:

- site:`<site-domain>` => shows results from domain and subdomains passed as arguments. You could also enumerate subdomains using the syntax site:*.`<site-domain>`.
- inurl:`<pattern>` => shows results including a specified pattern in the url.
- intitle:`<pattern>` => shows results including a specified pattern in the site title.
- filetype:`<file-extension>` => shows results including files indexed by google with the matching extension, combined with other filters you could get different files from specified websites or in combination with search queries.

**Note**: There is a misconfiguration/vulnerability called directory listing in web servers, this could allow someone to read files from a web server by using the operator intitle:index of in a google search.

- cache:`<site-domain>` => shows a google web cache page with the specified domain. Alternatively we could use the waybackmachine portal to perform this sort of look up.

## Other examples

- You could inurl to find the file that stores passwords like this: inurl/intitle:auth_user_file.txt or inurl/intitle:passwd.txt.

- There is a site called google hacking database (https://www.exploit-db.com/google-hacking-database) that will aid you when performing this sort of look ups using google dorks.

**Note**: the wp-config.bak in wordpress could be leaked in google if we are not careful, and it could contain credentials of sql databases attached to wordpress. 