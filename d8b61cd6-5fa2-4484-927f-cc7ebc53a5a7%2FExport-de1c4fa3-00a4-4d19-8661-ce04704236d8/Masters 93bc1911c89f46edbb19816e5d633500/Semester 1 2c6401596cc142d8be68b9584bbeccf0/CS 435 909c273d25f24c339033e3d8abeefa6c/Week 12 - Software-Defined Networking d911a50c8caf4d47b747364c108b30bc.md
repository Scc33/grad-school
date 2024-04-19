# Week 12 - Software-Defined Networking

### Date: November 19, 2022

### Topic: Quiz

### Recall

- Key characteristics of software-defined networks include
    - In addition to "An API interface to the data plane of switches" and "A programmable, logically centralized network controller", another key characteristic we discussed is the ability to build higher-level abstractions (e.g., policy definition languages) on top of the logically centralized controller
    - **An API interface to the data plane of switches**
    - **A programmable, logically centralized network controller**
- In traditional non-virtualized data centers, moving services (or VMs or tenants) between machines can be difficult because
    - Moving services can be difficult for all of these reasons: (a) because traditional data center networks are often very oversubscribed; (b) because IP prefixes are tied to certain racks or clusters in the network, as they are used for routing; (c) because some services depend on L2 features like multicast or broadcast.
    - **Some services need to be kept within a single Layer 2 domain.**
    - **IP addresses may need to be reassigned.**
    - **The performance of the running service can differ significantly if it is moved outside its primary rack or cluster.**
- The VL2 paper argues that if the data center has a relatively large number of relatively small flows, this is a good match for VL2's design because
    - VL2's approach is to spread traffic pseudo-randomly so that traffic is evenly spread across the fabric, reducing hotspots.  Having a larger number of relatively small flows will make the spread more even.  While the paper argues that dynamically changing routes will be hard because the system would have to react very quickly, this leaves open the possibility that one could build a system that does in fact react quickly – the approach of CONGA.
    - **Other solutions that dynamically change the routing of flows based on current congestion could theoretically perform better. However, it would be difficult to make these schemes practical because the overall network traffic pattern changes very quickly.**
    - **Individual flows may get unlucky by being (randomly) assigned to a path that causes congestion, but if this happens, it will be resolved quickly because the flow will last for only a relatively short time.**
- VL2's use of Valiant Load Balancing is an example of:
    - VL2 sends packets through a random top-level switch.  This does not depend on current traffic flow.
    - **Oblivious routing of traffic, meaning that the selected path for a flow does not depend on the current traffic flows or link utilizations**
- Ignoring VL2 for a moment, if we use only ECMP in a data center network, this is an example of:
    - ECMP picks the flow's outgoing port at each router pseudorandomly based on a hash of packet header fields.  This does not depend on current traffic flow.
    - **Oblivious routing**
- Recall the CONGA data center architecture from last week, or read the introduction of [the paper](https://people.csail.mit.edu/alizadeh/papers/conga-sigcomm14.pdf) now.  CONGA's traffic routing is an example of
    - CONGA tries to make adaptive routing fast by having switches learn about path performance in an end-to-end manner.
    - **Adaptive routing**
- Worst possible hashing
    - In the worst possible ECMP hashing, all 8 flows converge on a single link entering the switch that serves Ad. 10 Gbps / 8 = 1.25 Gbps
    - **1.25gbps**
- Shortest paths
    - ECMP only selects among shortest paths.
    - In the commonly used "fat tree" network topology, as well as leaf-spine topologies, there is only one shortest path going through each top-level switch.  This is true regardless of which servers are the source and destination.
    - **1**
- Average data rate {1,2,3,4}
    - This is the ideal case in which we get lucky with ECMP hashing, resulting in perfectly balanced flows.
    - **2.5gbps**
- UDP at 4gbps
    - Although such a scenario may not seem common, in a multi-tenant data center with thousands of untrusted tenants, we have to think about how things will go wrong.
    - 1gbps
- The scenario in the previous question falls outside the case where VL2 claimed to provide performance isolation, because
    - The Clos fabric built by VL2 will never be a bottleneck -- assuming "hose model" traffic, i.e., the traffic we request the network to handle respects the servers' NIC inbound and outbound line rates. In general, TCP will cause backoff to make this happen, at least given some time for it to converge.
    - **Some flows are not running TCP and did not back off when encountering congestion**
    - **The traffic does not conform to the "hose model": the injected traffic sent to Bd exceeds its line rate**
- VL2's goal is the "agility" of allowing any server to be assigned to any service.  To enable service mobility across the physical data center network, in VL2:
    - Note, however, that mobiliy is just one of the needs to achieve agility.
    - **Two separate IP address spaces are used – one to identify an application, one to identify its location – with a dynamic translation step between these.**
- AA refers to
    - **A server or virtual server**
- LA refers to
    - **A ToR (top of rack switch)**
- When a service moves in VL2:
    - Translation between the fixed AA and the potentially dynamic LA is one of VL2's key jobs.
    - **Its AA stays the same, but its LA may change.**
- Suppose a NVP data center has one tenant with 10 VMs and one with 100 VMs. Each VM is on a separate physical server. Each tenant allows any communication within its virtual network and no external communication. How many total unidirectional tunnels will be constructed in the data center?
    - NVP may build a large number of tunnels – in general, it scales quadratically with the size of the virtual network.
    - **9,990**
- In the same situation as the previous question, how many total instances of tenants' virtual networks will exist throughout the network?
    - Each instance of Open vSwitch on a host is given its own copy of the *entire* virtual network!
    - **110**
- Can NVP enforce microsegmentation, i.e., access control across tenants?
    - With an entirely configurable virtual network datapath, NVP has a high degree of flexibility in the policies it enforces.
    - **Yes, unauthorized packets will either be dropped at some step in the logical datapath, or the address of the remote tenant may be private, so there will be no address to send to in the first place.**
- NVP, as described in the paper, can directly guarantee
    - NVP is a software based solution.  Performance uniformity requires at least some capability of the physical hardware, so NVP by itself does not guarantee it.  Indeed, as we have seen, achieving ideal performance uniformity and isolation is difficult.
    - **Segmentation across tenants**
    - **Location-independent addressing**
    - **Layer 2 network semantics**

---

### Date: November 19, 2022

### Topic: Network Virtualization Case Study: NVP

### Recall

NVP

Challenge: Performance

SDN attributes

### Notes

- Network virtualization
    - Arbitrary network topology
        
        ![Untitled](Week%2012%20-%20Software-Defined%20Networking%20d911a50c8caf4d47b747364c108b30bc/Untitled.png)
        
- Open flow forwarding table
- Open vSwitch is programmable switching mechanism
    
    ![Untitled](Week%2012%20-%20Software-Defined%20Networking%20d911a50c8caf4d47b747364c108b30bc/Untitled%201.png)
    
- Large amount of state to compute
    - Full virtual network state at every host
        - Automated incremental state computation with nlog language
    - O(n^2) tunnels for a tenant with nVMs
    - Pipeline processing in virtual switch can be slow
        - First packet goes through full flow, subsequent packets are routed using cache
- API to the data plane
- Centralized controller that's orchestrating that programming
- High-level control abstractions

---

### Date: November 18, 2022

### Topic: Network Virtualization Case Study: VL2 - Part 2

### Recall

Application vs locator addresses

Does this achieve our goals?

### Notes

- VL2 - virtual layer 2 network
- Application addresses - location independent
- Locator addresses - tied to topology and used to route
- Application sends to AA then we look that up in directory server to get locator address

![Untitled](Week%2012%20-%20Software-Defined%20Networking%20d911a50c8caf4d47b747364c108b30bc/Untitled%202.png)

- IP address functionality is overload (ie its used to location and identification)
    - Application address takes the identification functionality
- Location independent addressing (AA are local independent)
- L2 network semantics
- Performance uniformity
    - Clos nonblocking
    - ECMP provides load balancing
- Security - directory system can allow and deny connections by choosing whether to resolve AA to LA

---

### Date: November 18, 2022

### Topic: Network Virtualization Case Study: VL2 - Part 1

### Recall

VL2 was predecessor to Microsoft Azure

### Notes

- In this case study internal traffic is 4x external traffic and the traffic is unpredictable, rapidly changing
- Nonblocking fabric - high throughput for any traffic regions
- Scale out (instead of scale up) - clos topology

![Untitled](Week%2012%20-%20Software-Defined%20Networking%20d911a50c8caf4d47b747364c108b30bc/Untitled%203.png)

- Want to spread traffic as much as possible
    
    ![Untitled](Week%2012%20-%20Software-Defined%20Networking%20d911a50c8caf4d47b747364c108b30bc/Untitled%204.png)
    
- Top of rack switch will send to any intermediate switch because they are all assigned the same address

---

### Date: November 18, 2022

### Topic: Multi-Tenant Data Centers: The Challenges

### Notes

- Agility - using any server for any service at any time
    - Better economies of scale and better reliability
- Need tenants to have their IP addresses able to be taken everywhere (without tenants even noticing)
- Performance uniformity - need to be able to move VMs without a hit to performance
- Network segmentation - in order to improve security becomes programs can’t trust each other

![Untitled](Week%2012%20-%20Software-Defined%20Networking%20d911a50c8caf4d47b747364c108b30bc/Untitled%205.png)

---

### Date: November 18, 2022

### Topic:  Software Defined Networking Architecture - Part 2

### Recall

Evolution of SDN

Open data plane interface

SDN Killer Apps

### Notes

- Flexible data planes
    - Label switching
        - Lay down specific path through network for classes of traffic
    - Active networks
        - Packet header points to program code
        - Packets carrying code with them that can be executed
- Logically centralized control
    - Routing control platform
    - Ethane
        - Centralized controller enforces policies for the network
- Opportunities
    - Hardware - with standardized API its easier to change hardware
    - Centralized controller - direct programmatic control of network
    - Makes network engineering more like the rest of software engineering
- Challenges of SDN
    - Performance and scalability
    - Distributed challenges still present (eg *logical* centralized controller*)*
- Cloud virtualization
    - Create separate virtual networks for tenants (allow flexible placement and movement of VMs)
    - Intra-datacenter traffic engineering

<aside>
📌 **SUMMARY: Software defined networking strives to make network programming more like regular software programming with logically centralized controls.**

</aside>

---

### Date: November 17, 2022

### Topic: Software Defined Networking Architecture - Part 1

### Recall

Hard to innovate with traditional networks

Use software on top of hardware to play around

### Notes

- Problems
    - Networks are complicated
    - Networks are distributed
    - No APIs, only knobs and dials
    - Network equipment is proprietary
- Data plane API
    - If we have logically centralized controller then we can have central place to give instructions

<aside>
📌 **SUMMARY: SDN can make innovation on top of the hardware easier.**

</aside>