# Week 13: Virtualization and Containerization

## Introduction

- You could rent hardware if you really wanted to, but standing up computers is hard work
- What is virtualization?
    - [https://opensource.com/resources/virtualization](https://opensource.com/resources/virtualization)
    - Process of running a virtual instance of a computer system in a layer of abstraction from hardware
    - Container —> isolated process
    - Virtualization —> simulate a whole OS, all the libraries, etc

## Virtualization

### Intro

- Economics of clouds require sharing resources
- How do we share physical computers? —> Abstraction
- Abstract computer, abstract network, abstract network
    - Cloud resources then run on top of all that abstraction
- Virtualization allows distributed computing without dependencies on physical resources

### Types of Virtualization

- Emulation
    - Program that emulates the function of a CPU
    - Do in hardware what a certain CPU would do with software
- Full
    - Software
        - Binary translation
        - Paravirtualization
    - Hardware Assisted
- MicroVMs
- OS level

### System Background

- Very early computers were single program computers (one computer just ran one task)
    - No idea of a process and the OS is just a thin wrapper around the BIOS
- Multi-user / multi-tasking required need to isolate programs and users
    - Brought the notion of a process
- World-view from a process
    - Image of program’s executable machine code
    - Memory is assigned and it is virtual memory (think 241 and paging)
    - Stack (temp data) and Heap (used to hold intermediate data) is unique to the process and
    - Ideally a process should be totally isolated from other processes
- Duel mode operations
    - OS has two modes: user mode, kernel mode
        - User mode
            - User process operate in user mode
        - Kernel mode
            - When the system boots, hardware starts in kernel mode and has more privileges
- CPU privilege protection
    - When instruction is executed the CPU checks if process is allowed or not
    - x86 has ring levels and every process has a ring level
        - GPF (general protection fault) when wrong level permission is applied

### Full Virtualization

- Virtual machine simulates enough hardware to allow unmodified “guest” OS (one designed for same CPU type) to run in isolation
- Virtual machine looks and feels exactly like a real computer

![Untitled](Week%2013%20Virtualization%20and%20Containerization%20201b85115e0344e9a141e105f69d6619/Untitled.png)

- Privilege types
    - Privileged instructions - a subset of unsafe
    - Privileged instructions should cause a trap
    - Original x86 were unsafe because there were 17 unsafe instructions
- Trap and emulate
    - Executable code from guest can execute directly on host CPPU by the hypervisor
        - Hypervisor configures CPU to “trap” all potentially unsafe instructions
        - A trap is like an interrupt and transfers control back to the hypervisor
        - The hypervisor will receive the trap and emulate the instruction in some safe way
    - Approach has good performance because majority of instructions will not cause a trap and will execute straight on CPU with no overhead

### Paravirtualization

- x86 processors were not virtualization until mid2000
    - Software-only virtualization is a technique to go around trap and emulate design
- Virtual machine does not simulate hardware but offers a special API that can only be used by modifying guest OS
    - Guest OS must be specifically modified to run on hypervisor
- Xen
    - Paravirtualization eliminates traps
    - Invasive changes to kernel to run Linux as paravirtualized guest

### Binary Translations

- Binary translation modifies sensitive instructions on the fly to virtualizable instructions
- Direct election on the CPU
- Performed on the binary code that is executed on the processor (no changes to guest operating kernel)

### 1st Generation Hardware

- Intel VT (IVT), AMD Virtualization (AMD-V)
- New less privileged execution mode called guest mode supporting direct execution of guest code
- New instruction `vmrun` transfers from host to guest mode
- Lacks explicit support for memory virtualization

### 2nd and 3rd Gen Hardware

- AMD RVI and Intel EPT
- VMM maintains a hardware-walked nested page table
- Most hypervisors emulate I/O devices
- 3rd gen allows for launching VMs within VMs

### MicroVMs and Unikernels

- MicroVM
    - Typical VMs has many virtual I/O devices to make it usable
        - Guest operating system supports device drivers, kernel modules, etc for all
    - FireCracker
        - Based on top of Linux KVM
        - Idea is to be as light weight as possible
        - Only virtual devices: one-button keyboard, interrupt controller, timer,  clock, virtualized block, virtualized network
        - VMM (virtual machine monitor) starts in 8ms and whole thing launches in 125ms
- Unikernel
    - Software is directly integrated with kernel it is running on
    - Compiled source code along with required system calls and drives are made into one executable program
    - Can only run a single process thus forking does not exist

## Containers

### Intro

- Hypervisors have remedied certain deficiencies in OS design but containers are more lightweight that a hypervisor
- In containers processes think they see a virtual kernel but in reality they are all sharing the same kernel
    - Kernel acts almost like a hypervisor to ensure container boundaries are not crossed

### Pillars of Linux Containers

- **NOT** chroot
    - Root directory (/) is top directory and all file system entries branch out from this root
- cgroups
    - Control how many resources each container can utilize
- Namespaces
    - Provide isolation
- Unionfs
    - Layer after layer of file systems

### Control Groups (cgroups)

- Limits, isolates, and measures reousrce usage of group of processes
- Allows for cloud providers to guarantee you a certain amount of resources
- Scheduling cgroups in completely fair scheduler requires thinking in terms of time slices

### Namespaces

- Namespace wraps a global system resource in abstraction so it appears to processes that they have isolated instance of the global resources
    - Linux has has hierarchy of processes and Linux namespaces all for hierarchies of processes with their own “subtrees”
        
        ![Untitled](Week%2013%20Virtualization%20and%20Containerization%20201b85115e0344e9a141e105f69d6619/Untitled%201.png)
        
        ![Untitled](Week%2013%20Virtualization%20and%20Containerization%20201b85115e0344e9a141e105f69d6619/Untitled%202.png)
        

### Union FileSystem (unionfs)

- Backbone of container images, keeps physical contents separate but appears to merge directories
- To access a file the runtime first tries on the top branch than tunnels lower if it isn’t found
- If user tries to modify a file on read-only layer it is **copied on write** to a read/write layer
- Programs inside don’t care which layer the files and directories come from
- **Docker images**
    - Container image is made of a stack of immutable or read only layers
        - Therefore we can keep launching containers off one image
            
            ![Untitled](Week%2013%20Virtualization%20and%20Containerization%20201b85115e0344e9a141e105f69d6619/Untitled%203.png)
            
- Graph driver - local instance of Docker engine that has cache of Docker image layer

### Docker Architecture

- Container runtime
    - Originally monolithic but later separated
    - Creates a container from that image and initializes and runs the container
    - `containerd` is based on `runc` and provides higher level functionality
        - Image push/pull, manages storage
    - `runc` is low level functionality of container runtime
        - Runs linux level features
- Docker engine provides functionality on top of container runtime
    
    ![Screenshot 2023-05-10 at 7.54.53 PM.png](Week%2013%20Virtualization%20and%20Containerization%20201b85115e0344e9a141e105f69d6619/Screenshot_2023-05-10_at_7.54.53_PM.png)
    
- Windows/Mac can have linux containers because Docker can launch VM (hyper kit) and then those containers run in the VM

### Container Networking

- Libnetwork implements Container network model
- Endpoint joins a sandbox to a network
- Network is a group of endpoints
- When you start a Docker a default bridge network is created automatically (legacy)
- Better approach is user defined networks (DNS resolution
    
    ![Untitled](Week%2013%20Virtualization%20and%20Containerization%20201b85115e0344e9a141e105f69d6619/Untitled%204.png)
    

## Quiz

- Which type of virtualization is feasible for the following scenario?
    - “A service needs to run an unmodified OS on a basic processor, separate from the host operating sysetm.”
        - **Full virtualization**
            - Unmodified OS, not on the host OS make the other two not  suitable.
    - “A service needs to run an unknown and unmodified OS on an advanced processor.”
        - **Hardware-assisted**
- Which type of virtualization provides better performance for the following scenario?
    - “Running multiple independent applications sharing the same kernel”
        - **Containers**
    - “Running two independent applications, each needs a different version of a kernel module”.
        - **Full virtualization**
- Who is responsible for scheduling and memory management when using containers?
    - **Host OS (Base OS) kernel**
- Docker is used to:
    - **Guarantee that the software will always run the same irrespective of environment**
        - Using the Dockerfile format, and relying on Union filesystem technology, docker images downloaded from a hub guarantee specfic software environments for deployment.
- Kubernetes provides a platform for automating deployment, scaling, and operations of application containers across clusters of hosts.
    - **True**
- A user application is not allowed to load control registers when running in kernel mode.
    - **False**
- In x86, kernel mode code runs in ring 0 while user processes run in ring 3.
    - **True**
- When a user application needs to handle an interrupt, it has to enter kernel mode.
    - **True**
- Xen does not require special hardware support, such as Intel "VT-x" or "AMD-V".
    - **True**
        - Paravirtualization is a software-only virtualization approach.
- Binary translation modifies all instructions on the fly and does not require changes to the guest operating system kernel.
    - **False**
        - Binary translation only modifies sensitive instructions.
- In unikernel, user application can transit to kernel mode using special instructions.
    - **False**
        - There is only one address space in unikernel. Applicaiton can be seen as running in kernel mode the whole time.
- Is it possible to install a second application with different dependencies into an existing unikernel?
    - **False**
        - Making changes to unikernel requires recompilation. Unikernel normally only runs one application.
- Which is not the reason that microVM is faster than a normal VM
    - **Having a minimal security protection.**
- AWS Lambda and AWS Fargate are using
    - **microVM**
- Which generation of hardware virtualization introduced IOMMU virtualization?
    - **Third**