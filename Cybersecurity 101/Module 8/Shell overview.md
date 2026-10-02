# Shell Introduction:
A shell is software that allows a user to interact with an OS. It can be a graphical interface, but it is usually a command-line interface, and this will depend on the operating system running on the target system.

In cyber security, it commonly refers to a specific shell session an attacker uses when accessing a compromised system, allowing them to run commands and execute software. This will allow attackers to execute several activities, some of which are described below.

1. **Remote System Control:** allows the attacker to execute commands or software remotely in the target system.

2. **Privilege Escalation:** If initial access through a shell is limited or restricted, attackers can explore ways to escalate privileges to more elevated or administrative access.

3. **Data Exfiltration:** Once attackers have access to execute commands through an obtained shell, they can explore the system to read and copy sensitive data from it.

4. **Persistence and Maintenance Access:** Once shell access is obtained, attackers can create access through users and credentials or copy backdoor software to maintain access to the target system for later usage.

5. **Post-Exploitation Activities:** After access to a shell is granted, attackers can perform a wide range of post-exploitation activities, such as deploying malware, creating hidden accounts, and deleting information.

6. **Access Other Systems on the Network:** Depending on the attacker's intentions, the obtained shell can be just an initial access point. The goal can be to hop through the network to a different target using the obtained shell as a pivot to different points in the compromised system network. This is also known as pivoting.

# Reverse Shell
1. A reverse shell, sometimes referred to as a "connect back shell", is one of the most popular techniques for gaining access to a system in cyberattacks.

2. The connections initiate from the initiate from the target system to the attacker's machine, which can help avoid detection from network firewalls and other security appliances.

# How Reverse Shells Work
##  Set up a Netcat(nc) Listener
A reverse shell will connect back to the attacker's machine. This machine will be waiting for a connection, so let's use Netcat to listen to a connection using the following command nc -lvnp 443.

The command above uses the -l option to indicate Netcat to listen or wait for a connection. The -v option enables verbose mode. The -n option prevents the connections from using DNS for lookup, so it will not resolve any hostname it will use an IP address. Finally, the -p flag indicates the port that will be used to wait for the connection, in the case above, port 443.

Any port can be used to wait for a connection, but attackers and pentesters tend to use known ports used by other applications like 53, 80, 8080, 443, 139, or 445. This is to blend the reverse shell with legitimate traffic and avoid detection by security appliances.

# Web Shell
A web shell is a script written in a language supported by a compromised web server that executes commands through the web server itself. A web shell is usually a file containing the code that executes commands and handles files. It can be hidden within a compromised web application or service, making it difficult to detect and very popular among attackers.

Web shells can be written in several languages supported by web servers, like PHP, ASP, JSP, and even simple CGI scripts. 

### Example Web Shell
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>

1. The above shell can be saved into a file with the PHP extension, like shell.php, and then uploaded into the web server by the attacker by exploiting vulnerabilities such as Unrestricted File Upload, File Inclusion, Command Injection, among others, or by gaining unauthorized access to it. 

2. After the web shell is deployed in the server, it can be accessed through the URL where the web shell is hosted, in this example http://victim.com/uploads/shell.php. 

3. As we observed from the code in shell.php, we need to provide a GET method and the value of the variable cmd, which should contain the command the attacker wants to execute. For example, if we want to execute the command whoami the request to the URL should be:

4. http://victim.com/uploads/shell.php?cmd=whoami
The above will execute the command whoami and display the result in the web browser.


