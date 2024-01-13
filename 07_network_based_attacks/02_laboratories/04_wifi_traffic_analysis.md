# WiFi Traffic Analysis

**Note**: Just when taking a look at a pcap with wifi traffic captured, you need to consider that IEEE 802.11 is the protocol of wifi.

**Note**: When we analyze WiFi traffic, we need to understand that we are not seeing TCP/IP traffic, we are seeing Wireless layer 2 traffic, that's why the etherenet frame runs over IEEE 802.11.

## Filters that can be applied to understand Wireless traffic

- Most of the time, we want to filter the beacon frame, this frame contains information about the AP, like the SSID and the type of security. So we can add the filter `wlan.fc.type_subtype == 0x0008` which will filter only by the beacon frame.

- We usually don't want to filter WPA in its version 1, so we can filter it out using `!(wlan.wfa.ie.wpa.version == 1)`.

- We can combine the previously two filters with another filter for the wlan tag number, in this case we want to filter out the tag 48 which represents RSN or the robust security network interface element. `!(wlan.tag.number == 48)`.

- Combining the three filters, we can get all the networks that are not protected.

**Note**: Most of the information we can obtain by checking the packets of 802.11 WiFi protocol can be read inspecting their tags.

- We can filter specific information running a filter with `contains`. For example `wlan contains Home_Network`, it should probably filter out the SSID and any other value that contains Home_Network in it.

**Note**: If we find packets that contain the tag 48, which represent RSN, it should probably contain secure strategy to connect with. It could be WPS, WPA/PSK or WPA2/PSK using AES.

- With this type of traffic we can only filter using MAC addresses, if we want to check for information sent or received we can use the filter `(wlan.ta == xx:xx:xx:xx:xx:xx)` for information transmited from a certain MAC address or `(wlan.ra == xx:xx:xx:xx:xx:xx)` for packet received by a certain MAC address.

- If we want to filter directly by MAC addressl, we can use the filter `(wlan.bssid == xx:xx:xx:xx:xx:xx)`.

- If we want to filter data type captured along with the the 802.11 connection, we can directly filter using the Data subtype of 802.11 `(wlan.fc.type_subtype == 0x0020)`.

- There's another subtype called Association Response, this can be filtered using `(wlan.fc.type_sybtype == 0x0001)`, it is one of the management frames used by the access point to inform the client of the acceptance or refusal of its association.

## Flags

- What is the name of the Open (No Security) SSID present in the packet dump?

SecurityTube_Open

- The SSID 'Home_Network' is operating on which channel?

6

- Which security mechanism is configured for SSID 'LazyArtists'? Your options are: OPEN, WPA-PSK, WPA2-PSK.

WPA2-PSK

**Note**: It is difficult to differentiate between WPA-PSK with AES (Advanced Encryption Standard) and WPA2-PSK with AES. So consider that the latter is the one that commonly uses WPA2-PSK with AES. WPA usually uses WPA with TKIP (Temporal Key Integrity Protoco). You will also notice that WPA2 doesn't support TKIP, but WPA does.

- Is WiFi Protected Setup (WPS) enabled on SSID 'Amazon Wood'?  State Yes or No.

Yes

- What is the total count of packets which were either transmitted or received by the device with MAC e8:de:27:16:87:18?

5701

- What is the MAC address of the station which exchanged data packets with SSID 'SecurityTube_Open'?

5c:51:88:31:a0:3b

- From the last question, we know that a station was connected to SSID 'SecurityTube_Open'. Provide TSF timestamp of the association response sent from the access point to this station.

115152625
