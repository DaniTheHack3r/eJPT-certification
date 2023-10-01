# Whois enumeration

Whois lookup is part of the process of passive information gathering, you can get relevant information about the domain, who registered it and who manages it for example.

Whois is a query and response protocol that is widely used for querying databases that store the registered users or assignees of an internet resource.

We can use the whois utility from kali linux or an alternative on the internet which is who.is.

## What are we looking for when performing whois enumeration?

There is plenty of information when querying using whois, however, we are looking for relevant information like name servers and PII. Note that if DNSSEC is active PII will be redacted.

We can also perform whois querying for ip addresses, in that case, the whois command will return relevant information for that ip address, such as network range, CIDR, and so on.

## What can we do with this information?

We can get PII to find targets and perform fishing attacks, or enumerate ip ranges to target networks inside a company. 