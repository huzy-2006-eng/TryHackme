1. For secure commuication SSL (Secure Sockets Layer) was introduced.
2.  After that TLS (Transport Layer Security) was created.
3. Like SSL, TLS is a cryptographic protocol operating at the OSI model's transport layer.
4. It allows secure communication between a client and a server over an insecure network.
5. By secure, we refer to confidentiality and integrity; TLS ensures no one can read or modify the exchanged data.
6. All other protocls have become secured because of TLS.

# PROCESS OF TLS:
1. The first step for every server(or client) that needs t identify itself is to get a Certificate Signing Request(CSR) and submits it to Certificate Authority(CA); the CA verifies the CSR and issues a digital certificate.

2. Once the signed certificate is received , it can be used to identify the server to others, who can confirm the validity of the signature.

3. For a host to confirm the validity, the certificates of the signing authorities need to be installed on the host.

4. In the non-digital world, this is similar to recognising the stamps of various authorities. The screenshot below shows the trusted authorities installed in a web browser.

5. A self-signed certificate cannot prove the server’s authenticity as no third party has confirmed it.

