# Week 8 - Application Layer and Security

### Date: September 28, 2022

### Topic: Quiz

### Recall

- The mapping from DNS names to IP addresses is
    - many-to-many (each name may have one or more IP addresses, and each IP address may have zero or more names)
- When a host wants the IP address of a host name, the request is typically first sent to a
    - Local DNS server
- Which of the following is true of denial of service (DoS) attacks? Check all that apply.
    - It often happens that the sources that flood the targeted servers in DDoS attacks are also compromised.
    - DoS is typically accomplished by flooding the targeted servers with superfluous requests.
- Suppose a host is at IP address 1.2.3.4, to which the domain name host.whatever.org is mapped. The host then moves to a different network where it has IP address 5.6.7.8. In order for clients to (eventually) find the host by looking up host.whatever.org, which kinds of DNS servers MUST be updated? Check all that apply.  (Note: "updated" here refers to updates outside of what happens automatically within the DNS system – like a human administrator making changes, or running a script that makes changes.)
    - Authoritative DNS server
- Consider the case of the previous question and suppose DNSSEC is in use throughout the DNS system. In this case, after the host moves, which kinds of DNS servers MUST be updated? Check all that apply.
    - Authoritative DNS server
- Consider the case of the previous two questions. How can the host ensure that all clients will definitely be able to find the host by looking up host.whatever.org, 5 minutes after its address change?
    - Ensure TTL on the domain name is less than 5 minutes
- The DNS system reduces the number of queries a client needs to look up names via:
    - Caching
- Suppose a client is querying host.whatever.org using a typical local DNS server as a recursive resolver, and that no involved party has any DNS records cached. Assume the authoritative server for whatever.org will return the record for host.whatever.org. How many servers are involved in the name lookup process?  (Assume the client is not a server.)
    - 4 (the local DNS server, a root server, a TLD server, authoritative for URL)
- In the scenario of the previous question, but now with caching, what is the minimum number of servers that may be contacted?
    - 0 (client itself may have name cached)
- Suppose client Alice queries a DNS server Bob, but eavesdropper Eve observes the communication. If all parties are employing DNSSEC, what can Eve see? Check all that apply.
    - The name Alice is querying
    - The IP address(es) associated with this name in Bob’s response
    - Bob’s public key
    - Bob’s digital signature of the response
- In DNSSEC, assurance of authenticity of a response is directly or indirectly dependent on which of the following? Check all that apply.
    - Digital signatures by DNS servers other than the authoritative DNS server
    - The digital signature by the authoritative DNS server of the answer
- An attacker is located at IP address 50.0.0.5, and will mount a DNS reflection and amplification attack against a victim at 2.0.0.5.  The attacker’s local DNS server is at 50.0.0.2, and the victim’s local DNS server is at 2.0.0.2. For most or perhaps all packets the attacker sends to conduct the attack, what IP source address will it use?
    - 2.0.0.5
- In the scenario of the previous question, for most or perhaps all packets it sends to conduct the attack, the attacker will use what IP destination address?
    - Other

---

### Date: September 26, 2022

### Topic: Security of DNS: Availability and DDos

### Recall

Attacks on DNS

DNS as attack vector

DNS security conclusions

### Notes

- Most common attack - resource exhaustion commonly through legitimate operation but with illegitimate quantity
    - Distributed denial of service (DDoS) attack uses many agents to exhaust resources
    - When DNS is down then website is effectively down because no one knowns IP
- Trick 1 - reflection
    - UDP-based DNS is connectionless so attacker will spoof its source address then DNS will send to victim thus overwhelming victim
        
        ![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled.png)
        
- Trick 2 - amplification
    - Small query but large answer
    - DNSSEC will produce a large answer because it has keys attached to message making them bigger
- DNS confidentiality can be solved using public-key crypto over HTTPS/TLS
- Integrity and authentication solve by DNSSEC
    
    ![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled%201.png)
    

<aside>
📌 **SUMMARY: DNS is both vulnerable to attack and can be used as an attack vector with reflection and amplification causing huge damage.**

</aside>

---

### Date: September 26, 2022

### Topic: Security of DNS: Confidentiality, Integrity, and Authenticity

### Recall

What is information security?

Is DNS secure?

How to improve DNS?

DNSSEC

Confidentiality with DNS

### Notes

- Confidentiality (people cannot read connection), integrity (message should arrive and not be altered), authenticity (communicating parties know the identity), availability (no one can take connection down)
- DNS is vulnerable in all of the above areas…
- Public key cryptography - communicate party A has pair of keys
    - Private key (used for encryption)
    - Public key (used for decryption)
        
        ![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled%202.png)
        
    - The person with private key can create signatures that are unique
        
        ![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled%203.png)
        
- DNSSEC - cryptographically sign DNS responses while building a chain of trust (use DNS hierarchy to cryptographically validate identity)
    
    ![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled%204.png)
    
    - DNSSEC solves integrity and authenticity problems
- DNS(SEC) over HTTPS but no standardization yet

<aside>
📌 **SUMMARY: On its own DNS is completely insecure but DNSSEC uses public key cryptography to solve for integrity and authenticity.**

</aside>

---

### Date: September 26, 2022

### Topic: The Domain Name System (DNS)

### Recall

History of IP mapping

DNS

How to use DNS

How to speed up DNS

DNS responses

### Notes

- IP addresses are great locators but IP addresses are tied to specific interface and they aren’t memorable
- Original solution - a physical address book (lol)
- DNS - a distributed database mapping names to addresses
- Top level hierarchy - root DNS servers
    - Top level domain (TLD) servers - .com/.edu/.uk/etc responsible for knowing IP addresses in that domain
        - Authoritative DNS servers - responsible for knowing name-to-ip mappings
- Name allocation and database insertion
    - Company registers unallocated name
    - Name registrar inserts mapping into top level (TLD) servers
    - Company’s server creates DNS records
        
        ![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled%205.png)
        
- Many queries involved with DNS lookup because client has to ask multiple levels and DNS servers will have huge load
    - Solution - caching, each DNS answer comes with a TTL (timeout)
    - Solution 2 - recursive name resolution
- Local DNS server acts on behalf of client as recursive resolver
    - The local DNS server will get better caching because working on behalf of many clients
    - Local DNS servers may not be physical local, they could be global public service (eg Google 8.8.8.8 and Cloudflare 1.1.1.1)
    
    ![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled%206.png)
    
- A type (map name to IP address), NS type (map domain to DNS server), CNAME (map name to canonical name), MX type (list name of email server associated with domain)
- DNS sits on the top level application layer and it could be moved down as a better architectural choice

![Untitled](Week%208%20-%20Application%20Layer%20and%20Security%20ebb7fd5aed644f7499977cadae429d79/Untitled%207.png)

<aside>
📌 **SUMMARY: DNS is a hierarchical database that attaches IP addresses to domains.**

</aside>