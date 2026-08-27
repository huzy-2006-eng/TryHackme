Consider the scenario where you just downloaded a 6 GB file and want to know whether the copy you downloaded is identical to the original file, bit for bit. How would you do that? Or if a good Samaritan handed you this 6 GB file on a USB memory drive, how can you be sure it is identical to the file you want to download?

**A hash value** is a fixed-size string or characters that is computed by a hash function. A **hash function** takes an input of an arbitrary size and returns an output of fixed length, i.e., a hash value. We will cover various exciting and clever uses of hash functions and values in this room.

# Hash Function:
1. Hash functions are different from encryption. There is no key, and it’s meant to be impossible (or computationally impractical) to go from the output back to the input.

2. A hash function takes some input data of any size and creates a summary or digest of that data. The output has a fixed size. It’s hard to predict the output for any input and vice versa. Good hashing algorithms will be relatively fast to compute and prohibitively slow to reverse, i.e., go from the output and determine the input. Any slight change in the input data, even a single bit, should cause a significant change in the output.

# Why is Hashing important?
1. Hashing plays a vital role in our daily use of the Internet. Like other cryptographic functions, hashing remains hidden from the user. Hashing helps protect data’s integrity and ensure password confidentiality.

2. Consider this example of hashing being used to protect your cyber security. When you log into TryHackMe, the server uses hashing to verify your password. In fact, as per good security practices, a server does not record your password; it records the hash value of your password. Whenever you want to log in, it will calculate the hash value of the password you submitted with the recorded hash value. Similarly, when you log into your computer, hashing plays a role in verifying your password. You interact more indirectly with hashing than you would think, and almost daily in the context of passwords.

# Hash Collision:
1. A hash collision is when two different inputs give the same output. Hash functions are designed to avoid collisions as best as possible. Furthermore, hash functions are designed to prevent an attacker from being able to create, i.e., engineer, a collision intentionally. However, because the number of inputs is practically unlimited and the number of possible outputs is limited, this leads to a pigeonhole effect.

2. The pigeonhole effect states that the number of items (pigeons) is more than the number of containers (pigeonholes); some containers must hold more than one item. In other words, in this context, there are a fixed number of different output values for the hash function, but you can give it any size input. As there are more inputs than outputs, some inputs must inevitably give the same output. If you have 21 pigeons and 16 pigeonholes, some of the pigeons are going to share the pigeonholes. Consequently, collisions are unavoidable. However, a good hash function ensures that the probability of a collision is negligible.

3. MD5 and SHA1 have been attacked and are now considered insecure due to the ability to engineer hash collisions. However, no attack has yet given a collision in both algorithms simultaneously, so if you compare the MD5 and SHA1 hash, you will see that they’re different. You can view the MD5 collision example on the MD5 Collision Demo(opens in new tab) page; furthermore, you can read the details of the SHA1 collision attack at Shattered(opens in new tab). Due to these, you shouldn’t trust either algorithm for hashing passwords or data.

# Stories of Insecure Password Storage for Authentication
1. ### Storing Passwords in Plaintext
Quite a few data breaches have leaked plaintext passwords. You’re probably familiar with the “rockyou.txt” password list on Kali Linux, among many other offensive security distributions. This password list came from RockYou, a company that developed social media applications and widgets. They stored their passwords in plaintext, and the company had a data breach. The text file contains over 14 million passwords. 

2. ### Using an Insecure Encryption Algorithm
Adobe’s notable data breach was slightly different. Instead of using a secure hashing function to store the hash values of the passwords, the company used a deprecated encryption format. Furthermore, password hints were stored in plain text, sometimes containing the password itself. Consequently, the plaintext password could be retrieved relatively quickly.

3. ### Using an Insecure Hash Function
LinkedIn also suffered a data breach in 2012. LinkedIn used an insecure hashing algorithm, the SHA-1, to store user passwords. Furthermore, no password salting was used. Password salting refers to adding a salt, i.e., a random value, to the password before it is hashed.

