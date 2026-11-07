1. **Authentication:** You want to be sure you communicate with the right person, not someone else pretending.
2. **Authenticity:** You can verify that the information comes from the claimed source.
3. **Integrity:** You must ensure that no one changes the data you exchange.
4. **Confidentiality:** You want to prevent an unauthorised party from eavesdropping on your conversations.

# Asymmetric encryption:
Exchanging keys for symmetric encryption is a widespread use of asymmetric cryptography. Asymmetric encryption is relatively slow compared to symmetric encryption; therefore, we rely on asymmetric encryption to negotiate and agree on symmetric encryption ciphers and keys.

# RSA:
RSA is a public-key encryption algorithm that enables secure data transmission over insecure channels. With an insecure channel, we expect adversaries to eavesdrop on it.

# Diffie-Hellman Key Exchange:
iffie-Hellman Key Exchange is often used alongside RSA public key cryptography. Diffie-Hellman is used for key agreement, while RSA is used for digital signatures, key transport, and authentication, among many others. For instance, RSA helps prove the identity of the person you’re talking to via digital signing, as you can confirm based on their public key. This would prevent someone from attacking the connection with a man-in-the-middle attack against Alice by pretending to be Bob. In brief, Diffie-Hellman and RSA are incorporated into many security protocols and standards to provide a comprehensive security solution.

# SSH(Secure Shell)-
In the above interaction, the SSH client confirms whether we recognise the server’s public key fingerprint. ED25519 is the public-key algorithm used for digital signature generation and verification in this example. Our SSH client didn’t recognise this key and is asking us to confirm whether we want to continue with the connection. This warning is because a man-in-the-middle attack is probable; a malicious server might have intercepted the connection and replied, pretending to be the target server.

In this case, the user must authenticate the server, i.e., confirm the server’s identity by checking the public key signature. Once you answer with “yes”, the SSH client will record this public key signature for this host. In the future, it will connect you silently unless this host replies with a different public key.

**At some point, one will surely hit a machine with SSH configured with key authentication instead. This authentication uses public and private keys to prove the client is a valid and authorised user on the server. By default, SSH keys are RSA keys. You can choose which algorithm to generate and add a passphrase to encrypt the SSH key.**

# Using SSH keys to get a "Better Shell":
During CTFs, penetration testing, and red teaming exercises, SSH keys are an excellent way to “upgrade” a reverse shell, assuming the user has login enabled. Note that www-data usually does not allow this, but regular users and root will work. Leaving an SSH key in the authorized_keys file on a machine can be a useful backdoor, and you don’t need to deal with any of the issues of unstabilised reverse shells like Control-C or lack of tab completion.

# Digital Signature:
Digital signatures provide a way to verify the authenticity and integrity of a digital message or document. Proving the authenticity of files means we know who created or modified them. Using asymmetric cryptography, you produce a signature with your private key, which can be verified using your public key. Only you should have access to your private key, which proves you signed the file. In many modern countries, digital and physical signatures have the same legal value.

 it is a chain; for example, the certificate is signed by an organisation, the organisation is trusted by a CA, and the CA is trusted by your browser. Therefore, your browser trusts the certificate

 