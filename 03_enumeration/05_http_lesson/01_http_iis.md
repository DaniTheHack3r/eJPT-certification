# Windows Recon: IIS

HTTP is in which web technologies are based on. If a company has a website running, it is probably there is some way to get in there. As some would say, that is an open backdoor.

Footprinting and enumeration during the lab:

- Ports 135, 139 and 445 are open, that reveals a windows machine.
- Port 80 is open, going to the web browser we see webgoat.net. A learning tool for penetration tester, a purposly vulnerable website.
- Port 80 is running microsoft IIS httpd 10.0.
- Port 3306 is running mysql.
- OS fingerprint returns no matches.

Another way to perform this enumeration is using the tool whatweb. Whatweb not only fingerprints the web server but it also run some apache scripts to test for vulnerabilities.

Another tool to get some information about the web server is http, it will perform a fetch operation to get the page and that would be it. We could get some information like how the site is returning the page before rendering it, in other words, plain html and headers.

Another tool to enumerate http protocol is dirb. It will try to enumerate all findable directories or paths for the website url using wordlists.

Another tool to get some information from the website is browsh, it will render, the best it can, the website using the shell. Pretty useful if you only have the shell to work with.