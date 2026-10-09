1. Although it is very convenient to log in and administer remote systems, it is risky when all the traffic is sent in cleartext.
2. It is easy for anyone monitoring for network traffic to get hold of your login credentials once u use telnet.
3. That is why OpenBSD developers released OpenSSH, an open-source implementation of SSH.

# Benefits of OpenSSH:
1. ### Secure authentication:
Besides password-based authentication, SSH supports public key and two-factor authenticaton.

2. ### Confidentiality:
OpenSSH provides end-to-end encryption, protecting against eavesdropping.
Furthermore, it notifies you of new server keys to protect against man-in-the-middle attacks.

3. ### Integrity:
 In addition to protecting the confidentiality of the exchanged data, cryptography also protects the integrity of the traffic.

4. ### Tunneling:
SSH can create a secure "tunnel" to route other protocols through SSH.
This setup leads to a VPN-like connection.

5. ### X11 Forwarding:
If u connect to a Unix-sytem with a GUI, SSH allows u to used the GUI over the network.

