# Week 13 - Wide-Area Networking for Cloud Computing

### Date: November 21, 2022

### Topic: Quiz

### Recall

- WAN link
    - By delaying the background traffic such that that 60% worth of the link’s capacity is spread across the next three time slots (20% each), you’d achieve 40% utilization throughout. Equivalently, you could operate with only 40% of the original scenario’s bandwidth. The point is that if you can differentiate services in terms of their network requirements; you can use traffic engineering to save expensive WAN bandwidth. This is one of the motives underlying both Google and Microsoft’s inter-DC WAN designs.
    - **.4**
- What are some of the benefits of having multiple geo-distributed data centers?
    - **Load balancing across sites**
    - **Lower latency for clients in multiple regions**
    - **Data availability in case of a natural catastrophe at one site**
- Which of the following techniques does Google’s B4 use for scalability?
    - Of course, there are other techniques too. The question only asked you to identify one from the list. B4 does not artificially restrict sites from communicating just for scalability, nor does it use a completely distributed design – there is centralized control implemented in an SDN style, although each site gets to locally make certain decisions as well. Please refer back to the lecture for more information.
    - **It aggregates links as well as traffic flows between pairs of sites.**
- Link fairness
    - All of the four individual flows get 0.5 units of flow. This results in the red application (with two flows) getting 1 unit of flow. The point is that link-level fairness may not result in application-level fairness (if that is a desired objective). The even broader point is that fine-grained traffic engineering can benefit from a network-wide, application-wide view. However, system constraints can get in the way of doing this – if you have many many applications and a very large number of nodes/sites and links, fine-grained traffic engineering may not be possible to scale. Even for a small number of sites, scaling techniques like B4s (in the above question) may be necessary.
    - **Red: 1 unit, Blue: 0.5 units, Green: 0.5 units**
- What is a TCP cookie?
    - **A cryptographic token included in a client’s request to a server, authenticating the client to the server and allowing the server to send data without completing a 3-way TCP handshake with the client**
- You’re sending 100 kilobytes of data from Chicago, USA to New Delhi, India (a distance of roughly 12,000 kilometers).  Assume that the bottleneck bandwidth on the route is x Gbps. How long does it take?
    - **Even if the Internet operated at the speed of light in a vacuum, at least 40 milliseconds**
- In which of these cases does caching of web data not help?
    - **Dynamic data (e.g., stock prices)**
    - **Personalized data**
    - **Encrypted data**
- Round trip from China map
    - **2.4**
- With CDN
    - **.55 seconds**
- Latencies with BGP
    - We can route between B and D through C, as long as we have servers (or routers) at C. This will save 20ms because of the triangle inequality violation between B, C, and D. Further, if the BGP-given route between A and E is A-C-D-E, then A-B-E could be made available by using an overlay.
    - **Yes**
- How does 8.8.8.8 achieve low latency from several different parts of the world? A single physical server cannot be within 10ms of both Singapore and New York.
    - **It uses IP anycast – the same IP address is announced to Internet peers from multiple locations, whereby clients in different locations reach different close-by instances of the service, even though they’re sending packets to the same address.**
- What factors might govern the choice of a CDN node to serve a request? (**Check all that apply**)
    - Physical distance is something that may impact network distance. The latter is what we care about directly. In some cases, it may be quite different from physical distance, for example, due to persistent routing scenarios where certain ISPs don’t have short routes to ISPs in the geographical neighborhood. In such a case, physical distance could be small between two communicating parties in these ISPs, but the network distance could still be large.
    - **Estimated latency to the client from different locations**
    - **Load at different CDN locations**
- Name resolution entries are cached in local DNS servers close to clients. What settings are appropriate for time-to-live (TTL) for name resolution cache entries for CDNs?
    - Having a long TTL for the CDN resolver means that one doesn’t have to query the TLD every time. The resolution for the CDN resolver is quite stable over time. However, for the individual clusters, the CDN resolver itself would like to make decisions over finer timescales based on present load and performance, and thus, having shorter TTLs is desirable.
    - **Short TTL for entry pointing to a specific cluster, longer for the entry pointing to the CDN resolver (which is further responsible for resolving names to a cluster)**
- Why might services like OpenDNS and GoogleDNS interfere with CDN operation?
    - It’s worth noting that the use of EDNS is meant, in part, to mitigate this problem, but it’s not clear what the extent of EDNS use is.
    - **Using such services can mean that the client and its DNS resolver are not located near each other, and thus, the CDN’s estimates for performance for the client can be incorrect.**
- Suppose you have a large pool of identical servers hosting a replicated service. Further, assume that the request-response time for the service is random, with the following distribution: 10ms for 99.8% of the requests, but 1 second for the remaining 0.2%. Assume requests are completely independent. If you make 100 requests in a batch in parallel, what is the probability that your batch of requests takes 1 second?
    - The likelihood that your batch needs 1 second is the same as the probability that at least one of the requests takes 1 second, and equivalently, *not all requests take 10ms*. What’s the probability of all requests taking 10ms? 0.998100, which is roughly 82%. So the probability we want here is roughly 18%.
    - **~18%**
- 3 or more replicated and no response
    - If you think of an individual query taking 1 second as a “success” (in the sense of events we are looking for; obviously, in the systems sense, this is a bad thing, not a success), then the probability of a success is given to be 0.002 (1 – 0.998). This question is asking the probability of 3 or more successes in 100 trials. You can use the binomial calculator to compute the value to be around 0.0011, which is quite small. The larger point is that the overhead of this replication can be quite minimal.
    - **~.1%**
- Further, in the above scenario (with the replication after 10ms), let’s assume that we have to replicate exactly 3 requests after 10ms. What is the likelihood that our batch of requests *still* takes 1 second?
    - 1 - 0.9983, i.e., roughly 0.6%. As you see in this example, replicating a small fraction of requests (which is the likely case, as you saw in the previous question) can get us much better chances of completing a batch of queries fast.
    - **~.6%**
- What types of overhead might we pay in general for request replication?
    - **Higher load on the servers serving the requests**
    - **Client-side cost of making the replicated queries**
    - **Additional network load from the additional requests and responses**
- Which of the following methods can applications themselves use to deal with TCP incast? (Check all that apply)
    - **Limit the size of individual responses so switches can accommodate more simultaneous responses in their buffers**
    - **Ignore one or more late responses, thereby being more tolerant to latency variations**
    - **Deliberately space out requests and responses to reduce the chances of incast**
- Bit rate
    - The traditional approach is to reduce the bit-rate if estimated capacity is smaller than the current rate. Refer back to the lecture for more details.
        
        ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled.png)
        
- Now suppose that in the above scenario, you were using the buffer-based algorithm described in the lecture (ignoring for a moment the fact that that algorithm is unlikely to have given you that sequence of bit-rates). How does the buffer-based algorithm react to the buffer occupancy in requesting the next chunk?
    - The buffer-based algorithm does not look at capacity estimates, except for a brief period when it is starting up and buffer occupancy does not give enough useful information. If the buffer occupancy is high, as shown here, then a high bit-rate chunk will be requested.
    - **It requests a chunk at a large bit-rate, close to the maximum, because the buffer occupancy is high.**

---

### Date: November 21, 2022

### Topic: Coping with Network Performance: Video Streaming Adaptation in Face of Variable Bandwith

### Notes

- Buffer used to mask differences in bandwidth availability
- Common solutions
    - Encode video in multiple bit rates and choose the one that matches available bandwidth
        
        ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%201.png)
        
    - Adaptive bit rate streaming
    - Decide based on buffer size alone?
        - Full buffer —> up video quality
        - Low buffer —> lower quality

---

### Date: November 21, 2022

### Topic: Coping with Network Performance: Application-layer Tweaks for Lower Latency

### Notes

- The only way to ensure reliability is at the application layer
- Latency long tail
    - Cassandra - rapid read protection allows coordinator to monitor outstanding requests and automatically send new requests if taking a long time
    - Replication of small fraction of requests can drastically speed up jobs
- Incast
    - Two many send request to same port overwhelming port causing high packet loss

---

### Date: November 19, 2022

### Topic: Client Connectivity

### Recall

Bandwidth vs latency

### Notes

- Web browsing is latency bound while video streaming is bandwidth bound
- Latency costs money (decreasing Google searches and Amazon purchases)
- Latency is the harder problem to solve
    
    ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%202.png)
    
- Internet is very slow
    
    ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%203.png)
    
- Bare metal latencies on the internet are high
    
    ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%204.png)
    

---

### Date: November 19, 2022

### Topic: CDNs

### Recall

Static caching isn’t enough

CDN=Content distribution networks

Steps to CDN

### Notes

- Static caching is not enough
    - Volume and diversity of content is a lot to cache
    - Content is more dynamic
    - Lots of encryption which can’t be cached
1. Spread content servers globally
2. Network the sites and the origin
    
    ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%205.png)
    
3. Direct clients to appropriate servers
- More options if you control the infrastructure
- Many companies rely on CDN provider like Akamai
- DNS customized by location
    - DNS responds depends on local DNS resolver’s guessed location
- Any cast routing (8.8.8.8)
    - Announce same BGP prefix from multiple locations

---

### Date: November 19, 2022

### Topic: Inter-Data Center Networking: Cutting-edge Solutions

### Recall

Common themes of WAN

Industry solutions

### Notes

- Themes
    - Diversity of services (some won’t care about latency)
    - Centralized TE using SDN, OpenFlow
    - Exact linear programming is too slow (heuristics required)
    - Dynamic reallocation of bandwidth
    - Edge rate limiting
- Google’s solution is called B4 circa 2011
    - Google keeps BGP as big red button backup
    - Google is using custom hardware
    
    ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%206.png)
    
    - TE = traffic engineering server, interacts with all datacenters

---

### Date: November 19, 2022

### Topic: Inter-Data Center Networking: The Problem

### Recall

Why multiple data centers?

MPLS

Drawbacks of MPLS

### Notes

- Data availability, load balancing, latency, local data logs, hybrid private cloud model
- WAN - wide are network

![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%207.png)

- CDN - content distribution network
- Traditional WAN approach - MPLS
    - Multi protocol label switching
    - WAN amortization is super expensive for large orgs
        
        ![Untitled](Week%2013%20-%20Wide-Area%20Networking%20for%20Cloud%20Computing%20a8dce5bd29cf48d8afec0ce8f77f086c/Untitled%208.png)
        
- Problems of MPLS
    - MPLS does not have global view so difficult to differentiate by service
    - Provides only link level fairness (doesn’t mean network wide fairness)
    - Local router level choices are greedy so traffic engineering sub optimal