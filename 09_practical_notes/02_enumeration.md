# Enumeration Notes

- It is a good idea to follow tracks when enumerating. At the end, you will not always know how to hack a machine, so, open your mind and try to follow documentation, deprecated methods, hacktricks, exploit-db, and gather all the information you can to then connect the points.

- If you get inital access during your recon/enumeration phase, don't look anywhere else, try to gather all the information you could from the exposed machine, you can check other technical details later.

- Local enumeration of the process running on a certain port on a linux machine will require a bit of expertise. Best options are to run `netstat -ano` and `ss -tl` or `ss -tln`. `ps aux` will help you enumerate other processes as well.

**Note**: SQL always needs ; at the of queries.
