1. Internet Message Control Protocol(ICMP)
 is mainly used for network diagnostics and error reporting. 

Two popular commands are used: (they are used for network troubleshooting):

 #### ping: 
 This command uses ICMP to test connectivity to a target system and measures the round-trip time (RTT).
 In other words, it can be used to learn that the target is alive and that its reply can reach our system.

 #### traceroute:(tracert)
 It uses ICMP to discover the route fom your host to the target.

# Ping:
1. The ping command sends an ICMP Echo Request (ICMP type 8).
2. The computer on the receiving end responds with an ICMP Echo Reply(ICMP TYPE 0).
3. Things that prevent us from getting areply:
   A.  system is offline or shut down.
   B.  A firewall might block the necessary packets for  ping to work.

   ping - -c 4 = stops sending packets after 4 sent.


# Traceroute:
1.  How can we make every router between our system and a target system reveal itself?

2. The internet protocol has a field called Time-to-Live(TTL) that indicates the maximum number of routers a packet can travel through before it is dropped.

3.  The router decrements the packet’s TTL by one before it sends it across. When the TTL reaches zero, the router drops the packet and sends an ICMP Time Exceeded message (ICMP Type 11). (In this context, “time” is measured in the number of routers, not seconds.)

3. The terminal output below shows the result of running traceroute to discover the routers between our system and example.com. Some routers don’t respond; in other words, they drop the packet without sending any ICMP messages.

 4. Routers that belong to our ISP might respond, revealing their private IP address. Moreover, some routers respond and show their public IP address, and this would let us look up their domain name and discover their geographic location. Finally, there is always a possibility that an ICMP Time Exceeded message gets blocked and never reaches us.




