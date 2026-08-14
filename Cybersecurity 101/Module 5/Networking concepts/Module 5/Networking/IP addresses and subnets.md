Every host on the network needs a unique identifier for other hosts to communicate with him. Without a unique identifier, the host cannot be found without ambiguity. When using the TCP/IP protocol suite, we need to assign an IP address for each device connected to the network.

One analogy of an IP address is your home postal address. Your postal address allows you to receive letters and parcels from all over the world. Furthermore, it can identify your home without ambiguity; otherwise, you cannot shop online!

As you might already know, we have IPv4 and IPv6 (IP version 6). IPv4 is still the most common, and whenever you come across a text mentioning IP without the version, we expect them to mean IPv4.

For a private IP address to access the Internet, the router must have a public IP address and must support Network Address Translation (NAT). At this stage, let’s not worry about understanding how NAT works, as we will revisit it later in this module.

Before moving on, I recommend memorising the private IP address ranges. Otherwise, you might see an IP address such as 10.1.33.7 or 172.31.33.7 and try to access it from a public IP address.

# Routing
In technical terms, a router forwards data packets to the proper network. Usually, a data packet passes through multiple routers before it reaches its final destination. The router functions at layer 3, inspecting the IP address and forwarding the packet to the best network (router) so the packet gets closer to its destination.

