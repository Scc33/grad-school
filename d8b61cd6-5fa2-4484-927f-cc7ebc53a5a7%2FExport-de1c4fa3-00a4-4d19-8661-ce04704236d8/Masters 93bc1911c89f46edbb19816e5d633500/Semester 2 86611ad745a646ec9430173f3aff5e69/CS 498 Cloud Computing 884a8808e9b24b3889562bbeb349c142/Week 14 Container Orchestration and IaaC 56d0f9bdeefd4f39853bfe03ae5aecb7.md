# Week 14: Container Orchestration and IaaC

## Container Orchestration in Docker, Docker Swarm, ECS, and ACI

### Docker Foundations

- Dockerfile
    - Imperative method to create an image
        - Imperative - commands one after the other telling the system what to do
    - Describes to the docker engine what layers to use
- Container
    - Set of processes within a namespace
- Docker container run -d (daemon mode)
- Kernel is shared between Docker instances
- Multistage Dockerfile
    - Multi stage allows us to not include unnecessary immediate layers
    - This saves a ton of storage
    - FROM …. AS
    - Then you can just copy what is built into the final docker image

### Docker Swarm Orchestration

- Container orchestration
    - Many applications consist of multiple components that need to be distributed across machines
    - User containers we can have each component running in its own container
    - Pre-built components for common uses can be made available on public registries
    - ‘Container as a service’
    - In swarm a service is an extension version of containers
    
    ![Untitled](Week%2014%20Container%20Orchestration%20and%20IaaC%2056d0f9bdeefd4f39853bfe03ae5aecb7/Untitled.png)
    
- Swarm services use a declarative model
    - You define the desired state and rely on docker to maintain that
- Nodes on Swarm
    
    ![Untitled](Week%2014%20Container%20Orchestration%20and%20IaaC%2056d0f9bdeefd4f39853bfe03ae5aecb7/Untitled%201.png)
    
- Services on Docker Swarm
    
    ![Untitled](Week%2014%20Container%20Orchestration%20and%20IaaC%2056d0f9bdeefd4f39853bfe03ae5aecb7/Untitled%202.png)
    

### Docker Networks, Bridge, Overlay

- Docker bridge networking
    - `docker network create my-net` and `docker create --name my-nginx --network my-next --publish 8080:80 nginx:latest` connects Nginx container to the my-net network
    - Any container connected to the my-net network has access to all ports on my-nginx container and vice versa
    - Also publishes port 80 in the container to port 8080 on the docker host
- Docker overlay network
    - Creates a distributed network among multiple Docker daemon hosts
    - Sits on top of the host-specific netowkrs
    - Transparently handles routing of each package
    - `ingress` - handles control and data traffic related to swarm services

### Internal Load Balancing

- User-defined networks provide DNS system
    - For most situations you should connect to service name which is load balanced between containers
        - http://my-service:8080
            
            ![Untitled](Week%2014%20Container%20Orchestration%20and%20IaaC%2056d0f9bdeefd4f39853bfe03ae5aecb7/Untitled%203.png)
            

### Routing Mesh and External Load Balancing

- Bridge networks on one host - containers connect to same bridge network expose all ports to each other
- On multi-host - Docker Swarm to publish ports
    - Swarm services publish ports using the routing mesh
    - Effectively Docker acts as a load balance for swarm services
- Ingress network plays important role in enabling publish ports over the swarm

### Volumes

- Docker containers are based on Unionfs
- When container is removed the top layer is also removed
- To persist changes outside a container we need to mount an external storage location
- Three types of host to container mapping
    - Bind mount - file or directory on host machine is mounted on container and directly reference absolute path
    - Volume - persistent storage abstraction
    - tmpfs - you don’t want data to persist either on host or container (good for security reasons)

### Secrets and Configs

- Secret is a blob of data
- Should not be unencrypted in Dockerfile or application source code
- Docker *secrets* centrally manages and only available to Swarm service and not available to standalone container

### Compose and Stacks

- Imperative - tell the system how to do things
- Declarative - tell the system what you want achieved
- Docker compose
    - Tell docker compose what you want and it creates it for you
- Docker compose and docker swarm both use compose specification

### Example 3-tier architecture in Swarm

- Frontend, application, backend

![Untitled](Week%2014%20Container%20Orchestration%20and%20IaaC%2056d0f9bdeefd4f39853bfe03ae5aecb7/Untitled%204.png)

### Compose stacks on AWS ECS and Azure ACI

- ECS is fully managed container orchestration
- Containers run on either customer managed EC2 instance or AWS margate

---

## Quiz

- The latest CentOS comes with Linux kernel version 4.18. If you are running a latest CentOS container on a Ubuntu with kernel version 5.4, which kernel version would you see inside the container?
    - **5.4**
- Which is the default Docker network driver?
    - **bridge**
- Containers on different networks can communicate using the bridge network.
    - **False**
- For communication among containers running on different Docker daemon hosts, you should use
    - **overlay network**
- For containers running on different host to communicate, you should use
    - **overlay network**
- For a container to communicate with another container running on the default bridge network, one can use either the target container's ip address or its container name directly.
    - **False**
- Docker Swarm routing mesh will report an error if an external load balancer reaches a node that does not have a task belonging to the requested service.
    - **False**
- When you publish a service port, the swarm makes the service accessible at the target port only on nodes that have a task running for that service.
    - **False**
- You are working on a course MP and want to use the IDE on host to edit codes and run the codes inside a container. Which is the best way to make the codes accessible inside the container?
    - **Bind mount**
- AWS ECS has two launch tyeps: EC2 and Fargate. EC2 will automatically manages all resource provisioning while for Fargate it's managed by customer.
    - **False**