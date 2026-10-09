# Frontend and Backend:
1. **HTML**-  (Hypertext Markup Language) is a foundational aspect of web applications. It is a set of instructions or code that instructs a web browser on what to display and how to display it. It could be compared to simple organisms living on the planet; these organisms have DNA, which is the instructions for how simple organisms are put together.

2. **CSS**- (Cascading Style Sheets) in web applications describes a standard appearance, such as certain colours, types of text, and layouts. Continuing the analogy with DNA, these could be compared to the parts of DNA that describe the colour, shape, size, and texture of the simple organism.

3. **JS**- (JavaScript) is part of a web application front end that enables more complex activity in the web browser. Whereas HTML can be considered a simple set of instructions on what to display, JavaScript is a more advanced set of instructions that allows choices and decisions to be made on what to display. In the planet analogy, JavaScript can be considered the brain of an advanced organism, which allows decisions to be made based on what and how something interacts with it.

4. **Database-** A Database is where information can be stored, modified, and retrieved. A web application may want to store and retrieve information about a visitor's preferences on what to show or not; this would be stored in a database. A planet may have more advanced inhabitants who store information about locations in maps, write notes in a diary or put books in a library and files in a filing cabinet.

5. There are many other Infrastructure components underpinning Web Applications, such as web servers, application servers, storage, various networking devices, and other software that support the web application. On a planet, these are the roads that are present, the cars that run on those roads, the fuel that powers the cars.

6. **WAF-**  (Web Application Firewall) is an optional component for web applications. It helps filter out dangerous requests away from the Web Server and provides an element of protection. This could be considered similar to how a planet's atmosphere can protect inhabitants from harmful UV rays.

# URL(Uniform Resource Locator):
A Uniform Resource Locator (URL) is a web address that lets you access all kinds of online content, whether it's a webpage, a video, a photo, or other media. It guides your browser to the right place on the Internet.

## Components of URL:
1. **Scheme-** The scheme is the protocol used to access the website. The most common are HTTP (HyperText Transfer Protocol) and HTTPS (Hypertext Transfer Protocol Secure). HTTPS is more secure because it encrypts the connection, which is why browsers and cyber security experts recommend it. Websites often enforce HTTPS for added protection.

2. **User-** Some URLs can include a user’s login details (usually a username) for sites that require authentication. This happens mostly in URLs that need credentials to access certain resources. However, it’s rare nowadays because putting login details in the URL isn’t very safe—it can expose sensitive information, which is a security risk.

3. **Host/Domain-** The host or domain is the most important part of the URL because it tells you which website you’re accessing. Every domain name has to be unique and is registered through domain registrars. From a security standpoint, look for domain names that appear almost like real ones but have small differences (this is called typosquatting). These fake domains are often used in phishing attacks to trick people into giving up sensitive info.

4. The **port number** helps direct your browser to the right service on the web server. It’s like telling the server which doorway to use for communication. Port numbers range from 1 to 65,535, but the most common are 80 for HTTP and 443 for HTTPS.

5. The **path** points to the specific file or page on the server that you’re trying to access. It’s like a roadmap that shows the browser where to go. Websites need to secure these paths to make sure only authorised users can access sensitive resources.

6. The **query string** is the part of the URL that starts with a question mark (?). It’s often used for things like search terms or form inputs. Since users can modify these query strings, it’s important to handle them securely to prevent attacks like injections, where malicious code could be added.

7. **Fragment-** The fragment starts with a hash symbol (#) and helps point to a specific section of a webpage—like jumping directly to a particular heading or table. Users can modify this too, so like with query strings, it’s important to check and clean up any data here to avoid issues like injection attacks.

# HTTP Request Line
The request line (or start line) is the first part of an HTTP request and tells the server what kind of request it’s dealing with. It has three main parts: the HTTP method, the URL path, and the HTTP version.

Example: METHOD /path HTTP/version

## 1. HTTP Methods:
The HTTP method tells the server what action the user wants to perform on the resource identified by the URL path. Here are some of the most common methods and their possible security issue:

1. **GET-** Used to fetch data from the server without making any changes. Reminder! Make sure you’re only exposing data the user is allowed to see. Avoid putting sensitive info like tokens or passwords in GET requests since they can show up as plaintext.

2. **POST-** Sends data to the server, usually to create or update something. Reminder! Always validate and clean the input to avoid attacks like SQL injection or XSS.

3. **PUT-** Replaces or updates something on the server. Reminder! Make sure the user is authorised to make changes before accepting the request.

4. **DELETE-** Removes something from the server. Reminder! Just like with PUT, make sure only authorised users can delete resources.

5. **PATCH-** Updates part of a resource. It’s useful for making small changes without replacing the whole thing, but always validate the data to avoid inconsistencies.

6. **HEAD-** Works like GET but only retrieves headers, not the full content. It’s handy for checking metadata without downloading the full response.

7. **OPTIONS-** Tells you what methods are available for a specific resource, helping clients understand what they can do with the server.

8. **TRACE-** Similar to OPTIONS, it shows which methods are allowed, often for debugging. Many servers disable it for security reasons.

9. **CONNECT-** Used to create a secure connection, like for HTTPS. It’s not as common but is critical for encrypted communication.

## 2. URL Path:
The URL path tells the server where to find the resource the user is asking for. For instance, in the URL https://tryhackme.com/api/users/123, the path /api/users/123 identifies a specific user.

Attackers often try to manipulate the URL path to exploit vulnerabilities, so it’s crucial to:

A. Validate the URL path to prevent unauthorised access
B. Sanitise the path to avoid injection attacks
C. Protect sensitive data by conducting privacy and risk assessments

## 3. HTTP Version:
1. HTTP/0.9 (1991)
The first version, only supported GET requests.

2. HTTP/1.0 (1996)
Added headers and better support for different types of content, improving caching.

3. HTTP/1.1 (1997)
Brought persistent connections, chunked transfer encoding, and better caching. It’s still widely used today.

4. HTTP/2 (2015)
Introduced features like multiplexing, header compression, and prioritisation for faster performance.

5. HTTP/3 (2022)
Built on HTTP/2, but uses a new protocol (QUIC) for quicker and more secure connections.

6. Although HTTP/2 and HTTP/3 offer better speed and security, many systems still use HTTP/1.1 because it’s well-supported and works with most existing setups. However, upgrading to HTTP/2 or HTTP/3 can provide significant performance and security improvements as more systems adopt them.

# Status Codes and Reason Phrases
1. **Informational Responses (100-199)**
These codes mean the server has received part of the request and is waiting for the rest. It’s a "keep going" signal.

2. **Successful Responses (200-299)**
These codes mean everything worked as expected. The server processed the request and sent back the requested data.

3. **Redirection Messages (300-399)**
These codes tell you that the resource you requested has moved to a different location, usually providing the new URL.

4. **Client Error Responses (400-499)**
These codes indicate a problem with the request. Maybe the URL is wrong, or you’re missing some required info, like authentication.

5. **Server Error Responses (500-599)**
These codes mean the server encountered an error while trying to fulfil the request. These are usually server-side issues and not the client’s fault.

# Common Status Codes
1. **100 (Continue)**
The server got the first part of the request and is ready for the rest.

2. **200 (OK)**
The request was successful, and the server is sending back the requested resource.

3. **301 (Moved Permanently)**
The resource you’re requesting has been permanently moved to a new URL. Use the new URL from now on.

4. **404 (Not Found)**
The server couldn’t find the resource at the given URL. Double-check that you’ve got the right address.

5. **500 (Internal Server Error)**
Something went wrong on the server’s end, and it couldn’t process your request.

# Response Headers extra:
Set-Cookie:
Example: Set-Cookie: sessionId=38af1337es7a8
This one sends cookies from the server to the client, which the client then stores and sends back with future requests. To keep things secure, make sure cookies are set with the HttpOnly flag (so they can’t be accessed by JavaScript) and the Secure flag (so they’re only sent over HTTPS).

Cache-Control:
Example: Cache-Control: max-age=600
This header tells the client how long it can cache the response before checking with the server again. It can also prevent sensitive info from being cached if needed (using no-cache).

Location:
Example: Location: /index.html
This one’s used in redirection (3xx) responses. It tells the client where to go next if the resource has moved. If users can modify this header during requests, be careful to validate and sanitise it—otherwise, you could end up with open redirect vulnerabilities, where attackers can redirect users to harmful sites.

# Security Headers
## 1. Content-Security-Policy(CSP)
A CSP header is an additional security layer that can help mitigate against common attacks like Cross-Site Scripting (XSS). Malicious code could be hosted on a separate website or domain and injected into the vulnerable website. A CSP provides a way for administrators to say what domains or sources are considered safe and provides a layer of mitigation to such attacks.

Within the header itself, you may see properties such as default-src or script-src defined and many more. Each of these give an option to an administrator to define at various levels of granularity, what domains are allowed for what type of content. The use of self is a special keyword that reflects the same domain on which the website is hosted.

