# Week 2 - Building a Network

### Date: September 3, 2022

### Topic: Quiz Week 2

### Recall

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled.png)

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%201.png)

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%202.png)

<aside>
📌 **SUMMARY: Link state routing provides the most info but is costliest, DV provides less info, and PV improves on DV.**

</aside>

---

### Date: September 3, 2022

### Topic: Path Vector Routing

### Recall

Just like distance vector but two changes

DV and PV in real world

Overview

### Notes

- Updates to distance vector routing
    - Store and share the path rather than just the distance
    - Ignore loopy paths when sending route advertisements
    - This eliminates permanent loops but not transient loops
- Routing information protocol (RIP) (RFC 1058)
- Enhanced interior gateway routing protocol (EIGRP)
- Border gateway protocol (BGP)
    - Developed for inter domain routing but recently repurposed for routing within datacenter

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%203.png)

<aside>
📌 **SUMMARY: Path vector routing improves on DV routing by storing and sharing the path rather than just distance.**

</aside>

---

### Date: September 3, 2022

### Topic: Distance Vector Routing

### Recall

Overview of distance vector routing

Distance vector routing algorithm

What triggers distance updates?

When should a router send a distance update?

Where does the forwarding table come from?

Count-to-infinity-problem

### Notes

- Routers exchange best known routes incrementally, doesn’t distributes maps
- Advertisements of best routes

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%204.png)

- If network is unchanging then eventually the protocol will converge
- Distance updates, link or node failures, link cost changes
- Can periodically send entire vector or can send triggered updates
- Router needs to remember which neighbor found the minimum distance
- Count-to-infinity problem - routers did not realize picked path is invalid
    - Set infinity to be a low value so that counting stops

<aside>
📌 **SUMMARY: Distance vector routing involves communicating the best path to neighbors rather that distributing all local information as in link state routing.**

</aside>

---

### Date: September 3, 2022

### Topic: Link State Routing Algorithm

### Recall

Reliable flooding algorithm

When do we know we are done learning the full network?

How many LSAs will be sent?

What if a link fails?

OSPF

### Notes

- Reliable flooding algorithm is gossiping latest information  to the entire network
    
    ![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%205.png)
    
- Never, the network may always be changing and updating so we will periodically re run the shortest algorithm computation
    - Initial runs will be suboptimal because the entire network isn’t known but should get better over time as the network is more fully understood
- N nodes and M links, then there will be between M and 2M LSAs (link state advertisements)
    - Node won’t send information back to sender because just got information from that sender so not quite 2M
- Uses sequence number to decide if there is new information to propagate
    
    ![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%206.png)
    
- Open shortest path first
    - One of the most common interior gateway protocols (IGPs) for routing inside a domain

<aside>
📌 **SUMMARY: Link state routing will reliably flood a network with information. Individual nodes use the flooded information calculate shortest paths and therefore their forwarding tables.**

</aside>

---

### Date: September 3, 2022

### Topic: Distributed Routing

### Recall

Two major types of routing protocols

Link state routing

### Notes

- Distributed routing algorithms are used when you don’t know what the network looks like
- Link state routing - distribute all local information globally, each router runs shortest path to compute its forwarding table
- Distance vector routing - routers exchange best known routes incrementally
- Each node in the router is going to distribute information
    
    ![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%207.png)
    
- Messages my be re-sent because sender doesn't know that the receiver may have already received it

<aside>
📌 **SUMMARY: Distributed routing algorithms are used when the entire network is unknown. The main types of distributed routing algorithms are link state routing and distance vector routing.**

</aside>

---

### Date: August 25, 2022

### Topic: The Control Plane

### Recall

Control plane

Date plane

Graphs

How do we compute shortest paths for forwarding tables?

Why does Dijkstra’s algorithm work?

Dijkstra caveats

Distributed routing protocols

### Notes

- Control plane plans routing
- Data plan performs forwarding
- G = (V, E, c) aka a weighted, undirected graph
- Dijkstra’s algorithms: computes least cost path from s (current node) to all nodes in V

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%208.png)

- We are hoping the node from the frontier with the minimum distance so we know we found a shortest path. Adding up all the shortest paths creates the overall shortest path
- Dijkstra’s time complexity: O((n+m) log n) where n is a node
- Cost algorithms can be swapped at will to calculate forwarding tables
- Dijkstra’s needs to know the entire graph but we don’t know the whole network so we need *distributed routing protocols*

<aside>
📌 **SUMMARY: Storing frontier tables wouldn’t scale so the control plane calculates forwarding tables by using shortest path algorithms like Dijkstra's.**

</aside>

---

### Date: August 25, 2022

### Topic: Inside a Switch Data Plane - 2

### Recall

*Data queue*

Head of line blocking

*The switching fabric*

Crossbar switch

Self-routing fabrics

*Output queues* 

### Notes

- Packets may arrive faster than next stage (fabric) can handle them
- Buffer will hold packets waiting to be sent to fabric (FIFO is easiest to implement)
- First car turning left so you get stuck behind that car turning left
- FIFO queue will cause head of line blocking
- To prevent head of line blocking use very fast fabric or virtual queues by port
- Shared I/O Bus is fundamentally limiting because no parallel
    
    ![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%209.png)
    
- Matrix enables connecting any input to any output (O(n^2)) components for n ports
- Each fabric is a small network (can uses O(nlogn) components) and can provide buffering within network
- Sometimes packets can arrive faster than the output port can handle them
- No head of line blocking problem at the output queue because its like an intersection where you can only go straight (think airport security line)

<aside>
📌 **SUMMARY: The switch data plane consists of an input port, input queue, switching fabric, output queue, and output port. Packets going through these components can become stuck due to head of line blocking so virtual queues can be used to prioritize flows.**

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%2010.png)

</aside>

---

### Date: August 25, 2022

### Topic: Inside a Switch Data Plane - 1

### Recall

Packet switches

Order of events inside a switch

Input packet processing

Output interface

Look up action

### Notes

- Packet forwarding is carried out in the data plane
- Think of these as the street intersections of the internet
- Input interfaces (port) —> packet processing —> input queues —> switch fabric —> output queue —> output interface (port) | all driven by control plane processor
- First converted (analog—>bits—>frames), then extract the header type and fields
- Data plane focuses on performance so little time therefore relying on simple instructions (FIB - forwarding information base)
- Simple method: exact match (doesn’t scale) | More flexible: *longest prefix match* (often implemented with special TCAM hardware)
    
    ![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%2011.png)
    

<aside>
📌 **SUMMARY: Switches relying on custom hardware and forwarding tables based on *longest prefix matching* to receive, route, and send packets in just a few hundred nanoseconds.**

</aside>

---

### Date: August 24, 2022

### Topic: Let’s Build a Network

![Untitled](Week%202%20-%20Building%20a%20Network%20c8a579c87ec444f7b400e823ea6236c8/Untitled%2012.png)

### Recall

Multi-hop network

Routing

Forwarding

Forwarding table

### Notes

- A hard problem even for just intradomain networks
- Plan paths across the network *(control plane)*
    - Time scale - msec to minutes
    - Often implemented on a general purpose hardware host
- Send packets from source to destination along path *(data plane)*
    - Needs to be very high performance
    - 40 Gbps input port, 1500 byte packet = 300ns response required
    - Often implemented on custom ASIC hardware
- Interface between control and data plane and specifies how data plane should function

<aside>
📌 **SUMMARY: Multi-hop networks are a complex problem consisting of two planes. A routing (control plane) and a forwarding (data plane). The control plane creates directions and the data plane handles the movement of packets through the network.**

</aside>