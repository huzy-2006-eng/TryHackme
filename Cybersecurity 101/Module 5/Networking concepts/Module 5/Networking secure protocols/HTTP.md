After resolving the domain name to an IP address, the client will carry out two steps:
1. Establish a TCP three-way handshake with the target server.
2. Communicate using the HTTP protocol;
for example, issue HTTP requests, such as GET /HTTP/1.1

# HTTP over TLS:
HTTPS stands for Hypertext Transfer Protocol Secure. It is basically HTTP over TLS. Consequently, requesting a page over HTTPS will require the following three steps (after resolving the domain name):

1. Establish a TCP three-way handshake with the target server.
2. Establish a TLS session.
3. Communicate using the HTTP protocol; for example, issue HTTP requests, such as GET / HTTP/1.1

# Getting the Encryption key:
1. Adding TLS to HTTP leads to all the packets being encryted.
2. We can no longer see the contents of the exchanged packets unless we get access to the private key.
3. After providing the decryption key and runnng it again, we conclude that TCP and TLS handshakes don't change; the main difference starts with the HTTP protocol GET.

#### The key takeway is that TLS offered security for HTTP without requiring any changes in the lower or higher layer protocols.
#### TCP and IP were not modified, while HTTP was sent over TLS the way it would be sent over TCP.