Whenever we want to access a network we need to configure the following:
1. IP Address
2. Router
3. DNS Server

Whenever we connect our device to a new network, the above configurations must be set according to the new network. Manually configuring these settings is a good option, especially for servers. Servers are not expected to switch networks; you don’t carry your domain controller and connect it to the coffee shop WiFi. Moreover, other devices need to connect to the servers and expect to find them at specific IP addresses.

DHCP rseolves IP conflict.
Ip Conflict - Two devices having same ip addresses.

DHCP Follows 4 Steps:

#### DHCP Discover:
The client broadcasts a DHCPDISCOVER message seeking the local DHCP server if one exists.

#### DHCP Offer:
The serverresponds with a DHCPOFFER message with an IP address available for the client to accept.

#### DHCP Request:
The client responds with a DHCPREQUEST message to indicate that it has accepted the offered IP

### DHCP Acknowledge:
The server responds with a DHCPACK message to confirm that the offered IP address is now assigned to this client.

## Example:
192.168.66.133

In the DHCP packet exchange:
1. The client starts without any IP network configuration.It only has a MAC address. 
In the first and third packets, DHCP Discover and DHCP Request, the client searching for a DHCP server still has no IP network configuration and has not yet used the DHCP server's offered IP address.
Therefore, it sends packets from the  IP address 0.0.0.0 to the broadcast IP address 255.255.255.255 .

2. As for the data link layer, in the first and third packets, the client sends to the broadcast MAC address, ff:ff:ff:ff:ff:ff.
The DHCP server offers an available IP address along with the network configuration in the DHCP Offer.
It uses the client's destination MAC address.

At the end we expect DHCP server has provided us with the following:
1.  The leased IP address to access network resources.
2. The gateway to route our packets outside the local network.
3. A DNS server to resolve domain names.

