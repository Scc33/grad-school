# Week 1 - Internet Basics

### Date: August 23, 2022

### Topic: What is the Internet?

### Recall

Protocol

RFC (request for comments)

Layer

Autonomous system

Life of a packet

IP (internet protocol)

TCP

Intradomain routing

Interdomain routing

Forwarding

Layers of the internet

### Notes

- A set of rules for parties to interact to achieve some goal
- Internet engineering task force uses these to design standardization of internet protocols
- Application (HTTP), Transport, Network, Data Link, Physical (each layer building on the one below)
- Class starts at networking and builds up from there
- Internet is a network of networks, with each autonomous system having an AS number
- The internet is a shared channel so their is other people’s data going down the same pipeline as yours
- Options for sharing: circuit switching (divide capacity for each channel), packet switching (chops data into small chunks that can be transmitted independently)
    - Packet switching has no guarantee of available resources, packets could get lost, reordered, or capacity could change (TCP transmission control protocol handles packets, unreliable datagram interface)
- TCP is part of the transport layer and it handles ordering delivery, abstracting byte stream, and congestion control
- Gives “best effort” datagram abstraction to the higher protocols like TCP and can remain independent of underlying communication medium
- Provides hierarchical naming scheme
- Plans for desirable routes inside of one domain
- E.G. BGP routes packets between networks
- Uses header values from IP packet and instructions from control plane (routing) to send packets onward

![Untitled](Week%201%20-%20Internet%20Basics%202798fe799efb49489a2b60518464f7b4/Untitled.png)

<aside>
📌 **SUMMARY: The internet is a network of networks that uses packet switching to make efficient use of finite physical resources. TCP handles the magic of ordering and aligning packets for the endpoints while the IP handles the name scheme of devices on the network.**

</aside>

---

### Date: August 24, 2022

### Topic: Interent History

### Recall

Galactic Network

Circuit switching

Packet switching

Resiliency

First computer network

ARPANET

“Flag day”

Future evolution

### Notes

- J. C. R. Licklider first head of DARPA computer research 1962
- Operators physically plug cables in locations to route the call and complete a circuit
- Physical channel carrying data, phases (setup, data transfer, tear-down)
- One operation: send packet, packets are stored (queued) in each router and forwarded

![Untitled](Week%201%20-%20Internet%20Basics%202798fe799efb49489a2b60518464f7b4/Untitled%201.png)

- Centralized —> decentralized —> distributed have increasing resiliency
- ARPA funded project connecting MIT to Santa Monica, CA
- Interface message processor - first packet switch
- ARPANET began to evolve to Internet as TCP and IP were developed and deployed (this put more pressure on endpoints to align and structure packets)
- NCP to TCP/IP on ARPANET January 1st 1983
- Core protocols have changed little
- Now we have malicious parities, extreme complexity, incredible growth, mobility

<aside>
📌 **SUMMARY: Idea for the internet emerged first emerged in the 1940s through 1960s. These ideas evolved from universities with government funding. New technologies were organically created that enabled increased adoption, more traffic, and more applications to be plugged into the network.**

</aside>