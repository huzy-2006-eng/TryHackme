1. When two hosts communicate over a network, an IP packet is encapsulated within a data link frame as it travels over layer 2.

2. Remember that the two common data link layers we use are Ethernet (IEEE 802.3) and WiFi (IEEE 802.11).

3. Whenever one host needs to communicate with another host on the same Ethernet or Wi-Fi, it must send the IP packet within a data link layer frame. 

4. Although it knows the IP address of the target host,it needs to look up the target's MAC address so the proper data link layer can be created.

5. However, the devices on the same Ethernet network do not need to know each other’s MAC addresses all the time; they only need to know each other’s MAC addresses while communicating.

6. Everything revolves around IP addresses. Consider this scenario: You connect your device to a network, and if the network has a DHCP server, your device is automatically configured to use a specific gateway (router) and DNS server. Consequently, your device knows the IP address of the DNS server to resolve any domain name; moreover, it knows the IP address of the router when it needs to send packets over the Internet. In all this scenario, no MAC addresses are revealed. However, two devices on the same Ethernet cannot communicate without knowing each other’s MAC addresses.

# ARP (Address Resolution Protocol):
ARP makes it possible to find the possible MAC address of another device on the Ethernet.

In the example below, a host with the IP address 192.168.66.89 wants to communicate with another system with the IP address 192.168.66.1. 

It sends an ARP Request asking the host with the IP address 192.168.66.1 to respond. The ARP Request is sent from the MAC address of the requester to the broadcast MAC address, ff:ff:ff:ff:ff:ff as shown in the first packet. 

The ARP Reply arrived shortly afterwards, and the host with the IP address 192.168.66.1 responded with its MAC address. From this point, the two hosts can exchange data link layer frames.

ARP is considered layer 2 because it deals with MAC addresses. Others would argue that it is part of layer 3 because it supports IP operations. What is essential to know is that ARP allows the translation from layer 3 addressing to layer 2 addressing.
