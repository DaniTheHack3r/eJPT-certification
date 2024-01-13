# Filtering WiFi

In this laboratory we are going to filter using tshark.

- First we can try filtering wireless traffic using `tshark -r $CAPTURE_FILE -Y 'wlan'`.

- Now let's try to filter the deauthentication packet. To achieve that, we are going to run `tshark -r $CAPTURE_FILE -Y 'wlan.fc.type_subtype==0x000c'`.

- Now if we would like to filter the WPA handshake, we can run `tshark -r $CAPTURE_FILE -Y 'eapol'`.

- Now we are going to display the SSID and the BSSID when filtering the subtype 0x0008, which is the beacon frame `tshark -r $CAPTURE_FILE -Y 'wlan.fc.type_subtype==0x0008' -Tfields -e wlan.ssid -e wland.bssid`.

- Now what if we want to display the BSSID of a certain SSID? we can do it like this `tshark -r $CAPTURE_FILE -Y 'wlan.ssid==$SSID' -Tfields -e wlan.bssid`.

- Now we are going to try to display the channel of a certain SSID, we can do it like this `tshark -r $CAPTURE_FILE -Y 'wlan.ssid==$SSID' -Tfields -e wlan_radio.channel`.

- What if we want to see the deauthentication frame? And display the receivers. We can do it like this `tshark -r $CAPTURE_FILE -Y 'wlan.fc.type_subtype==0x000c' -Tfields -e wlan.ra`.

- Now, what if we want to check for some information about one receiver? We could probably even check the http headers that belong to the device with a certain MAC address we found in the pcap. We could do it like this `tshark -r $CAPTURE_FILE -Y 'wlan.ta==xx:xx:xx:xx:xx:xx && http' -Tfields -e http.user_agent`. We get the user agent to figure out the model and manufacturer.
