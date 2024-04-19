# Week 15: Architecting Cloud Applications

## Kubernetes Container Orchestration

### Intro

- Kubernetes is not a platform as a service
    - It doesn’t ditch many important aspects and all that is left to you
    - Many other systems such as Deis, OpenShift, and Eldario are built on top
    - Less opinionated than Docker Swarm
- Platform to orchestrate the deployment, scaling, and management of container-based applications
    - Primary responsibility of Kubernetes is container orchestration
    - Containers are scheduled to run on physical or virtual machines
    - Can replace dead, unresponsive, or unhealthy containers
- minikube is local Kubernetes focusing on making it easy to learn and develop for Kubernetes
- Docker Desktop comes with a pre-installed Kubernetes installation
- Cloud Kubernetes Offerings
    - GCP Google Kubernetes Engine (GKE), AWS Elastic Kubernetes Engine (EKS), Azure Kubernetes Service (AKS)

### Architecture

- Master node
    - API server, controller, scheduler, etcd
    - Kubernetes has a “hub-and-spoke API pattern”
    - Control plane can horizontally scale
    - Responsible for global state of the cluster
- Worker node
    - kubelete, Kube-proxy, Container Runtime
- Node runs pods
- etcd
    - A highly available consistent key-value store
    - Used to store the state of the system
- kublet
    - An agent runs on each node within in the cluster
    - Manages the pods
- kube-proxy
    - Manages routing of requests and traffic for both node and pods
- Container-runtime
    - Any OCI (open container initiative) compliant runtime (ex Docker)
- Namespace
    - Supports multiple virtual clusters backed by the same physical cluster
    - Names of resources need to be unique within a namespace
- Resource quota
    - Defined by a resource quota object provides constraints that limit aggregate resource consumption per namespace

### Pods

- A grouping of one or more containers that share some namespaces
    - Eg containers in a pod share networking
    - Containers in a pod can communicate with each other through `localhost`
- Pod abstraction allows for innovative design patterns still most of the time we see single container pods
- Pod architectures
    - Sidecar - made up of two containers
        - Application container
        - Sidecar container (augments and improves the application container)
        - Example use case: adding HTTPS to a legacy service
    - Ambassador
        - Brokers interactions between application and the rest of the world
        - Example use case: shard a service, service discover
            
            ![Screenshot 2023-05-09 at 9.11.17 PM.png](Week%2015%20Architecting%20Cloud%20Applications%20afd018bdccf74e41aa60f5567574a38a/Screenshot_2023-05-09_at_9.11.17_PM.png)
            

### Higher Level Resource Abstractions

- Labels - key/value pairs attached to objects such as pods
    - Labels can be used to organize and elect subsets of objects
    - Label selectors are used to select objects based on their labels
- ReplicaSet - maintain a stable set of replica Pods running at any given time
- Deployment - manages ReplicaSets and provides declarative updates to Pods
    - Manages rollout for a ReplicaSet
        
        ![Untitled](Week%2015%20Architecting%20Cloud%20Applications%20afd018bdccf74e41aa60f5567574a38a/Untitled.png)
        
- StatefulSet - manages deployment and scaling of a set of Pods and provides guarantees about the ordering and uniqueness of Pods
    - Unlike Deployment a StatefulSet maintains sticky identity for pods
- Job - creates one or more Pods that will continue to retry execution of Pods until specified number successfully terminate
    - When a specified number of successful completions is reached the job is finished
    - Example - One Job object in order to reliably run one Pod to completion

### Services

- Everything before this section is about launching and maintaining a cluster, services are about communication between
- A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them
    - Only manages the communication between them
    - Controls a group of pods (determined by label selector)
    - Pattern is sometimes called a mircoservice
    - When created a service has a unique IP address (clusterIP)
        - Communication to service is automatically load-balanced to member pod of the service
- Pods run in a flat cluster wide address space, when a node dies the pod dies with it
    - Deployment will restart the Pod but it will have a different IP address making communication hard

### Networking Model

- Every node in a Kubernetes cluster runs a `Kube-proxy`
    - `kub-proxy` watches the control plane for the addition of Service and Endpoint objects (pods)
    - Responsible for implementing a form of virtual IP for services
- User space proxy mode
    
    ![Untitled](Week%2015%20Architecting%20Cloud%20Applications%20afd018bdccf74e41aa60f5567574a38a/Untitled%201.png)
    
- Iptables proxy mode
    
    ![Untitled](Week%2015%20Architecting%20Cloud%20Applications%20afd018bdccf74e41aa60f5567574a38a/Untitled%202.png)
    
- IPVS
    
    ![Untitled](Week%2015%20Architecting%20Cloud%20Applications%20afd018bdccf74e41aa60f5567574a38a/Untitled%203.png)
    

### Service Discovery and Ingress

- Primary modes of discovering services
    - Environment variables - kubelet adds environment variables for each active service
    - DNS - cluster aware DNS server watches Kubernetes API for new services and creates DNS records for each one
- Publishing services
    - ClusterIP - makes service available only within the cluster
    - NodePort - exposes service on each node IPs as a port
    - LoadBalancer - exposes service using cloud providers load balance
    - ExternalName - maps contexts of service to externalName field by returning CNAME
- Ingress
    - API manages external access to services in cluster, typically HTTP
        
        ![Untitled](Week%2015%20Architecting%20Cloud%20Applications%20afd018bdccf74e41aa60f5567574a38a/Untitled%204.png)
        

### Final Thoughts

- Docker Swarm vs Kubernetes
    - Task vs pod
        - A task manages a single container while a pod can manage many containers sharing a network
    - Service vs ReplicaSet
        - Defines desired state of an application service that has multiple instances
    - Service vs Deployment
        - A deployment is a ReplicaSet augmented with rolling updates and rollback capabilities
    - Routing Mesh vs Service
        - Routing mesh is L4 routing and load balancing while service is logical set of pods with stable endpoint to access them
    - Network vs Network policy
        - Swarm uses SDNs to firewall containers
        - Kubernetes has flat network architecture
    
    ![Untitled](Week%2015%20Architecting%20Cloud%20Applications%20afd018bdccf74e41aa60f5567574a38a/Untitled%205.png)
    
- Helm
    - Helm is package manager for Kubernetes
    - Helm charts are Kubernetes YAML manifests combined into single package
    - Helm deploys charts which you can think of as a packaged application (similar to yum or apt)
    - Collection of versioned, application resources which can be deployed as one unit

## Quiz

- Which of the following is not a function of Kubernetes?
    - **Create container image based on user specified requirements.**
        - Kubernetes is a platform to orchestrate the deployment, scaling, and management of container-based applications. It does not create container image based on user specified requirements.
- What is the smallest control unit in Kubernetes?
    - **Pod**
        - In Kubernetes the smallest control unit is a Pod
- How many master node does Kubernetes has?
    - **User define**
        - The number of master nodes in Kubernetes is not certain. Users can define the number of master nodes according to their needs.
- A Pod is a Kubernetes abstraction that represents a group of
    - **one or more application containers**
        - A Pod is a grouping of one or more containers that share some namespaces.
- Which of the following is not a component of the master node?
    - **Kube-proxy**
        - A mster node contains API server, controller, scheduler, and etcd. Kube-proxy is part of the worker node.
- Kubernetes can only support Docker container runtime.
    - **False**
        - Kubernetes is [deprecating Docker](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.20.md#deprecation) as a container runtime after v1.20.
- Sidecar model requires two nodes to work.
    - **False**
        - Sidecar is a kind of single node pattern.
- Which component of Kubernetes cluster node is responsible for implementing a form of virtual IP for Services?
    - **kube-proxy**
        - Kube-proxy is responsible for implementing a form of virtual IP for Services.
- Which component of Kubernetes cluster node is responsible for responsible for managing the pods?
    - **kublet**
        - Kubelet is an agent that runs on each node within the cluster. It is responsible for managing the pods.
- Which component of Kubernetes master node is responsible for storing the state of the cluster?
    - **etcd**
        - etcd is a highly available consistent key-value store and it is used to store the state of the cluster.