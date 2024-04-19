# Week 5 - Planetary Scale Routing

### Date: September 11, 2022

### Topic: Quiz

### Recall

What protocol does a router use to learn routes for which the next-hop router would
be in another AS?

- eBGP

Which statement is true?

- If an active route is no longer available, a BGP router can send a
withdrawal message to the neighbors.

Which statement(s) are true?

- ASes typically don’t want to publicly expose their internal topology and
policies.

What basic routing algorithm is used by BGP?

- Path vector routing

Hot potato routing refers to

- Each router individually sending traffic to the nearest feasible
exit for that router.

Traceroute may provide an incomplete picture of the physical end-to-end path because

- **Some devices along the path are not running IP**
- It provides the sender with information about the forward path from source to
destination, but not the return path from destination back to source
- Routers may be configured to not respond with ICMP messages
- End-hosts may be configured to not respond with ICMP messages

---

### Date: September 11, 2022

### Topic: ICMP and Traceroute

### Recall

Management plane

ICMP

Traceroute

### Notes

- Systems and protocols used by humans and code to configure and operate network devices
- Internet control message protocol (ICMP)
    - Error reporting for IP
    - Companion protocol to IP
        - ICMP packets can be generated in response to an IP packet
            - Echo request: for ping utility
            - Echo reply: in response to request
            - Time exceeded
            - Destination port unreachable… etc
- How do we figure out where packets go?
    - IP packet’s TTL drops to zero ⇒ ICMP time exceeded
    - Can be run as local commands
        
        ![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled.png)
        
    
    ![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled%201.png)
    
    - So we can send dummy messages with increasing TTL
        
        ![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled%202.png)
        
    - Traceroute gives us an idea of what is going on with our packet directions

<aside>
📌 **SUMMARY: ICMP is a companion protocol to IP and when combined with traceroute it is helpful for debugging connections.**

</aside>

---

### Date: September 6, 2022

### Topic: Interdomain Routing Summary

### Recall

Acronyms

Why two IP based routing systems?

Short comings of BGP

### Notes

- AS - autonomous system
- IGP - interior gateway protocol
- EGP - exterior gateway protocol
- BGP - border gateway protocol
- eBGP - portion of BGP advertising routes externally
- iBGP - position of BGP advertising routes within AS
- Intradomain routing - share all information, execute single coordinated plan
- Interdomain routing - limit information, allow local domain policy decisions
- Short comings
    - Security
        - No certification of who owns IP prefix
        - No certification of whether an advertised AS path is real
    - Performance
        - No end-to-end metrics
        - AS path length has little to do with performance
    - Manageability
        - Difficult to observe why a route was picked

---

### Date: September 6, 2022

### Topic: Routing Policy in BGP

### Recall

Mechanisms to implement routing policies

Best path decision

Policy

How to use?

### Notes

- Import policy
    - Which AS did route come from? Did AS path include specific AS? Is route for specific IP prefix?
    - Filter route, tag
- Best path decision process
    - Highest localPref value, configuration by AS
    - shortest AS path length, configuration by neighboring AS
    - lowest origin type, not configurable
    - lowest multi-exit discriminator (MED) - configurable by neighboring AS
    - eBGP over iBGP, not configuration
    - lowest interior gateway protocol (IGP), configurable by AS
    - tie breaking - not configurable
- Export policy
    - To which AS would we advertise? What is next hop AS? Is route specific IP prefix?
    - Filter route, tag with MED
- Uses of policies
    - Prefer customers over providers
        - AS gets paid for traffic to customer, peer (exchange traffic), AS has to pay for traffic to a provider
    - Block non-customer routes
    - Hot potato routing - get rid of packets as fast as possible
        - Use eBGP learned over iBGP and prioritize lowest IGP cost

<aside>
📌 **SUMMARY: There are many BGP routing policies to adopt. The policies can be used to execute on priorities such as sending traffic to customers or using the fewest resources.**

</aside>

---

### Date: September 5, 2022

### Topic: Inside the Protocol (BGP)

### Recall

BGP maintains sessions between routers

BGP at one router

Multiple routing systems working together

### Notes

- Two neighboring BGP routers maintain a “peering session” or “adjacency”
    - Messages exchanged:
        - OPEN
        - NOTIFICATION - send an error
        - KEEPALIVE
        - UPDATE - shares routing information
            - Withdrawn routes
            - Next hop - IP addresses to which packets should be forwarded
            - Multi-exit discriminator and local preference
            - AS_PATH or AS_SET
            - Network layer reachability information
- RIB - routing information database

![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled%203.png)

- Full mesh design
    - a knows next hop is c but d and e don’t because they are running interior routing
    - Step 1: Construct iBGP sessions between each eBGP router and each interior router
    - Step 2: construct dereferenced forwarding table
        
        ![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled%204.png)
        
- How inter and intra-domain routing interact depend on AS architecture
    - Interior routers have default router to any boarder router
    - iBGP full mesh between routers (O(n^2) TCP connection)
    - iBGP route reflections
        - One router redistributes routers to all other routers with n-1 TCP connections for n routers
    - Full seperation: tunnels
        - interior routers need no knowledge of external world, border routers tunnel packets between each other
        - Modern design approach used for large networks

<aside>
📌 **SUMMARY: BGP routers maintain a peer session with each other, route based on policy, and orchestrate internal traffic (full mesh, route reflections, tunnels)**

</aside>

---

### Date: September 5, 2022

### Topic: Border Gateway Protocol

### Recall

AS

BGP

eBGP

iBGP

### Notes

- BGP is the only widely-used interdomain routing protocol
- Built around concept of autonomous system (AS)
- BGP
    - path vector routing procol
    - Adds metadata and decision-making features
    - Originiate IP subnets as destinations
    - Advertise and learn routes externally - *eBGP*
    - Propagate learn routes internally (within AS) - *iBGP*
- Policy, not distance, selects path

![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled%205.png)

<aside>
📌 **SUMMARY: BGP is made of two sub-algorithms (eBGP and iBGP) and it decides paths based on**

</aside>

---

### Date: September 5, 2022

### Topic: Building Planetary-Scale Routing with BGP

### Recall

![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled%206.png)

Changes for internetworking across domains

### Notes

- Routing policies differ
    - Many networks try to minimize own cost rather than e2e performance
    - Privacy and internal topologies may be sensitive
    - Security - what networks are trustworthy?
    - What routing algorithm to use when no agreement on goal?
- Previous routing algorithm were better at local decision making

![Untitled](Week%205%20-%20Planetary%20Scale%20Routing%2084e0fd9a463c466e99a977cc5ed85b4b/Untitled%207.png)

<aside>
📌 **SUMMARY: The internet is a big place and the many autonomous systems that are apart of the internet may not agree on common goals.**

</aside>