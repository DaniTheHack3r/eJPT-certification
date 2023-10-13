# HTTP IIS Nmap Scripts

1. Identify IIS Server

Version is IIS httpd 10.0

Run `http-enum` script with nmap for further enumeration like interesting directories available in the web server.

2. Get webserver header details

To get webserver header details, we can use the nmap script `http-headers`.

Headers:

| http-headers: 
|   Cache-Control: private
|   Content-Type: text/html; charset=utf-8
|   Location: /Default.aspx
|   Server: Microsoft-IIS/10.0
|   Set-Cookie: ASP.NET_SessionId=khggyl0t4dz4phvys3htgbrz; path=/; HttpOnly; SameSite=Lax
|   X-AspNet-Version: 4.0.30319
|   Set-Cookie: Server=RE9UTkVUR09BVA==; path=/
|   X-XSS-Protection: 0
|   X-Powered-By: ASP.NET
|   Date: Fri, 13 Oct 2023 02:42:49 GMT
|   Connection: close
|   Content-Length: 130

3. Enumerated HTTP methods

To get http methods we use the nmap script `http-methods`. If we want to pass a specific url, we can pass script-arg `http-methods.url-path=/path/`.

Available http methods:

http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST COPY PROPFIND DELETE MOVE PROPPATCH MKCOL LOCK UNLOCK PUT
|   Potentially risky methods: TRACE COPY PROPFIND DELETE MOVE PROPPATCH MKCOL LOCK UNLOCK PUT
|_  Path tested: /webdav/

4. Detect WebDAV configuration - etc.

To enumerate some information about webdav, we can run the nmap script `http-webdav-scan` with script-arg `http-methods.url-path=/path/`. It uses exactly the same script arg as the previous one.

WebDAV configuration:

| http-webdav-scan: 
|   Server Date: Fri, 13 Oct 2023 02:48:14 GMT
|   WebDAV type: Unknown
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, POST, COPY, PROPFIND, LOCK, UNLOCK
|   Server Type: Microsoft-IIS/10.0
|_  Public Options: OPTIONS, TRACE, GET, HEAD, POST, PROPFIND, PROPPATCH, MKCOL, PUT, DELETE, COPY, MOVE, LOCK, UNLOCK
