# Week 11 - Host Virtualization, Routing, and Congestion Control

### Date: November 19, 2022

### Topic: MP on SDN

### Notes

- Top level are core switches
- Second level are edge switches

![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled.png)

---

### Date: October 8, 2022

### Topic: Quiz

### Recall

The fat-tree network below has a total of 32 switch-switch links. (Verify that this is true.) How many of these links will be used by a tree spanning all the switches? Remember: we’re excluding server-switch links in both counts and are counting cables, not directed edges.

- 19

Assuming that there’s no other traffic in the network, how much aggregate bandwidth is available from the left-most pod (the left-most four servers) to any other pod in the fat-tree below with the switches marked with **X** having failed? Count only bandwidth in the direction from the left-most pod to the other; assume links are all unit capacity and that we have perfect multipath routing.

- 2

How does TRILL enable the use of all the links in the network?

- By running a link-state protocol between the switches

In BGP, the path announcements nodes make to neighbors contain:

- The autonomous system-level path from the node to the destination

How does ECMP avoid packet reordering?

- By consistently using the same path for packets of the same flow
    - ECMP uses hashing over packet header fields to determine which path will be picked for a packet. This results in packets of the same flow (i.e., sharing the fields over which the hash is computed) consistently ending up on the same path.

Between a specific pair of servers, how many ECMP paths can be set up for the fat-tree topology (as in this paper: [A Scalable, Commodity Data Center Network Architecture](http://ccr.sigcomm.org/online/files/p63-alfares.pdf)) built with switches with 10 ports each, i.e., k = 10? Ignore any switch hardware constraints on ECMP; we’re only looking for the number of equal-cost shortest paths.

- 25
    - Correct! The general expression is (k/2)^2 equal-cost shortest paths.

How does CONGA do forwarding on multiple paths?

- Congestion is monitored on the various paths between pairs of leaf switches, with the least congested paths being chosen.

What are flowlets?

- Flowlets are packet-groups in the same flow that are separated by large enough gaps from other packet-groups such that sending them along different paths has a reasonably small likelihood of reordering a flow’s packets.

How do containers (for example, with Docker) typically differ from virtual machines?

- Each virtual machine runs its own operating system, while containers may depend on the underlying system’s kernel and other resources.
- Applications can be packaged into containers needing much smaller disk and memory footprint than with virtual machines.
- Containers can be instantiated much faster than virtual machines.

At 100Gbps, with all packets being 100 Bytes in size (including the preamble, etc.), how much time can we afford to spend on processing each packet to be able to process packets at line-rate, sequentially?

- 8 nanoseconds

How does SR-IOV help with the difficulty of packet processing at line rates?

- Each virtual machine has hardware resources on the NIC from where it reads packets meant for it.
- Packets are passed to a VM's memory from the NIC using direct memory access, without invoking the hypervisor.
- It uses a simple fast packet classifier on the NIC itself.

What are some drawbacks of SR-IOV’s approach?

- Migration of VMs is trickier because their network state is tied to the NIC.
- The simple on-NIC packet classifier does not provide general purpose packet forwarding logic.

Which of these design decisions enables Open vSwitch to provide fast-enough performance for common workloads while allowing general purpose packet forwarding logic?

- Division of user-space and kernel-space tasks: user-space handles network state updates and processes the first packet of flows, while kernel-space is optimized for fast forwarding of future packets.
- The kernel-space packet classifier is a simplified, collapsed version of rules applicable to packets seen recently, thus making processing faster.
- An even simpler cache allows constant-time lookups mapping incoming packets to the applicable forwarding entry in the kernel-space classifier.

Assuming that TCP is in the additive increase phase and the congestion window is *X* bytes, what will the congestion window be after the sender detects a single packet loss?

- X/2
    - TCP uses multiplicative decrease in response to a packet loss when it is operating in the additive increase phase. The decrease factor is 2, so *X*/2. As we noted in the lectures, this multiplicative decrease can be unnecessary in many situations.

Assuming that TCP is in the additive increase phase and the congestion window is *X* bytes, what will the congestion window be after the sender detects a single packet loss?

- Loss is a poor signal of persistent congestion. Losses can also occur due to other transient factors.
- Multiplicative decrease can be too aggressive – perhaps the sender’s rate is only marginally larger than the available capacity.
- Waiting until a loss before reacting to congestion means waiting until buffer occupancy is large. This increases queuing latencies.

Assume that data travels over fiber at a speed of 2*c*/3, where *c* is the speed of light in a vacuum. What is the (one-way) propagation delay across 300 meters of fiber running across a data center floor? (This might seem annoying, but the point of such questions is to make sure you have a better sense of these timescales.)

- 1.5 microseconds

Assuming a line rate of 10Gbps, what time elapses between a packet arriving in a buffer with five packets already queued (each packet being 9000 bytes in size), and reaching the head of the queue (i.e., just before its bytes start to get sent across the wire)?

- 36 microseconds
    - You have 5 * 9000 * 8 bits = 36 * 104 bits. At a line-rate of 10Gbps = 1010 bits per second, this takes 36 * 10-6 seconds to transmit.

In data centers, queuing delay caused by just a few packets can exceed the propagation delay. What problem(s) does this pose?

- Large buffer occupancies can inflate end-to-end latencies by orders of magnitude.
    - As you see in the previous few questions, queuing delay can be much larger than propagation delay. Not only does this increase latency by many times over, it also makes variations in latency large – when queues are empty the latency is small, and when they’re full, latencies are many times larger. This is an important concept that influences the design of congestion control in data centers. Please make sure you view the lecture video again if you don’t fully grasp it!

Suppose that to address TCP incast, we reduce the TCP connection timeout value. Which of the following is true?

- While this may help increase throughput if some of the TCP connections were timing out due to losses, latencies can still be high and variable because of large buffer occupancies.
    - You should learn to reason about the consequences of such design choices: if you make change X, what will its likely impact be? If connections were timing out due to incast, and thus sometimes leaving the link under-utilized, lowering the timeout period can increase throughput because connections will resume faster, and thus utilize the link better. However, it doesn’t address latency – with the timeout, you’re only changing how quickly TCP flows resume sending, you’re not addressing buffer occupancy.

How does DCTCP try to provide both low latency (i.e., keeping buffer occupancies small) and high throughput?

- It marks packets with congestion signals as the buffer starts to fill beyond a threshold. If the threshold is low, this signals congestion much before the buffer is full.
- The senders adjust their rate in proportion to the number of congestion markings they receive, unlike TCP’s multiplicative decrease.
- Small buffer occupancies also allow buffers to absorb traffic bursts, thus reducing packet losses and helping maintain high throughput.

If the congestion window at a sender is *X* bytes and it receives congestion markings based on which fraction of marked packets is updated to 0.4 (i.e., the *α* calculated per equation (1) in the DCTCP paper – [Data Center TCP (DCTCP)](https://people.csail.mit.edu/alizadeh/papers/dctcp-sigcomm10.pdf) is 0.4), what is the congestion window adjusted to?

- .0.8 *X*
    - The congestion window is adjusted to *X* * (1 − *α*/2). Refer to the reading for more details.

What considerations govern the setting of DCTCP’s congestion marking threshold, *K*?

- If it’s too large, buffer occupancy will still be high.
- If it’s too small, throughput can be low because congestion is signaled more often than necessary.

---

### Date: October 8, 2022

### Topic: Readings

### Recall

[TCP Congestion Control](https://www.rfc-editor.org/rfc/rfc5681)

[Use of BGP for routing in large-scale data centers](https://datatracker.ietf.org/doc/html/draft-lapukhov-bgp-routing-large-dc-07)

### Notes

```
This document defines TCP's four intertwined congestion control algorithms: slow start, congestion avoidance, fast retransmit, and fast recovery.  In addition, the document specifies how TCP should begin transmission after a relatively long idle period, as well as discussing various acknowledgment generation methods.  This document obsoletes RFC 2581.
```

- When data centers get very large BGP is an effective routing control protocol

<aside>
📌 **SUMMARY:**

</aside>

---

### Date: September 17, 2022

### Topic: Congestion Control Discussion

### Recall

- One designer and operator of the datacenter so they can upgrade somewhat easier
- Most of this course has talked about performance on the network layer, but actual performance to the end layer depends on application (or at least measured there)

---

### Date: November 17, 2022

### Topic: Congestion Control - Part 3

### Recall

Throughput vs latency

DCTCP

### Notes

- Conflicting goals
    - High throughput: buffers absorb bursts
    - Low latency: large, full buffers increases latency
- Data center TCP
    - Explicit congestion notification (ECN)
    - Looks at average congestion (queue length) over a recent time period
    - Market the packets with bits indicating if congested
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%201.png)
        
    - Get the direct signal (rather than infer via packet loss) then respond the same way (multiplicative decrease)
    - Problems of DCTCP
        - DCTCP is not TCP friendly (can’t combine DCTCP and TCP)
        - DCTCP doesn’t address slow start
        - DCTCP doesn’t address application level behavior

<aside>
📌 **SUMMARY: Data center TCP is a huge advancement over regular TCP**

</aside>

---

### Date: November 17, 2022

### Topic: Congestion Control - Part 2

### Recall

Problems with TCP

Large queues

Scatter-gather traffic pattern

Incast

### Notes

- Multiplicative decrease is a huge factor that can lead to underperformance and loss isn’t a good indicator of congestion
- Because within a data center large queues are probably the reason for dropped packets
- Full queues can lead to order of magnitude decrease in performance
- In scatter gather hundreds of queries are sent out then recollected by the host (for example this is what happens in Google searches)
- TCP incast - so much traffic increasing queues and therefore latency

<aside>
📌 **SUMMARY: TCP congestion control is the most optimized technique for within data centers.**

</aside>

---

### Date: November 17, 2022

### Topic: Congestion Control - Part 1

### Recall

What is congestion?

### Notes

- Rate > capacity = packet loss and unfair distribution of traffic
- Rate < capacity = inefficient use of network resources
- Congestion is not static which makes this a hard problem
- Congestion probing
    - Sender treats network as a black box
    - Send packets, wait, see how many ACKs, adjust rate based on number of ACKs
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%202.png)
        
- How TCP handles congestion control

![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%203.png)

<aside>
📌 **SUMMARY: TCP congestion control uses slow start then additive increase. It halves whenever there is a dropped packet.**

</aside>

---

### Date: November 17, 2022

### Topic: Routing and Traffic Engineering: Packet Forwarding on Multiple Paths

### Recall

Multipath routing

ECMP

Flowlet

### Notes

- Want to spread traffic around so no one route is oversubscribed
- Want to load balance network traffic, but that is computationally expensive
- Want to solve in a distributed manner
- Equal cost multi-path routing
    - Randomly pick from paths which are equal cost
    - Equal choice can happen at each hop
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%204.png)
        
- Flowlets - if gap between packets is larger than our latency estimate we send packet groups on different paths, the groups reduces the risk of reordering
- Overview
    - Single-entity control
    - Switch forwarding tables are very large (tens of thousands of layer 2 and 3 entities)
    - Topology is known and controlled by operator

<aside>
📌 **SUMMARY: Rather than using the same path every time (which can lead to too much traffic on a single route) we spread traffic around the network with something like equal cost multi-path routing.**

</aside>

---

### Date: November 16, 2022

### Topic: Routing and Traffic Engineering

### Recall

Spanning Tree Protocol

TRILL

OSPF

BGP

### Notes

- STP - achieve loop free routes in small networks
    - Picks a tree and routes passages along that tree
    - Very simple and gives up some performance
    - Need very large and very expensive switches at the top because they are handling lots of traffic (vertical scaling)
- Transparent Interconnection of Lots of Links
    - All links are usable (because we have the entire topology)
    - Requires new hardware to support the protocol and still single failover point
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%205.png)
        
- Open shortest path first
    - Data center works like the traditional internet
        - Meaning it uses IP and operates on layer 3 (so more configuration required)
    - Little configuration available because using traditional routing algorithms
- BGP is the internet scale protocol but also can be used in the data center
    - Once again layer 3 so VM configuration will be complex
    - Converging will be slower
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%206.png)
        

<aside>
📌 **SUMMARY: Routing within the data center is growing even more complex so the routing algorithms have stepping in complexity to match.**

</aside>

---

### Date: September 17, 2022

### Topic: Host Virtualization Discussion

### Recall

- Virtualization means better economies of scale
- Tradeoff between flexibility and performance but we really want both

---

### Date: October 8, 2022

### Topic: Host Virtualization

### Recall

Benefits of virtualization

Server virtualization

Networking VMs

Side note: Containerization (Docker)

SR-IOV

### Notes

- Virtualization allows for sharing physical infrastructure and rapidly spinning up and down
- VMs are managed by a hypervisor
    - Hypervisors include: Zen, KVM, VMWare ESXI ect
    - Network interface is also virtualized
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%207.png)
        
- The hypervisor runs a virtual switch which wires up the VMs to the physical interface
- Running the entire OS inside a VM is a lot of used up resources and instead can be shared
    - Example VM has an entire OS inside of it
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%208.png)
        
    - Docker, Kubernetes, and container platforms instead sit on an OS and run applications from inside of a container which makes them lighter weight
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%209.png)
        
- Single-root I/O Virtualization
    - The NIC provides a physical function and several virtual functions
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%2010.png)
        
- Open vSwitch
    - Decision making resides in the user space while the kernel handles fast packet forwarding
        
        ![Untitled](Week%2011%20-%20Host%20Virtualization,%20Routing,%20and%20Conges%2097a9204bb4614281ab591f03abc25c6a/Untitled%2011.png)
        

<aside>
📌 **SUMMARY: NIC (network interface card) is a physical resource that is used to control networking. It can be shared via virtualization.**

</aside>