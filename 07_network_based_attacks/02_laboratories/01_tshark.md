# Tshark

- We will start in a command shell environment. The first step is to check current tshark version with `tshark -v`.

- We can check the help menu by running `tshark -h | more`. 

**Note**: With `more` we can check one page at a time instead of seeing the whole help output.

- Let's check the interfaces we have available for capturing packets with `tshark -D`. And to start capturing, we can run `tshark -i $INTERFACE_NAME`.

- If we have a pcap saved, we can read it with tshark by running `tshark -r $FILE_NAME`.

**Note**: You can check the count of the pcap file output you got from tshark by piping it through `wc`.

**Note**: When you are using tshark, you need to understand what you are look for in order to make the search a little bit easier and more efficient. Consider that tshark helps you automate packet capture inside scripts, just like TCPDump, as both are command line interface programs.

- In order to get hierarchy by protocol using tshark, we can run `tshark -r $FILE_NAME -z io,phs -q` where -z stands for statistics and io,phs will give us the protocol hierarchy.
