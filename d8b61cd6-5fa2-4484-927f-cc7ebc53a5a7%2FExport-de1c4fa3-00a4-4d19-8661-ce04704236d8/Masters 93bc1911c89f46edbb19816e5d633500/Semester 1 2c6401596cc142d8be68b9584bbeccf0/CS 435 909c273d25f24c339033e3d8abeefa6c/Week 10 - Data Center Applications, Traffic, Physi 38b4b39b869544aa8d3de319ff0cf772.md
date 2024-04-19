# Week 10 - Data Center Applications, Traffic, Physical Structure

### Date: October 6, 2022

### Topic: Quiz

### Recall

Probability distribution of flows by size

- 70% of flows are at most 1000 kilobytes in size

Cumulative distribution function of flows by size

- 70% of flows are at most 1000 kilobytes in size

Suppose you have a large pool of identical servers hosting a replicated service. Further, assume that the request-response time for the service is random, with the following distribution: 10ms for 99.9% of the requests but 1 second for the remaining 0.1%. Assume requests are completely independent. If you make 100 requests in a batch in parallel, what is the probability that your batch of requests takes 1 second?

- ~10%

In real systems, as opposed to the hypothetical setting in Question 3, what might cause requests to **not** be independent?

- Under high load at servers, service times for requests may be higher
- Network congestion from other requests may increase service times.

How many servers does a complete fat-tree topology (as in this paper: [A Scalable, Commodity Data Center Network Architecture](http://ccr.sigcomm.org/online/files/p63-alfares.pdf)) built using switches with 6 ports (i.e., k = 6) support?

- 54

Is the fat-tree topology (as in this paper: [A Scalable, Commodity Data Center Network Architecture](http://ccr.sigcomm.org/online/files/p63-alfares.pdf)) a tree, i.e., does it have a loop-free structure?

- No

How many paths exist in a fat-tree topology (as in this paper: [A Scalable, Commodity Data Center Network Architecture](http://ccr.sigcomm.org/online/files/p63-alfares.pdf)) from an arbitrary root switch downward to an arbitrary server? Consider only minimal-length paths.

- 1

With the switches marked with "X" eliminated, are these two topologies identical? For example, would they have identical failure responses?

- No

How does the number of cables in a fat-tree topology (as in this paper: [A Scalable, Commodity Data Center Network Architecture](http://ccr.sigcomm.org/online/files/p63-alfares.pdf)) scale with port-count of the individual switches used to build it, i.e., the parameter *k*? Ignore constant factors.

- $k^3$

What are some of the benefits of being able to deploy larger clusters of servers connected at high bandwidth? (Feel free to refer to this week’s readings.)

- Applications need not be restricted to within-rack deployment and can achieve higher scale.
- Larger clusters with high bandwidth improve the ability to pack jobs into the servers – in more restricted environments, under-utilized servers can be isolated from each other, making it difficult to use them together for tasks. This leads to under-utilized, fragmented infrastructure.
- Large clusters with high bandwidth allow spreading data across different failure zones (for example, across rows of racks which have different power supplies).

---

### Date: October 8, 2022

### Topic: Physical Structure

### Recall

Lots of physical infrastructure 

Big switch approach

Tree approach

Clos networks

Fat-tree network

### Notes

- Need power supply, agreeable weather, cables going in and out of the data center
- The “big switch” approach has a “big crossbar” at the top connecting all the internal racks
    - The “big crossbar” would be very hard to implement and require n^2 connections
        
        ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled.png)
        
    - Perhaps the simplest approach but big switch needs high locality to work well and is very expensive… and… it scales poorly because port limitations
- Tree approach is similar to the “big switch” idea but just add multiple layers
    - Little better at scaling but can have congestion at the top level when servers on one side try to talk to the other side
        
        ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%201.png)
        
- Clos networks were originally developed in the 1950s for telephones
    - Advantage: use small cheap elements to build a large network
    
    ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%202.png)
    
- Fat-tree was inspired by the clos network
    - Can be scaled by increasing the number of layers or number of ports at each layer
    - Provides large number of redundant paths
        
        ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%203.png)
        
        ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%204.png)
        
    - Lots of cables and the longer the cable the more likely it will need to be optics which is expensive

<aside>
📌 **SUMMARY: Example internal data center topologies include: big switch, tree, clos, and fat-tree.**

</aside>

---

### Date: October 8, 2022

### Topic: Application and Traffic Patterns

### Recall

Scatter-gather traffic pattern

What does data center traffic look like?

Implications of networking

### Notes

- Scatter-gather
    - Example: a web search
    - Process to scatter and gather at the end
        
        ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%205.png)
        
- A majority of internet traffic is within data centers (inside not going out) instead of across the internet
    
    ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%206.png)
    
- Example: Google for fault tolerance has spread data around reducing locality and increasing network demands
- **Implications for networking:** data center internal traffic is big, tight deadlines for network I/O, congestion and TCP incase, need for isolation across applications, centralized control at flow level may be difficult
    - Variable latency is large problem (99% of requests are 1ms but 1% are 1s long means that when making lots of requests in data center there will be high overall latency)
        - Can accept poorer performance by disregarding slow requests or making multiple requests and only using the fastest
    - TCP doesn’t work well inside a datacenter
    - If poor isolation then one slow application will slow the entire network
    
    ![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%207.png)
    

<aside>
📌 **SUMMARY: Data centers have loads of internal traffic.**

</aside>

---

### Date: October 8, 2022

### Topic: Intro to Part 2 of the Course

### Recall

Cloud computing stitches together hundred of thousands of computers combining compute and storage with networking

### Notes

![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%208.png)

![Untitled](Week%2010%20-%20Data%20Center%20Applications,%20Traffic,%20Physi%2038b4b39b869544aa8d3de319ff0cf772/Untitled%209.png)