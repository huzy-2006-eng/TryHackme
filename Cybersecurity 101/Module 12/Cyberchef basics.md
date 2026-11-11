CyberChef is a simple, intuitive web-based application designed to help with various “cyber” operation tasks within your web browser. Think of it as a Swiss Army knife for data - like having a toolbox of different tools designed to do a specific task. These tasks range from simple encodings like XOR or Base64 to complex operations like AES encryption or RSA decryption. CyberChef operates on recipes, a series of operations executed in order.

# The Operations Area

| Operations | Description | Examples |
| :--- | :--- | :--- |
| From Morse Code | Translates Morse Code into (upper case) alphanumeric characters. | `---- . . . . - - . . - - . . .` becomes `THREATS` when used with default parameters |
| URL Encode | Encodes problematic characters into percent-encoding, a format supported by URIs/URLs. | `https://tryhackme.com/r/room/cyberchefbasics` becomes `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Froom%2Fcyberchefbasics` when used with the parameter “Encode all special chars” |
| To Base64 | This operation encodes raw data into an ASCII Base64 string. | `This is fun!` becomes `VGhpcyBpcyBmdW4h` |
| To Hex | Converts the input string to hexadecimal bytes separated by the specified delimiter. | `This Hex conversion is awesome!` becomes `54 68 69 73 20 48 65 78 20 63 6f 6e 76 65 72 73 69 6f 6e 20 69 73 20 61 77 65 73 6f 6d 65 21` |
| To Decimal | Converts the input data to an ordinal integer array. | `This Decimal conversion is awesome!` becomes `84 104 105 115 32 68 101 99 105 109 97 108 32 99 111 110 118 101 114 115 105 111 110 32 105 115 32 97 119 101 115 111 109 101 33` |
| ROT13 | A simple Caesar substitution cipher which rotates alphabet characters by the specified amount (default 13). | `Digital Forensics and Incident Response` becomes `Qvtvtny Sbernsvpf naq Vapvqrag Erfcbafr` |

# The Recipe Area
This is considered as the heart of the tool. In this area, you can seamlessly select, arrange, and fine-tune operations to suit your needs. This is where you take control, defining each operation's arguments and options precisely and purposefully.

 The recipe area is a designated space to select and arrange specific operations and then define their respective arguments and options to customize their behaviour further. In the recipe area, you can drag the operations you want to use and specify arguments and options.

Features include the following:

**Save recipe:** This feature allows the user to save selected operations.
**Load recipe:** Allows the user to load previously saved recipes.
**Clear Recipe:** This feature will enable users to clear the chosen recipe during usage.

The bottom part of the image above is the BAKE! button. This processes the data with the given recipe.

Additionally, you can tick the Auto Bake checkbox. This feature allows users to automatically cook using the selected recipe without manually clicking BAKE! every time.

# CyberChef Steps
1. Setting a clear objective is essential. This step involves defining specific and achievable goals. It helps answer the question, "What do I want to accomplish?". Objectives are vital in providing direction, purpose, and focus to your goals. One example would be, "During a security investigation, I found a gibberish string; I want to know what hidden message it contains if it has one."

2. Next, put your data into the input area. In this step, you use your data. This is where you paste or upload the gibberish string that you found.

3. The third step is to select the Operations you want to use. This can be tricky if you are not familiar yet with what you are dealing with. Following our example, we are still determining what to use to understand this gibberish string. During our research, we found relevant information that this gibberish string might be using anything related to encryption. Therefore, we decided to use any operations under the Encryption/Encoding category, including but not limited to ROT13, Base64, Base85, or ROT47. Note that we can use a lot of operations under this category. 

4. Lastly, check the output to see if it is the intended result. This begs the question, "Have we achieved our objective?". In our example, it would mean, were we able to decode the gibberish string we found? If yes, then that's it! If not, we may need to repeat the steps that we have taken.

# Extractors

| Specific | Description |
| :--- | :--- |
| Extract IP addresses | Extracts all IPv4 and IPv6 addresses. |
| Extract URLs | Extracts Uniform Resource Locators (URLs) from the input. The protocol (HTTP, FTP, etc.) is required, otherwise there will be far too many false positives. |
| Extract email addresses | Extracts all email addresses from the input. |

# Date and Time

| Specific | Description |
| :--- | :--- |
| From UNIX Timestamp | Converts a UNIX timestamp to a datetime string. |
| To UNIX Timestamp | Parses a datetime string in UTC and returns the corresponding UNIX timestamp. |

A UNIX timestamp is a 32-bit value representing the number of seconds since January 1, 1970 UTC (the UNIX epoch). To convert "Fri Sep 6 20:30:22 +04 2024" into a UNIX Timestamp, use the operations To UNIX Timestamp, where the result would be 1725654622. If you wish to convert it back to a more readable format, you can use From UNIX Timestamp.

# Data Format

| Operations | Description | Examples |
| :--- | :--- | :--- |
| From Base64 | This operation decodes data from an ASCII Base64 string back into its raw format. | `V2VsY29tZSB0byB0cnloYWNrbWUh` becomes `Welcome to tryhackme!` |
| URL Decode | Converts URI/URL percent-encoded characters back to their raw values. | `https%3A%2F%2Ffgchq%2Egithub%2Eio%2FCyberChef%2F` becomes `https://gchq.github.io/CyberChef/` |
| From Base85 | notation for encoding arbitrary byte data. It is usually more efficient than Base64. This operation decodes data from an ASCII string (with an alphabet of your choosing, presets included). | `B0u!rDjj7BEbo7` becomes `hello world` |
| From Base58 | is a notation for encoding arbitrary byte data. It differs from Base64 by removing efficiently misread characters (i.e. l, I, 0, and O) to improve human readability. | `AXLU7qR` becomes `Thm58` |
| To Base62 | is a notation for encoding arbitrary byte data using a restricted set of symbols that humans can conveniently use and process by computers. The high number base results in shorter strings than with the decimal or hexadecimal system | `Thm62` becomes `6NiRKOY` |

Operations such as Base(64, 85, 58, 62) are known as base encodings. Base encoding takes binary data (strings of 0s and 1s) and transforms it into a text-based representation using a specific set of ASCII (American Standard Code for Information Interchange) characters.

# Example
 Let's say we have to encode "THM":
**Step 1:** Convert to Binary and Merge (Manually)

T = 01010100, H=01001000, M = 01001101. Next, concatenate these binaries and make sure they have 24 characters. You should have 010101000100100001001101

**Step 2:** Divide and convert to Decimal
Separate 010101000100100001001101 into 6 characters each. You should have 010101 000100 100001 001101. These are 6-bit characters; we should have four instances of this now. We need to convert each instance to Decimal. Let's convert, then!

**Step 3:** Convert to Base64
Now that we have the Numbers from the previous step, which are 21, 4, 33, and 13, let's look for the equivalent characters from our table below. This table represents a base64 index table.

