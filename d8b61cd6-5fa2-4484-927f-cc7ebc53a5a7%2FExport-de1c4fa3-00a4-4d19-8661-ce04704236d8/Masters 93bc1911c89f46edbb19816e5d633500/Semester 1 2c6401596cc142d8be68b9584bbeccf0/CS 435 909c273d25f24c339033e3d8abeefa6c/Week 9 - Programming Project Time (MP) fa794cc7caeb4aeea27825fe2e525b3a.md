# Week 9 - Programming Project Time (MP)

### Date: October 9, 2022

### Topic: Routing MP

### Notes

- Helpful setup hints
    - Use the external JSON library as format for passing information back and forth
    - Use C++, create as many files as you want using `#pragma once`
        - Compile with g++ and add -g flag for extra debug information with gdb
        - Use std::thread, std::atomic, std::mutex
    - sudo iptables —flush (fixes internet issues)
- Manager is defined for us
    - IPtables is like a firewall defining what can and cannot be listened to
    - Each node is a spun up process of what we write in this MP
        
        ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled.png)
        
- What needs to be done
    - Implement a shortest path routing algorithm
    - Route packets from source to destination
    - Update routes based on configuration changes (cost changes, failures)
    - Linux iptables define virtual network interfaces for nodes to use
- Environment setup
    - `sudo iptables --list`
    - `ipconfig` to grab value to replace eth0
    - Nodes are give the ipaddress 10.1.1.n where n is [0,255]
- Key tasks
    
    ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%201.png)
    
- Implementation - your code
    - Starter code in the assignment files (main.c & monitor_neighbors.h)
    - Running the code: `./<router_binary> nodeid initial_costs_file logfile`
        - `nodeid` - virtual interface number for this node
        - `initial_costs_file` - is the cost file
            - Each line the nodeid and cost is provided, missing entry means a cost of 1, neighbor link may not exist
        - `logfile` - where program writes events it was a part of, all nodes must make a log file even if no event happens
        
        ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%202.png)
        
        ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%203.png)
        
    - Broadcast the heartbeat with a loop from 0…255
    - First a node reads values from initial cost file, can have cost between nodes that are down!
    - Logging implementation
        
        ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%204.png)
        
- Recommended steps
    - UDP functions
    - Pass JSON payload around
    - Implement router algorithm
        - Define data structure to store graph information
        - Define data structure to store forwarding table
    - Implement heart beating with threading
- JSON
    
    ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%205.png)
    
- Need to convert when sending ints to the network
    
    ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%206.png)
    
- Other tips
    
    ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%207.png)
    

### Date: October 15, 2022

![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%208.png)

- Probably going to need to serialize the json before sending it
    - Use the header format of 2-byte magic number then 8-byte size then JSON
- What are the routing algorithms
    - Link state - what neighbors does each node in the network currently connect to
    - Path vector - what are the paths that m y neighbors have to all other reachable nodes
        
        ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%209.png)
        
- Remember to follow tips
    
    ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%2010.png)
    
- Link state
    - Distribute all local information globally
    - Each router runs shortest path algorithm to compute its forwarding table
        
        ![Untitled](Week%209%20-%20Programming%20Project%20Time%20(MP)%20fa794cc7caeb4aeea27825fe2e525b3a/Untitled%2011.png)