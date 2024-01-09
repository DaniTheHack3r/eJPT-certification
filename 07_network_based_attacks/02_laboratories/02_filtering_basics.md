# Filtering Basics

For this lesson we are going to take tshark and apply some display filters to it. It will help us understand how far we can go and what we could integrate to our scripts and tools workflow.

- We will start by reading again the pcap file and filtering http traffic using `tshark -r $FILENAME -Y 'http'`.

**Note**: If you pipe it through `more`, you can browse through te big file easily, page by page.

- Now we are going to see the traffic between 2 specific ip addresses, by running `tshark -r $FILE_NAME -Y 'ip.src==$SOURCE_IP && ip.dst=$DESTINATION_IP'`.

- Let's look at a GET request method, by running `tshark -r $FILE_NAME -Y 'http.request.method==GET'`.

- We are now going to filter fields displayed when taking a look at the pcap file. We can start by running `tshark -r $FILE_NAME -Y 'http.request.method==GET' -Tfields -e frame.time -e ip.source -e http.request.full_uri`.

- We could try to filter using the operator `contains` followed by an expression, for example `tshark -r $FILE_NAME -Y 'http contains password'` will display if the http request of any package contains something related to the word password, probably a field or real password.

- We could also use tshark to add a filter by host. For example `tshark -r $FILE_NAME -Y 'http.request.method=GET && http.host==$HOST_NAME' -Tfields -e ip.dst` will show you any package that was sent to the specified host name and it will display the field of the destination port.

- As an exercise, we are going to play a little bit with the tshark utility. First, let's filter by an ip contains and see if a particular machine reached to it `tshark -r $FILE_NAME -Y 'ip contains amazon.in && ip.src=$SOURCE_IP' -Tfields -e ip.src -e http.cookie`. This will display the cookie, which could give us useful information.

- Now let's say we want to check the user agent, run `tshark -r $FILE_NAME -Y 'ip.src=$SOURCE_IP && http' -Tfields -e http.user_agent`.
