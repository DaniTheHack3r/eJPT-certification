# Port Scanning with Auxiliary Modules

+ Auxiliary modules are used to perform functionality like scanning, discovery and fuzzing.

+ We can use auxiliary modules to perform both TCP & UDP port scanning as well as enumerating information from services like FTP, SSH, HTTP etc.

+ Auxiliary modules can be used during the information gathering phase of a penetration test as well as the post exploitation phase.

+ We can also use auxiliary modules to discover hosts and perform port scanning on a different network subnet after we have obtained initial access on a target system.

**Note**: Post exploitation scanning techniques cannot be performed using nmap, at least not as easy. That's why we use auxiliary modules to perform these tasks after initial access. 

## Lab Infrastructure

+ Our objective is to utilize auxiliary modules to discover open ports on our first target.

+ The next step will involve exploiting the service running on the target in order to obtain a foothold.

+ We will then utilize our foothold to access other systems on a different network subnet (pivoting).

+ We will then utilize auxiliary modules to scan for open ports on the second target.

**Note**: Check the page 53 of the pdf to see the network infrastructure.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it Port_Scan for this example.

- We can start by searching portscan modules. We can see that there are different types of scans, including tcp and syn scans.

**Note**: The target machine is the next ip after your ip address. If your ip is x.x.x.2, the target IP will be x.x.x.3.

- There are several options like the port range, the jitter, the delay and the maximum number of threads by target. In this case, is enough to set the RHOSTS with the corresponding target to start running the scan.

- In this lab in particular, we will find port 80 open. As this lab doesn't have a remote desktop available, we cannot see what it is hosting on a web browser. Let's use curl to download the html code to see if we can spot something.

- The web server should be running XODA, which should be enough to make some search in MSF. Run `search xoda` to see if there are any exploits available.

**Note**: On this case, we are not focusing on vulnerability detection and exploitation. We only want to get initial access. In that case, the exploit listed while searching should be enough to get that initial access.

- To execute the exploit module, we only need to set up the RHOSTS, and we need to take a look at the TARGETURI, in this case, the xoda path is in the root of the web server. After a successful execution, you should get a meterpreter session.

- Inside the meterpreter session, we can get some information about the system with `sysinfo`. It is a linux environmnt.

- Now we need to pivot to the next computer, we will start by initializing a shell in order to execute commands easier in the target linux environment. In this case, we can execute `shell` from meterpreter and then `/bin/bash -i` inside the shell to access bash.

- By running `ifconfig` we can get all the information related to the interfaces the machine is connected to. Here we will spot the primary NIC, the one we both share, but there's a second interface with a totally different subnet, we can scan it for new targets.

**Note**: The current machine is the victim-1, which in the new subnet has the ip ending in .2, the new target called victim-2 will be .3 in the new subnet.

- Now we will be going back to meterpreter. From there, we are going to use the utility `autoroute` by running `run autoroute -s $PIVOT_TARGET_IP` the -s stands for subnet, we don't need to pass along the subnet address and mask, it is enough passing the target ip address. It will the try to route through the current open session.

- Now we will go back to the msfconsole by putting the current session on background by running `background` from meterpreter. We can check the session is in background by typing `sessions` from the msfconsole.

- We will use the tcp port scanner once more and add the new ip address to the RHOSTS option. It will use the victim-1 computer to reach the victim-2 through the network. We can also adjust the ports we want to scan by setting the option PORTS if we want. When the scan completes, we should see different TCP ports open: 22, 21, 80 on victim-2.

- If we want to perform UDP scans, we will use a different auxiliary module called "udp_sweep". Search it with `search udp_sweep` and select the only one.

- We could perform the udp scan on the first target, to make it simple. Just add the target ip to the RHOSTS. No results should be returned as the target is not running any service over udp.
