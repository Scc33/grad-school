# Week 1: Cloud Computing Foundations

# Cloud Computing Foundations

## Cloud Computing Introduction

- Software as service - user a providers applications over a network
- Platform as a service - deploy customer-created applications to a cloud
- Infrastructure as a service - run and provide access to physical hardware

![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled.png)

## Cloudonomics

- Utility pricing
    - Unit costs of cloud are more expensive than owning the resources but you can scale up and down
    - Suppose you need 200 resources to meet peak demand than you must always have 200 available even if the average is much smaller like 10
    - When utility premium is less than the ratio of peak demand to average demand
    - Hybrid can be a good option too because you can own resources to support the average and use cloud to scale up
        - Comparison: owning own car to drive around town and rent a car when traveling
- Benefits of common infrastructure
    - Comparison: this is like multiplexing in networking… its cheaper to be able to cram multiple applications into the same area
        
        ![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%201.png)
        
    - A fixed asset facility servicing highly variable jobs yields a low utilization
        - Multiplexing jobs with different distributions may increase smoothness
        - Addition n independent jobs reduces variance by $1/sqrt(n)$
            - Because of this the advantages of scale get smaller
        - Best case is negative correlation and worst case is positive correlation

## Big Data

- Definition - data set that is so large it is impossible to process on one computer
- Characterized by velocity, size, and complexity

# Tiers of Cloud Services

## IaaS

- Infrastructure as a service
    - Foundational service, most basic, and really enables everything built on top of it
    - Allows user to rent computing resources and the product is a virtual computer
    - Virtual computer/server can be accessed remotely and do whatever you want
- Virtualized resources
    - Different customers have different needs and it is difficult to offer every specific type required
    - Solution - cloud provider maintains a fleet of similar, powerful hardware
    - Chunks can be carved out of these powerful underlying computers
    - MaaS - metal as a service
        - Cloud provider rents you and entire box/computer
    - CPUs can often be somewhat shared resources but memory limits need to be stricter
- Advantages of IaaS vs on-prem
    - No need to run a datacenter
    - OpEx vs CapEx
        - scale up and down OpEx vs CapEx which is fixed
        - CapEx is up front
    - Faster innovation
- Examples
    - Microsoft Azure, Amazon EC2 (Elastic Compute Cloud), Google Cloud Platform Computer Engine
- Pricing
    - On-demand - some fixed rate that you pay as you need for that resource
    - Reserved - you pay up front to reserve a resource and you get a discount
    - Spot pricing - the cost floats depending on demand
- IaaS sub-category: containers and orchestration
    - Containers is a light-weight virtual machine
- Regions and zones (AZ - availability zones)
    - Cloud provider has physical datacenters around the world
    - Divide the world into ‘regions’ and subdivide regions into availability zones
    - The closer the data centers are the better the latency but the higher change of simultaneous failure
    - Zones are smaller than regions
        - Example: Region is AWS us-east-1 and AZ are us-east-1a … us-east-1f
        - Details of how these zones are implemented is often private and not relevant to customers because they logically work together
        - Local zone - is an extension of a region that allows you to pick data centers that are geographically close to users

## PaaS

- Platform as a service
- PaaS is more opinionated than IaaS and will make design choices about what the application will want
- Maintains infrastructure, manages available solutions (libraries, languages, databases, queues, etc), handles autoscaling, consistent data storage solutions, etc
- Web services and scale up vs scale out
    - Cloud is all about scaling out
    - Very simple idea of a webservice
        
        ![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%202.png)
        
    - When you need more compute or resources you add resources and stick a load balancer (reverse proxy) on top of it all
        
        ![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%203.png)
        
    - When more detail is required eventually you will scale databases
        - One database will be the master and the database servers will be helpers
            
            ![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%204.png)
            
    - However what if the computation is really intensive or takes a while…
        - We want the user to have quick response so have a web tier (presentation tier)
        - Separate the application tier (logic tier) that handles the computation
        - A queue links the presentation to the logic
            
            ![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%205.png)
            
    - This architecture is so common that many PaaS will offer a load balancer, a queue, and autoscaling
- Example of PaaS is AWS Elastic beanstalk
    
    ![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%206.png)
    
    - All the machinery is already provided and you can just drop in your application code
    - Examples are Microsoft Azure App Service, Google App Engine, and Heroku
    - AWS Elastic Beanstalk is an abstraction layer on top of EC2
        - You tell it the the type of application you're running and it puts EC2 instances in autoscaling group behind Elastic load balancer
        - Applications run in a secure environment and retain full control over underlying AWS resources
    - GAE - Google App Engine, PaaS offering by Google
- PaaS has some vendor lock in
    - May limit you to proprietary interfaces and languages
    - Difficult to switch to another host

## MBAAS

- Mobile backend as a service
- For almost every app you’ll need networking, load balancing, databases, social network integrations, notifications, etc
- Many commonalities
    - Many use MongoDB, REST API, microservices, front-end design framework

## SaaS

- Software as a service
- Software distribution: retail —> downloads over the internet —> broadband and browser distribution
- Examples: Gmail, Jira, Google Docs, Docusign, Salesforce, TurboTax, Coursera
- Multi-tenant architecture - same software for all customers but data is specific for individual user
- Client-side software runs in users’ browser while server side runs in the cloud with APIs connecting the two often via REST calls
- Advantages
    - Flexible and scalable payments
    - Automatic updates
    - Access anywhere
- Disadvantages
    - Lose control
    - No access to source code
    - Provider service disruptions impact you

## Comparison of Tiers

- Building on a PaaS may offer faster building and makes your life easier but IaaS will make it easier to switch later because you have more control

![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%207.png)

![Untitled](Week%201%20Cloud%20Computing%20Foundations%207cf0e13f862944378706c32492897d65/Untitled%208.png)

# Quiz

- Most economical
    - “A long-running business serves 10,000 users during the day and 100 during the night.”
        - In-house servers
            - Since all the days needs high bandwidth, the in house servers will be more economical
    - “A long-running business serves 1,000 daily but 1,000,000 during the holiday session.”
        - Hybrid
    - “A long-running business needs 10,000 computers for one-time data processing.”
        - Cloud
- Big data
    - Examples
        - Genomic records for a whole country
        - Astronomy telescope observations
    - Properties
        - Volume, Velocity, Variety, Veracity
- In cloudonomics, the coefficient of variation (*Cv*) is a measure of smoothness of (aggregate) demand(s). What is the impact of increasing the load from 1 workload to *n*  on *Cv* under perfectly positively correlated demands?
    - *Cv* remains constant
        - When the load is increased from 1 to n for perfectly positively correlated demands: Mean: n.μ(X), standard deviation: n.𝜎(X), Aggregate Cv = Cv (X) =𝜎𝜎(X)/μ(X)
- What is the best model of delivery for the following scenario?
    - “An Electronic Health Record system for clinics and doctors”
        - SaaS
    - “A web hosting solution for PHP web applications”
        - PaaS
    - “A lightning-fast storage solution for gigantic amounts of data, using a proprietary network routing algorithm.”
        - IaaS
    - “ACME company needs to provide a widely used application to all its marketing team.”
        - SaaS
    - “ACME company needs to deploy a system with an in-house modified Operating System, with a custom kernel optimized for heightened security.”
        - IaaS