# Penetration Testing with the Metasploit Framework

+ The MSF can be used to perform and automate various tasks that fall under the penetration testing life cycle.

+ In order to understand how we can leverage the MSF for penetration testing, we need to explore the various phases of a penetration test and their respective techniques and objectives.

+ We can adopt the PTES (Penetration Testing Execution Standard) as a roadmap to understanding the various phases that make up a penetration test and how Metasploit can be integrated in to each phase.

## Penetration Testing Execution Standard

The Penetration Testing Execution Standard (PTES) is a penetration testing methodology that was developed by a team of information security practitioners with the aim of addressing the need for a comprehensive and upto-date standard for penetration testing.

## Penetration Testing Phases

The following diagram outlines the various phases involved in a typical penetration test.

**Note**: Check page 31 of the pdf for figure reference.

## Penetration Testing With MSF

| Penetration Testing Phase           | Metasploit Framework Implementation            |
| ----------------------------------- | ---------------------------------------------- |
| Information Gathering & Enumeration | Auxiliary Modules                              |
| Vulnerability Scanning              | Auxiliary Modules, Nessus                      |
| Exploitation                        | Exploit Modules & Payloads                     |
| Post Exploitation                   | Meterpreter                                    |
| Privilege Escalation                | Post Exploitation Modules, Meterpreter         |
| Maintaining Persistent Access       | Post Exploitation Modules, Persistence Modules |
