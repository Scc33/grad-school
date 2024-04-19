# Week 2: Communication and Virtual Private Clouds

# Cloud Computing Glue

- Cloud computing is about running compute task and storing data on other computers
- Have we seen this problem before?
    - Yes, inter-process communication, communication on a local network, communication on the internet

# Communication, Internet Protocol, HTTP, REST

## Communication: Single-node Networked

- Communication in single machine
    - Shared memory block, shared file system, signals, POSIX sockets (eg SOCK_DGRAM), Remote method invocation (RMI - java processes call methods in other JVM), message queue, message passing (Unix pipe)
- Middleware
    - Software providing services to application beyond available from OS
    - Middleware can provide abstractions which makes building distributed applications feel more like single-node programs
        
        ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled.png)
        
- RPC frameworks
    - RPC - remote procedure call
    - Simple solutions like Java RMI don’t work at large scale because of failures, network traffic, etc
    - Apache Thrift
    - Google Protocol Buffer
        - Define functions that will be called remotely and then compile
        - Compilation generates automated code which handles communication (serialization, marshaling, network calls, reviving)

## IP, HTTP, RPC on HTTP

- 5 level model (from CS 435)
    - Application, transport, IP, Link, data
        
        ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%201.png)
        
    - Transport layer handles packetizing data and typically implemented at OS level
        - TCP - guarantees all bytes received are identical to those are sent, UDP
    - Application layer
        - HTTP/HTTPS (RESTful), FTP, WebSocket, SMTP, DNS, SSH, etc
- HTTP Protocol
    - Originally targeted static web pages: ***Client requests, server responds, connection is closed***
    - Works on top of TCP for reliable transport (HTTP1/HTTP2)
    - HTTP resources are identified and located on network by Uniform Resource Locators (URLs) using Uniform Resource Identifiers (URIs)
        
        ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%202.png)
        
    - HTTP/1.0 used separate connection to server for every resource, HTTP/1.1 can reuse TCP connection multiple times (persistent sessions)
    - HTTP message formate
        - Request verbs
            - GET, POST, PUT, DELETE, PATCH, etc
        - Request message
            - Request header fields, empty line, optional message body
        - Response message
            - A status line indicated response code, response header fields, empty line, optional message body
    - RPC on HTTP
        - For many types of RPC the client/server conversation is fine
        - Replace HTML markup with XML or JSON (JSON-RPC) for representation of data
            - Example Bitcoin server uses JSON-RPC

## RESTful Architecture

- A style of software architecture
- URI addressable resources, accessible via HTTP
    
    ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%203.png)
    
- GET is safe (does not change state)
- GET, PUT, DELETE are idempotent
    - You can execute them more than once and get the same state change result
- The key abstraction of information in REST is a resource which becomes just a mapping to some URI
- POST creates a resource, PUT updates a resource
    
    ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%204.png)
    

## Service Oriented Architecture and SOAP

- SOA
    - SOA is a philosophy of encapsulating application logic in services with uniform interface and making public available via discovery mechanism
    - Benefits: reusable code, interaction, scalability, reduce costs
- SOAP - service oriented architecture protocol
    - SOAP is web based APIs using XML validation
        - XML schemas provisioned with WSDL documents
        - Schemas could get very involved
    - Evolved as successor to XML-RPC
    - Because it follows objects, rules, and constraints SOAP is more strict protocol than REST
    - Microservices architecture is very similar to SOA (SOA 2000-2010) and Microservices (2015-)
        - Containerization, agile, CICD, asynchronous programming all enabled microservices
            
            ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%205.png)
            

## Asynchronous RPC and WebSocket

- Using old HTTP (.9/1.0/1.1) what if remote server takes a long time? Well we could keep polling the server periodically but not a good solution
- Web 2.0 brought bidirectional client/server communication
    - Asynchronous RPC aka streaming API
    - Example: AJAX, jQuery
- RPC libraries can issue asynchronous methods to the server and server can inform them of the response later
    - Use cases: Google docs, chats, multiplayer. games, stock price updates, etc
- WebSocket protocol
    - WebSocket is an application protocol running on top of TCP
        - Purely event driven and application listens for events on the web socket
        - Asynchronous communication in networked environment requires handling faults
    - Uses ws:// or wss:// (secure)
    - Uses an initial HTTP session and port to process handshake
        - Opening handshake (HTTP to start then after handshake it ‘upgrades’ to ws)
        - Data handshake
        - Closing handshake
    - There're four different events in WebSocket:
        - Open - fires to establish a connection
        - Message - contains the data from the server
        - Error - fires in response to an unexpected event (failure)
        - Close - fires when the WebSocket connection is closed
        
        ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%206.png)
        

## HTTP2 Push, Streaming Video

- Added server push and data streaming
    - New data in a new stream to the browser stored in a cache
    - HTTP/2 utilizes server-side events
- AWS API Gateway has support for all types of API requests
    - REST, WebSocket, HTTP

# Virtual Private Clouds

## VPC - Virtual Private Clouds

- Network virtualization solution
    - Amazon Virtual Private Cloud (VPC), Microsoft Azure Virtual Network (VNECT), Google Virtual Private Cloud (VPC)
- More important to cloud architecture than cloud development
- Goal: isolate different customers’ network packets from each other
- In AWS a VPC is associated with a region
    - VPC has range of available IP addresses known as a CIDR range
    - Your VPC is subdivided into logically separate segments
    - Subnets and each subnet gets a smaller CIDR range
    - Instances (EC2, RDS, etc) can be launched in a subnet
        
        ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%207.png)
        
- CIDR - classless inter-domain routing, method of allocating IP address ranges
    - Mask will keep so many bits the same while the lower bits can change (same idea as subnets from 435)
    - 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 reserved for private internets
    - First four IP addresses and last IP address in each subnet are reserved
        - 10.0.0.0 - network address
        - 10.0.0.1 - VPC router
        - 10.0.0.3 - reserved for future use
        - 10.0.0.255 - network broadcast address
            
            ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%208.png)
            

## VPC Subnets

- Example - a public subnet to host internet-facing resources and a private subnet for databases that accept requests
- Can create multiple subnets in multiple AZs to ensure high availability
- Private subnets - any incoming traffic from internet cannot directly access the resources
    - Technically a subnet is private if there is no route in the routing table to the wider internet
- Public subnet has access to internet gateway defined in routing table
    - Each resource in public subnet gets a private IP within CIDR range and a public IP accessible from the internet
- Each VPC has associate “Main Route Table”
    - Default VPC has route in its “Main Route Table” to an internet gateway
    - Subnets can have their own custom route table
    - Selection of the optimum route for a network is done based on longest prefix match

## VPC Gateways

- Internet gateway is a logical construct not a specified instance or resource
    - AWS does behind the scenes work to allow highly available gateway and attached to VPC
- NAT Gateways
    - Network address translation
    - Virtual router or gateway in a public subnet that enables instances in private subnet to interact with the internet
    - Modifies the network address information in the IP header
        - When a reply is received from the internet it changes the reply-to address from IP address to EC2 private IP address
    - Two types of NAT
        - NAT Instance - runs as an EC2 Instance
        - NAT Gateway - fully managed by AWS, requires elastic IP
- Bastion Host - used to access private machines hosted in a private network in a VPC
    - Server whose purpose is to provide access to private network from external network
    - Minimizes the chances of penetration
    
    ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%209.png)
    

## Advanced VPC Gateways

- Virtual private gateway
    - If subnet doesn’t have a route to the internet gateway but has traffic routed to virtual private gateway for site-to-site VPN known as a VPN only subnet
        
        ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%2010.png)
        
- VPC Peering
    - Make connection between VPCs within same account or different account in same or different region
    - VPC endpoints
        - Generally AWS services are different entities and do not allow for direct communication without going through IGW, NAT, VPN, or AWS Direct connect
        - VPC endpoint enables private connections between services which improves bandwidth and security
            
            ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%2011.png)
            
- Routing in VPC vs Physical network
    - Amazon backend intercepts any MAC ARP request, looks up routing tables, and returns the destination without implementing ARP

## VPC Security and Firewalls

- AWS offers two types of security
    - Security groups
        - EC2 instance level firewall
        - Can be gradual to the IP and incoming vs outgoing
        - Security groups IDs can be specified as a source IP to allow communication from all instances that are attached to that security group
    - Network access control lists (NACL)
        - Subnet firewall
        - Every VPC has a default NACL
        - NACL rules are evaluated based on rule numbers starting at the lowest number to the highest number
            
            ![Untitled](Week%202%20Communication%20and%20Virtual%20Private%20Clouds%209f8b029aafc748f893909ca8fd115ff9/Untitled%2012.png)
            
- Flow logs
    - Logs all of the networking which can be used for auditing

# Quiz

- What Communication framework or technology do many Big Data systems use, and why?
    - Apache Thrift, because it is scalable and easy to use the auto-generated RPC functions.
- Which of the following technologies are transport layer systems in the Internet Protocol?
    - UDP, TCP
- What are the event types in WebSocket?
    - Open, close, error, message
- Under which scenario would we be better off using HTTP Streaming API?
    - In a massive multiplayer game
- What is the function of Middleware?
    - Software that provides services to applications beyond those generally available at the operating system.
    - Middleware is a type of computer software that provides services to software applications beyond those available from the operating system. It can be described as "software glue".
- “Data representation for (un)marshalling on different machines and programming languages”
    - XML
    - The fundamental format of XML is standardized, if you share or transmit XML across systems or platforms, either locally or over the internet, the recipient can still parse the data due to the standardized XML syntax.
- Which technology will address the following need? “Create, Update, Read, and Remove objects over the web”
    - REST
- Which technology can best address the following need? “Human readable representation of data”
    - JSON
- “Send method execution requests to a remote object”
    - SOAP
    - SOAP is a remote procedure call technology.
- What HTTP verbs are used in RESTful APIs?
    - **PUT, GET, DELETE**