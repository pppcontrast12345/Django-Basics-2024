1.0 Internet and HTTP
---------------------------------------------------------
What is the Internet?

&nbsp;&nbsp;&nbsp;&nbsp;▪ *Vast network that connects billions of devices together all over the globe.*

---------------------------------------------------------
Network
---------------------------------------------------------
&nbsp;&nbsp;&nbsp;&nbsp;▪ *Network is a group of two or more devices that
can communicate.*

---------------------------------------------------------
Web Server Work Model
---------------------------------------------------------

	Client (Browser/App)  ->  Web Server (Nginx/Apache)  ->  Technology Stack (Node.js/Flask/Django)
	         |                        |                             |
	         V                        V                             V
	  HTTP Request (GET/POST)  ->  Application Logic ->  Query Database (SQL/NoSQL)
	         |                        |                             |
	         V                        V                             V
	   HTTP Response       <------- Processed Data  <------- Query Result
	   (HTML/JSON/Other)

&nbsp;&nbsp;&nbsp;&nbsp;▪ *Servers are the machines that provide services to
other machines.*

&nbsp;&nbsp;&nbsp;&nbsp;▪ *Clients are the machines that are used to connect to
those services.*

---------------------------------------------------------
Network Protocol
---------------------------------------------------------
▪ *Set of rules and standards, that allow communication
between network devices.*

▪ *Include mechanisms for devices to identify and make
connections with each other.*

▪ Example for standard network protocols:
  
&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>TCP, UDP, IP, ARP</strong>
  
&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>HTTP, FTP, TFTP, SMTP, SSH</strong>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ IP (Internet Protocol): Handles addressing and routing of packets.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ TCP (Transmission Control Protocol): Ensures reliable data transmission.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ UDP (User Datagram Protocol): Used for faster but less reliable communication.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ HTTP (Hypertext Transfer Protocol): Used for web communication.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▪ FTP (File Transfer Protocol): Used for transferring files.

---------------------------------------------------------
Packets
---------------------------------------------------------

▪ *Every message, file or stream of information sent over
computer networks is broken down into small chunks
called <strong>packets</strong>.*

▪ *Each packet contains important information inside of it
called a header:*

&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>Contents</strong>

&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>Origin</strong>

&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>Destination</strong>

---------------------------------------------------------
HTTP Request Methods
---------------------------------------------------------

Method Description:

&nbsp;&nbsp;&nbsp;▪ POST Create / store a resource


&nbsp;&nbsp;&nbsp;▪ GET Read / retrieve a resource


&nbsp;&nbsp;&nbsp;▪ PUT Update / modify a resource


&nbsp;&nbsp;&nbsp;▪ DELETE Delete / remove a resource

<strong>Other HTTP Methods:</strong>

&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>CONNECT</strong> - method is used to establish a tunnel to a server, usually for protocols that require full-duplex communication, such as HTTPS.

How it works: *Typically, it’s used by proxies to create a network connection between the client and the server. It’s most commonly associated with SSL/TLS connections (encrypted HTTP connections).*


&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>HEAD</strong> -  is similar to GET, but it only retrieves the headers of the response, not the body.


Use case: *This method is used to gather metadata (such as content type, length, etc.) about a resource without downloading the actual content. It's useful for checking if a resource exists, its status, or other properties.*


&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>OPTIONS</strong> -  is used to describe the communication options for the target resource or server.

Use case: *It's often used to discover allowed HTTP methods for a specific resource or server, and to check for cross-origin resource sharing (CORS) support.*


&nbsp;&nbsp;&nbsp;&nbsp;▪ <strong>TRACE</strong> - method is used for diagnostic purposes. It allows the client to see what data (headers) has been received by the server and what the response would look like (echoed back by the server).

How it works: *It performs a loopback test along the path to the target resource. The server sends back the request in the response body, allowing the client to see any changes or transformations made by any intermediate proxies.*

---------------------------------------------------------
URL (URL Uniform Resource Locator)
---------------------------------------------------------

&nbsp;&nbsp;&nbsp;▪ A URL is a reference to a web resource that specifies its location
on a network and a mechanism for retrieving it

&nbsp;&nbsp;&nbsp;▪ A URL is a specific type of URI (Uniform Resource Identifier)

&nbsp;&nbsp;&nbsp;http://&nbsp;&nbsp;&nbsp;localhost:&nbsp;&nbsp;&nbsp;8080&nbsp;&nbsp;&nbsp;/demo/index.html&nbsp;&nbsp;&nbsp;?id=27&lang=en&nbsp;&nbsp;&nbsp;#lecture

&nbsp;&nbsp;&nbsp;[protocol]&nbsp;&nbsp;&nbsp;[ host]&nbsp;&nbsp;&nbsp;[port]&nbsp;&nbsp;&nbsp;[path]&nbsp;&nbsp;&nbsp;[query string]&nbsp;&nbsp;&nbsp;[fragment]

&nbsp;&nbsp;&nbsp;&nbsp; ▪ host - *domain name or the IP address of the server where the resource is located.*

&nbsp;&nbsp;&nbsp;&nbsp;  ▪ port - *port is a number that identifies a specific process or service running on the
server.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ path - *specifies the location of the resource on the server.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ query string - *contains parameters that provide additional data to the server.*

&nbsp;&nbsp;&nbsp;&nbsp; ▪ fragment - *points to a specific section within the page.*

---------------------------------------------------------
MIME (Multi-Purpose Internet Mail Extensions)
---------------------------------------------------------

&nbsp;&nbsp;&nbsp;▪ *Internet standard for encoding resources.*

&nbsp;&nbsp;&nbsp;▪ *Originally developed for email attachments.*

&nbsp;&nbsp;&nbsp;▪ *Used in many Internet protocols like HTTP and SMTP.*

<strong>MIME Type / Subtype Description:</strong>

&nbsp;&nbsp;&nbsp;&nbsp;▪ application/json JSON data

&nbsp;&nbsp;&nbsp;&nbsp;▪ image/png PNG image

&nbsp;&nbsp;&nbsp;&nbsp;▪ image/gif GIF image

&nbsp;&nbsp;&nbsp;&nbsp;▪ text/html HTML

&nbsp;&nbsp;&nbsp;&nbsp;▪ text/plain Text

&nbsp;&nbsp;&nbsp;&nbsp;▪ text/xml XML

&nbsp;&nbsp;&nbsp;&nbsp;▪ video/mp4 MP4 video

&nbsp;&nbsp;&nbsp;▪ application/pdf PDF document

---------------------------------------------------------
HTTP Response Codes
---------------------------------------------------------

▪ HTTP response code classes:

&nbsp;&nbsp;&nbsp;&nbsp;▪ 1xx: informational (e.g., <strong>"100 Continue"</strong>)

&nbsp;&nbsp;&nbsp;&nbsp;▪ 2xx: successful (e.g., <strong>"200 OK", "201 Created"</strong>)

&nbsp;&nbsp;&nbsp;&nbsp;▪ 3xx: redirection (e.g., <strong>"304 Not Modified", "301 Moved
Permanently", "302 Found"</strong>)

&nbsp;&nbsp;&nbsp;&nbsp;▪ 4xx: client error (e.g., <strong>"400 Bad Request", "404 Not
Found", "401 Unauthorized", "409 Conflict"</strong>)

&nbsp;&nbsp;&nbsp;&nbsp;▪ 5xx: server error (e.g., <strong>"500 Internal Server Error",
"503 Service Unavailable"</strong>)





