# Nmap auditing fundamentals

In this lab we are going to talk about asset management, one of the 17 capabilities presented by CMMC v1.0, and we are going to use nmap to audit it.

Usually, you are going to have a network map in the organization. An excel or database with all the names and ips of endpoints, workstations, firewall, networking devices, that are connected to the network. This is a really important asset for any organization to keep track of where all the devices are and what they do or host. This is similar to what pentesters but from a black box point of view.

Performing network scanning through nmap and enumerating those assets using an agressive scan on the hosts in the network and then compare those assets scanned to the actual inventory we have of machines will serve as proper auditing.