# Week 3 - Building an Internetwork

### Date: September 5, 2022

### Topic: Quiz

### Recall

The maximum length of packet in a standard IPV4 communication is:

- 2^16=64kb

If a network needs 50,000 host addresses, what IPv4 prefix length will provide enough addresses while leaving as few as possible unused?

- 16 : 2^16=65,536 addresses

If networks were constrained to use the historical “classful” method of IP allocation, which of the following two networks would use the same class?

- A network with 300 hosts and a network with 50,000 hosts

Control messages – that is, messages between IP modules in routers to deal with operations outside of delivering application data to end-hosts -- are handled by:

- ICMP

Consider an implementation of an IP router that strictly follows IP’s layered architecture. When the IP module is processing a packet, data or headers from which of the following protocols is treated as opaque data (so the data is forwarded, but not parsed into individual fields)? (Check all that apply.)

- TCP, HTTP

Consider an implementation of an IP router that strictly follows IP’s layered architecture. When the IP module is processing a packet, data or headers from which of the following protocols is not inspected, because it was removed by a lower layer before being handed to IP? (Check all that apply.)

- Ethernet

In the soft state semantics of a DCHP server’s lease of an IP address to a client, which of the following are true? (Check all that apply):

- The DHCP server is responsible for terminating the lease
- The client is responsible for renewing the lease while it is still in use

---

### Date: September 5, 2022

### Topic: Using IP Addresses to Route & Forward

### Recall

Prefixes as destinations

Forwarding requires more than IP

ARP

Basic principles of IP addresses

### Notes

- IP prefix attached to some router (idea of a node in a graph)
- IP allows for overlapping prefixes, use the longest prefix match to find where to go

![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled.png)

- ARP - address resolution protocol
    - Goal: map an IP address to a local network address (ex MAC address)
    - Each device on local network knows its own IP and local address
    - ARP table

![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%201.png)

- Hierarchy allows scale
    - Allocate and subdivide ownership hierarchically
    - Preform IP routing and forwarding based on IP prefixes
    - Perform local packet delivery using ARP

<aside>
📌 **SUMMARY: Local networks may not know where to forward data so they use prefix matching and ARP tables to understand outside IP addresses.**

</aside>

---

### Date: September 5, 2022

### Topic: IP Address Assignment

### Recall

Why IP naming is hard

Assign subnets within an organization

DHCP - dynamic host configuration protocol

Soft state

### Notes

- Ethernet has MAC addresses (medium access control) which are unique identifiers but location independent
    - IP addresses are identifiers and locators
- IP address are distributed by ICANN
- Subnet - refers to a set of IP addresses
- Each local network below IP are assigned an ethernet subnet
    - IP routers form boundaries between subnets
        
        ![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%202.png)
        
- Automatically manages address assignments to host
    - Client sends DHCP Discover message to broadcast address 255.255.255.255
    - DHCP server responds with address
    - Client replies to claim address
    - DHCP seems like a buddy or mentor giving info on IP, DNS, and mask
- Client needs to explicitly renew their state otherwise their IP address binding is cleared after a timeout

<aside>
📌 **SUMMARY: IP address naming is difficult because it is an identifier and a locator. IP addresses are distributed by ICANN and DHCP servers handle dolling out at the local network level.**

</aside>

---

### Date: September 5, 2022

### Topic: IP address Structure

### Recall

What does one IP address mean?

Identifier format

Hierarchical addressing

What is a subnet?

![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%203.png)

### Notes

- IP address is an identifier for an interface
    - A device may have multiple interfaces (WiFi vs LTE)
    - Therefore each device may have several IPs
    - 127.0.0.1 is the loop back address to the local device (lo)
- Format
    - IPv4 - 2^32 possibilities typically written in octet form (192.168.1.66)
    - IPv6 - 2^128
- Internetwork address identifies a network and a host
    - Dividing up an IP address
        - Subnets - variable length prefix of bits
        
        ![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%204.png)
        
- Mask lets us easily compute if address is in a subnet (bitwise and)
    
    ![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%205.png)
    

<aside>
📌 **SUMMARY: Subnets allow for hierarchical naming of devices connected to the internet.**

</aside>

---

### Date: September 5, 2022

### Topic: Fragmentation: Handling Heterogeneity in Packet Lengths

### Recall

MTU

Fragmentation

IP Packet Format

### Notes

- MTU - maximum transmission unit
- Send has no clue what maximum size along e2e path and doesn’t even know the path
- If network doesn’t support large size then it can be fragmented and reassembled at the endpoint (example of end-to-end argument)
    - Reassembly
        - Occurs at recipient
        - If not receiving all packets then discard them all discovery
    - Avoid fragmentation if possible
        - Can employe MTU
        - Special don’t fragment bit in IP header
- 20x32byte header
    - Identification - 16 bits identifies originally sent datagram
        
        ![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%206.png)
        

<aside>
📌 **SUMMARY: Packets are sent as large as possible but will be fragmented if the packet is larger than the MTU of a network.**

</aside>

---

### Date: September 5, 2022

### Topic: The IP Service Model

### Recall

IP service is “least common denominator

E2E argument

Endpoints necessary & sufficient for reliability

### Notes

- IP service model
    - Datagram - packet switched messages (not stream)
    - Best effort delivery
- In-network implementation of reliability is hard and still needs more work done at endpoints
    - Implemented reliability at endpoint level simplify lower layers and is more correct
- So IP might as well be unreliable because its simpler and might as well used datagrams

<aside>
📌 **SUMMARY: IP is unreliable and uses datagrams because it is all that is required to function.**

</aside>

---

### Date: September 5, 2022

### Topic: Let’s Build an Internetwork

### Recall

Internetwork

Interdomain Challenges

Naive way of handling heterogeneity

Unifying protocol

Layering

### Notes

- A collection of heterogeneous networks joined in to a logical networking providing e2e communication
    
    ![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%207.png)
    
- Every internetwork-capable device understands every networks’ protocol (n hosts, m protocols, n*m interactions, m^2 protocol conversions)
- IP forms unifying layer where every internetwork-capable device needs to understand IP
- Layering is form of modularity
    - IP forms narrow waist layer
        
        ![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%208.png)
        
    - Layer n depends directly on layer n-1
- IP is an overlay network
    - Overlay network is a logical network whose links are an underlying network
    - Each IP-level hop uses underlying network e2e service as a tunnel

<aside>
📌 **SUMMARY: IP is a narrow, overlay layer that obscures the lower level calls and providers support for reach interdomains.**

</aside>

![Untitled](Week%203%20-%20Building%20an%20Internetwork%20be9d4226a1424693a2ebb004f488ff38/Untitled%209.png)