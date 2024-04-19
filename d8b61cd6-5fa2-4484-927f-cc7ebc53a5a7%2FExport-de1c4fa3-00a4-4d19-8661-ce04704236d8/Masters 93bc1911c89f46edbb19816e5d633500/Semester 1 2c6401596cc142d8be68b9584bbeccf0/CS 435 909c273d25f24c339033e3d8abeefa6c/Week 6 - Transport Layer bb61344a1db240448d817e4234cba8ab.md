# Week 6 - Transport Layer

### Date: August 5, 2019

### Topic: Quiz

### Recall

- What services are provided by UDP? (Check all that apply.)
    - Unreliable datagram delivery
    - Multiplexing multiple connections to processes running at the same IP address
- What services are provided by TCP? (Check all that apply.)
    - Ongoing connection between sender and receiver
    - Multiplexing multiple connections to processes running at the same IP address
    - Reliable byte stream data delivery
    - Flow control
    - Congestion control
- Communication offered by TCP is:
    - Full-duplex (simultaneous communication between both parties)
- In a sliding window protocol, if SWS=RWS=8, at least how many bits should the sequence number space have?
    - 4
- In TCP slow start prior to timeout occuring, what happens to congestion window size over the course of one RTT?
    - Multiplied by 2
- Four nodes are connected in series: A – B – C – D. The three links have bandwidth 4 Gbps, 75 Mbps, and 80 Mbps, respectively. The three links have physical lengths 25 km, 400 km, and 10 km respectively. The links are full duplex. The rate of transmission errors on the links, the switching time at B and C, and the time to transmit an ACK are all negligible and can be ignored. A large file is to be sent from A to D, and there is no other traffic on the links. Packets are 1000 B, including headers. Use the definition that 1 Mbps = 1,000,000 bits per second. Ignoring reliability and packet headers, what is the maximum throughput that can be achieved?
    - 75 Mbps
- In the setting of the previous question, suppose the links are optical fiber, and keep in mind that the speed of light in optical fiber is roughly 66% of the speed of light in a vacuum. What is the approximate RTT of the A-D connection, in milliseconds? (You can assume that there is no congestion in the network, and give an answer for very small packets, so that the RTT comes from propagation delay rather than transmission delay. Give at least two digits of precision after the decimal.)
    - 2*((25+400+10)x10^3)/(.66*299792458)=.0043969=4.3969
- In the setting of the previous question, what throughput will be achieved by the Stop and Wait protocol, in KB/sec?
    - 227.79kb
- In the setting of the previous question, suppose A and D are running a sliding window protocol. What is the smallest window size in KB that can achieve the maximum throughput of the physical path?
    - **(75*125)*(4.3969x10^-3)=**41.2209375 (bandwidth throughput of network)
- If a transport connection’s throughput is 80 Mbps and RTT is 10 milliseconds, MTU is 1000 bytes and packets are sent using the full MTU, what is the maximum number of packets that will be transmitted before an acknowledgement is received?  (Ignore packet header size.)
    - 100 packets
- Suppose a TCP session A is transmitting on a 100 Mbps bottleneck link, and reaches the full bottleneck rate. A second TCP session B begins sharing the same bottleneck link to stream a movie. Initially, session B is streaming at a low frame rate topping out at 10 Mbps, but then the user increases the quality to Super Ultra HD so that session B is no longer application-limited and always has application data ready to send. Assume both flows continue indefinitely, and have the same RTT. After some time passes, the average rate for each flow will be:
    - About 50 Mbps for session A and 50 Mbps for session B
- What is the main mechanism within TCP that produces the outcome of long-term average sending rates in the previous question?
    - Additive Increase, Multiplicative Decrease
- In general, when N TCP senders share a single bottleneck link in the real world, which of the following are true?
    - The senders may oscillate around an equal split where each sender gets 1/N of the throughput, sometimes sending slower and sometimes sending faster.
    - The senders may have unequal long-term average rates if their RTTs differ.

---

### Date: September 25, 2022

### Topic: Transmission Control Protocol (TCP)

### Recall

TCP as the Jack of all trades

Theory vs Reality

Active work in transport protocol

### Notes

- Process-level multiplexing
    - Port number (distinct from UDP)
- Connection oriented employing three-way handshake
- Reliable byte stream using sliding window protocol
    - Bi-directional data flow with loss detection via RTT
- Flow control - window based rate limiting
- Congestion control - slow start, exponential acceleration, AIMD congestion control
- Theory
    - Find approximate rate with exponential increase and e2e algorithm converges to efficiency
- Actual
    - Many flows never exit slow start
    - Slow converge because additive increase is slow and loss signal only happens after router queue fills up
    - Application performance goal is not clear (latency vs throughput)
- Ongoing research for transport protocols
    - In-network mechanisms like explicit feedback or queue management
    - Endpoint mechanisms like new control algorithms or incorporating other congestion signals
    - Transport products - custom solutions like Google’s QUIC

<aside>
📌 **SUMMARY: TCP provides multiplexing, connection, reliable byte stream transfer, flow control, and congestion control. The transport layer is not a solved problem and still undergoes a lot of active research.**

</aside>

---

### Date: September 25, 2022

### Topic: Congestion Control Design

### Recall

Inferring congestion

Slow start phase

Congestion avoidance algorithm

AIMD

Flow vs congestion control

### Notes

- No widely-adopted mechanism in IP for routers to tell endpoints of congestion so sender must infer congestion
- Infer congestion via loss - inferred from packet loss which is inferred from packet being very late compared with RTT estimate
    - Can also infer congestion via latency increase
- Slow start phase - idea start cautiously because no capacity information is available
    
    ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled.png)
    
- If signal of congestion, slow down; otherwise speed up
    
    ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%201.png)
    
- AIMD converges to perfect efficiency
    - Decrease is like a tax on everyone and additive increase is like redistribution
        
        ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%202.png)
        
    - Average sending rate may be suboptimal but hovers around equilibrium
    
    ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%203.png)
    
- Congestion control is one of the long standing challenges of networking
    - Flow control - one resource, explicit declaration
    - Congestion - dynamic applications and complex environment
        
        ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%204.png)
        

<aside>
📌 **SUMMARY: Congestion control uses a slow start phase then AIMD to setup then converge to an equilibrium that shares resources efficiently.**

</aside>

---

### Date: September 25, 2022

### Topic: Congesting Control Introduction

### Recall

Features of the transport layer

Rate control 

Controlling rate in sliding window protocols

Flow control

Congestion control

### Notes

- Transport layer features
    
    ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%205.png)
    
- Why control sending rate?
    - Sending rate can exceed what receiver can handle
    - Sending rate can exceed what network can handle
    - Too slow - poor throughput
    - Too fast - increased latency and packet loss
        - Goodput - throughput delivered to app (vs throughput sent through the network - different because dropped packets)
- Pace controls
    - Can use window size to control rate
        - In general rate = SWS / RTT
    - Packet pacing - duplicity limit timing between packet sends
        
        ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%206.png)
        
    - Flow control
        
        ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%207.png)
        
        - Traditional TCP mechanism - limit window
            - Upon congestion slow down otherwise speed up resulting in oscillation around optimal

<aside>
📌 **SUMMARY: Packet sending must be regulated using either flow control or congestion control in order to stop pack loss or poor throughput.**

</aside>

---

### Date: September 25, 2022

### Topic: Sliding Window Protocols

### Recall

Stop and wait is too slow

Pipelining

How to generalize stop and wait

Sender side of pipelining send and wait

Receive side of pipeline send and wait

ACK messages

Window sizes

Sequence numbers

### Notes

- Problem with stop and wait
    - Its the stopping and the waiting - only one packet “in flight” at a time resulting in low throughput
- Designing a process involving sequence of stages where each stage can begin processing next test before last task has been completed
- Sliding window will keep track of multiple outstanding messages
    
    ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%208.png)
    
    - Sender side
        - Setup - fixed send window size (SWS), maintain state of each message in window
            - Ready (unsent), Sent (but not ACKed), ACKed
        - When message in window is Ready
            - Send each message (in stream order)
        - When ACK arrives
            - If ACK outside window - ignore
            - Mark specified packets as ACKed, while leftmost message is ACKed slide right
        - On timeout of sent packet
            - Move back to Ready state
    - Receiver side
        - Fixed receive window size (RWS) (equal or not equal to SWS)
            - Ready (unsent), Sent (but not ACKed), ACKed
        - When message arrives
            - If message falls outside window, ignore
            - Mark messages as received
            - Send ACK
            - While leftmost message is Received
                - Deliver to application, slide right
- What should we put in ACK?
    - Single-message, cumulative, SACK (selective ACK)
    
    ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%209.png)
    
- What are windows measured in?
    - Bytes
- How big should window be?
    - Smallest window that keeps the link busy
    - SWS = bandwidth-delay product (BDP) = connection throughput x RTT
        - Connection throughput x RTT allows sender to send at full rate
    - Allows sender to send at full rate
    
    ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%2010.png)
    
    - TCP seq# uses 32 bits so will wrap after 4GB
        - Number of sequence numbers ≥ SWS + RWS

<aside>
📌 **SUMMARY: Pipelining the stop and wait protocol (reliable byte stream) results in higher performance.**

</aside>

---

### Date: September 20, 2022

### Topic: Reliable Byte Stream Transport

### Recall

What is the goal of a reliable byte stream?

Designing a protocol

ACK messages

Stop and wait protocol

### Notes

- Goal - build a reliable byte stream service (built on top off unreliable datagram service
    - Connection establishment then data transfer then connection termination
    - Lots can go wrong: delivered, dropped, delayed, unordered, corrupted
- First idea - have the send wait for confirmation then resend if no confirmation
    - Successful delivery (ACK - acknowledgement message)
    - Unsuccessful delivery - timeout or negative acknowledgement (NACK)
    - Feedback via ACK & timeout mechanisms
        
        ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%2011.png)
        
        - What could go wrong - well we could have a lost ACK or we could have a delayed ACK
    - We need to clarify *what* was sent & received
        - Use a sequence number
            
            ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%2012.png)
            
            - Still a problem - lower *throughput* because only on unACKed packet in flight at a time so time depends on round trip time (very slow protocol)
                - Throughput = (MTU-headers)/RTT
            - Solution - need multiple packets in flight at once

<aside>
📌 **SUMMARY: To design a reliable byte stream protocol we need ACK messages as well as sequence numbers to determine ordering.**

</aside>

---

### Date: September 17, 2022

### Topic: Multiplexing Connections with UDP

### Recall

Multiplexing and demultiplexing among processes

How does connectionless multiplexing work?

How does connection-oriented multiplexing work?

User datagram protocol (UDP)

Takeaways

### Notes

- Multiplexing - multiple communication channels over one underlying channel
    - Mux - encodes data from multiple channels onto one
    - Demux - decodes data from one channel onto multiple
- Transport layer multiplex process-level communication over network layer
    - Connectionless - each message is independent (like a datagram)
    - Connection-oriented. - channel remains open until explicit closed
- Connectionless multiplexing
    - Parties - server (waiting to accept connections), client (initiates connection)
    - Step 1: each party creates a socket and binds to a specified port number
    - Step 2 - client knows address & port of server
    - Step 3 - knowing address and port the client sends a message to the server
    - Step 4 - server receives message
    - Step 5 - application responds (destination taken from the arrived packet)
- Connection is persistent so it needs an identifier
    - 4-tuple: source IP, source port, destination IP, destination port
- Functionality: IP + multiplexing, very simple protocol
    - Unreliable best effort service
        
        ![Untitled](Week%206%20-%20Transport%20Layer%20bb61344a1db240448d817e4234cba8ab/Untitled%2013.png)
        
    - Example: DNS and NTP run on UDP rails
    - UDP can often be enough and provide maximum performance and flexibility
- Minimal transport layer function - multiplexing (uses ports)
- UDP provides minimum service of the transport layer

---

### Date: September 11, 2022

### Topic: The Transport Layer: Introduction

### Recall

Layer differences

What the transport layer provides to applications

### Notes

- Network layer is about multi-hop communication across the network between hosts
- Transport layer is about communication between processes
- The transport layer has a harder job because it has to provide good performance and act like a stream to the observing processes
- Network layer provides abstraction of a tunnel offering best effort datagram service
- Goals of transport layer (what it can provide)
    - Multiplexing between processes - distinguishing amount multiple processes at the same IP host address
    - Connection abstraction - association between two communicating parties
    - Reliable byte stream
    - Rate control
- Multiple different transport protocols (unlike the internetwork layer which only has one option: IP)

<aside>
📌 **SUMMARY: The transport layer provides services to applications acting up the tunnel datagram abstraction that the network layer provides.**

</aside>