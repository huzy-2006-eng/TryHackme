# Types of Firewalls:
## 1. Stateless Firewall-
This type of firewall operates on layer 3 and layer 4 of the OSI model and works solely by filtering the data based on predetermined rules without taking note of the state of the previous connections. This means it will match every packet with the rules regardless of whether it is part of a legitimate connection. It maintains no information on the state of the previous connections to make decisions for future packets. Due to this, these firewalls can process the packets quickly.

However, they cannot apply complex policies to the data based on its relationship with the previous connections. Suppose the firewall denies a few packets from a single source based on its rules. Ideally, it should drop all the future packets from this source because the previous packets could not comply with the firewall’s rules. However, the firewall keeps forgetting this, and future packets from this source will be treated as new and matched by its rules again.

## 2. Stateful Firewall-
Unlike stateless firewalls, this type of firewall goes beyond filtering packets by predetermined rules. It also keeps track of previous connections and stores them in a state table. This adds another layer of security by inspecting the packets based on their history with connections. Stateful firewalls operate at layer 3 and layer 4 of the OSI model. Suppose the firewall accepts a few packets from a source address based on its rules. 

In that case, it will take note of this connection in its stated table and allow all the future packets for this connection to automatically get allowed without inspecting each of them. Similarly, the stateful firewalls take note of the connections for which they deny a few packets, and based upon this information, they deny all the subsequent packets coming from the same source.

## 3. Proxy Firewall-
The problem with previous firewalls was their inability to inspect the contents of a packet. Proxy firewalls, or application-level gateways, act as intermediaries between the private network and the Internet and operate on the OSI model’s layer 7. They inspect the content of all packets as well.

The requests made by users in a network are forwarded by this proxy after inspection and masking them with their own IP address to provide anonymity for the internal IP addresses. Content filtering policies can be applied to these firewalls to allow/deny incoming and outgoing traffic based on their content.

## 4. Next-Generation Firewall-
This is the most advanced type of firewall that operates from layer 3 to layer 7 of the OSI model, offering deep packet inspection and other functionalities that enhance the security of incoming and outgoing network traffic. It has an intrusion prevention system that blocks malicious activities in real time.

It offers heuristic analysis by analyzing the patterns of attacks and blocking them instantly before reaching the network. NGFWs have SSL/TLS decryption capabilities, which inspect the packets after decrypting them and correlate the data with the threat intelligence feeds to make efficient decisions.


| Firewalls | Characteristics |
| :--- | :--- |
| Stateless firewalls | - Basic filtering<br>- No track of previous connections<br>- Efficient for high-speed networks |
| Stateful firewalls | - Recognize traffic by patterns<br>- Complex rules can be applicable<br>- Monitor the network connections |
| Proxy firewalls | - Inspect the data inside the packets as well<br>- Provides content filtering options<br>- Provides application control<br>- Decrypts and inspects SSL/TLS data packets |
| Next-generation firewalls | - Provides advanced threat protection<br>- Comes with an intrusion prevention system<br>- Identify anomalies based on heuristic analysis<br>- Decrypts and inspects SSL/TLS data packets |

# Firewall Rules
The basic components of a firewall’s rule are described below:

1. **Source address:** The machine’s IP address that would originate the traffic.
2. **Destination address:** The machine’s IP address that would receive the data.
3. **Port:** The port number for the traffic.
Protocol: The protocol that would be used during the communication.
4. **Action:** This defines the action that would be taken upon identifying any traffic of this particular nature.
5. **Direction:** This field defines the rule’s applicability to incoming or outgoing traffic.

## Types of Actions
1. **Allow:**
A rule’s “Allow” action indicates that the particular traffic defined inside the rule would be permitted.

For example, let’s create a rule with an action to allow all the outgoing traffic from our network for port 80 (used for HTTP traffic to the Internet).


| Action | Source | Destination | Protocol | Port | Direction |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Allow | 192.168.1.0/24 | Any | TCP | 80 | Outbound |

2. **Deny:**
A rule’s “Deny” action means that the traffic defined inside the rule would be blocked and not permitted. These rules are fundamental for the security team to deny specific traffic coming from malicious IP addresses and create more rules to reduce the threat surface of the network.

For example, let’s create a rule with an action to deny all the incoming traffic on port 22 (used for remotely connecting to a machine via SSH) of our critical server.


| Action | Source | Destination | Protocol | Port | Direction |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Deny | Any | 192.168.1.0/24 | TCP | 22 | Inbound |

3. **Forward:**
The action “Forward” redirects traffic to a different network segment using the forwarding rules created on the firewalls. This applies to the firewalls that provide routing functionality and act as gateways between different network segments.

For example, let’s create a rule with an action to forward all the incoming traffic on port 80 (used for HTTP traffic) to the web server 192.168.1.8.


| Action | Source | Destination | Protocol | Port | Direction |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Forward | Any | 192.168.1.8 | TCP | 80 | Inbound |

# Directionality of Rules
1. **Inbound Rules**
Rules are categorized as inbound rules when they are meant to be applied to incoming traffic only. For example, you might allow incoming HTTP traffic (port 80) on your web server.

2. **Outbound Rules**
These rules are made for outgoing traffic only. For example, blocking all outgoing SMTP traffic (port 25) from all the devices except the mail server.

3. **Forward Rules**
Forwarding rules are created to forward specific traffic inside the network. For example, a forwarding rule can be created to forward the incoming HTTP (port 80) traffic to the web server located in your network.

