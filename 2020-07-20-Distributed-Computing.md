# Distributed Systems

- Fundamentals
    - Definition
        - Loosely coupled vs Tightly coupled systems
            - Tightly : Single system wide primary memory. Physical communication done through shared memory. Usually referred to as **parallel processing systems**.
            - Loosely : Each system has its own primary memory. Physical communication done through passing messages across network. **Distributed computing systems**.
    - Advantages of Distributed Systems
    - Network OS vs Distributed OS
    - Models of Distributed OS
        - Minicomputer model
        - Workstation model
        - Workstation-server model
        - Processor pool model
        - Hybrid model
    - Issues with Distributed Systems
        - Transparency
            - Access Transparency
            - Location Transparency
            - Replication Transparency
            - Failure Transparency
            - Migration Transparency
            - Concurrency Transparency
            - Performance Transparency
            - Scalability Transparency
        - Reliability
        - Flexibility
        - Scalability
        - Performance
        - Heterogeneity
        - Security
    - Inter-process communication
        - Shared data
        - Message passing
    - Other topics
        - Monolithic vs Microlithic kernel
        - Stateful vs Stateless server
- Message Passing
    - Introduction
    - Desirable features of a good message-passing system
        - Simplicity
        - Uniform semantics : The semantics should be as uniform as possible in terms of local and remote communication.
        - Efficiency : If the system is not efficient, then application designers will try to avoid using it. An IPC protocol of message passing can be made efficient by reducing the number of exchanged messages. Some common optimisations made in this sense:
            - Avoiding the cost of establishing and terminating connections between a pair of processes for each exchange of messages.
            - Piggybacking acknowledgement of previous messages with the next message.
            - Minimising the cost of maintaining the connection between the two processes.
        - Reliability :
            - Running in the face of failure that might be caused due to node failure, or communication link breakdown. Guaranteed delivery of messages. Handled using acknowledgments and retransmissions.
            - Avoiding duplicate messages. Done using sequence numbers for messages.
        - Correctness : feature related to group communication under IPC.
            - Atomicity : Message delivered to all nodes or none
            - Ordered delivery : Messages arrive at receiver end in correct order
            - Survivability : The messages to be delivered to different nodes should reach even in the face of possible failures.
        - Flexibility : IPC protocols for a message passing system must be flexible enough to cater to the various needs of different applications, i.e. the IPC primitives should be such that the users have the flexibility to choose and specify the types and levels of reliability and correctness requirements of their applications.
        - Security : A good message passing system provides secure end-to-end communication. Needed steps :
            - Authentication of the sender of a message by the receiver.
            - Authentication of the receiver of a message by the sender.
            - Encryption of a message before sending it over the network.
        - Portability :
            - The message passing system should be portable
            - The systems build using the message passing system should be portable. The design of high level primitives involved in the message passing system should take the heterogeneity of the system in consideration.
    - Message structure
    - Synchronisation
    - Buffering
    - Encoding and Decoding of Message Data
    - Process Addressing
    - Group Communication
- Remote Procedure Calls
    - Introduction*
    - The RPC model*
    - Transparency of RPC*
        - Local procedures and remote procedures are indistinguishable. These needs two types of transparencies :
            - Syntactic transparency (Not very difficult to achieve) : Remote procedure call should have the same syntax as that of the local procedure call.
            - Semantic transparency (Almost impossible to achieve) : Semantics of a remote procedure call should be the same as that local procedure call.
    - Implementing RPC mechanism*
    - Stub generation*
    - RPC messages*
    - Parameter passing semantics*
    - Call semantics*
    - Communication protocols for RPCs*
    - Client-server binding*
    - Server management
- Synchronisation
    - Clock synchronisation*
    - Event ordering*
        - Happened before relation for partial ordering
            - Concurrent processes don't have a sense of happened before relation, hence this way of ordering of events is partial ordering. Since all global events are not ordered. Ordering happens with respect to only related processes.
        - Logical clocks
        - Event ordering using Lamport's algorithm

            Each process has its own clock. 

            Lamport's algorithm conditions : 

            1. Clock should always move forwards for all involved clocks. 
            2. If the time on the clock of two interacting processes, i.e. time on one process (the sender) is different from another process (the receiver), then to handle that the sender sends the message with the timestamp on its clock, and checks if the time on the message is greater than that on the receiver process's clock, then the update should be the message's time + 1, else we can just increment for the current clock's time.
            3. An event occurring should lead to increment in clock value. 
            - Using counters
            - Using physical clocks
        - Total event ordering
            - Modification of the above defined Lamport's algorithm. There should be a way to order the same time on different processes. One can be assigning process id's to process, and accordingly ordering them based on relative time, and process ids. This gives a unique timestamp for all processes in the system.
    - Mutual Exclusion*
        - Centralised approach
            - A node is chosen to decide which processes request to enter the critical section can be granted on the basis of some scheduling algorithm on the basis of request message received. They maintain the order in the queue, and use the request, allocate, and release message scheme for resource allocation.
            - Single point of failure.
        - Distributed approach
            - Total ordering of the events is required here. Lamport's method of total ordering can be used here.
            - Message to all nodes for approval. Can't enter own critical section till approvals come from all nodes. The messages don't reply and wait if they are themselves executing the critical section or are have lower timestamp for execution of critical section than the message they received the request from.
        - Quorum-based approach : Maekawa's algorithm
        - Token-passing approach
            - Token is passed between nodes, which operate in a ring structure. If the node wants to enter the critical section, it keeps the token, and when the need is finished, it passes it on to the next node.
    - Deadlock*
        - Introduction
        - Necessary conditions for deadlock
        - Deadlock modelling
        - Constructing resource allocation graph
            - Circle for involved processes. Rectangle for involved resources, with dots indicating the units of resources available in the system.
            - Edge from resource dot to process, if allocated to that resource. Edge from process to resource rectangle, if resource is requested.
            - If each resource in the resource allocation graph has one unit, then a cycle is necessary and sufficient condition for deadlock, else, we need a knot for a deadlock to occur.
        - Wait-for-graph
            - Constructed using the resource allocation graph by dropping the resource nodes and the edges that they are involved, and including edges between the owner and requesting processes.
        - Strategies for handling deadlocks

            Handling deadlocks in distributed systems is much more complicated as compared to centralised systems. 

            - Types of deadlocks in distributed systems
                - Resource Deadlock
                - Communication Deadlock : Process is waiting for a message from another process, and cannot move forward without it. Same as single resource instance deadlock.
                    - Can be modelled using WFG as well
            - Deadlock avoidance

                Resources are not immediately allocated, rather an analysis is done, whether there is a way for allocation can be done to maintain the safe state (assumption is made that the resource is allocated) the resource is allocated, else the request is deferred. 

                - Safe and unsafe states
                    - Safe states are states from which we can guarantee that all processes can reach their completion, i.e. there is a safe sequence available.
                - Safe and unsafe sequences
                    - Safe sequence is a sequence of state transitions for resource allocation, that leads to proper completion of all processes.
                - Unsafe states are not necessary deadlock states, but might lead to deadlocks.
            - Deadlock prevention

                designing the system in such a way that one of the 4 conditions necessary for deadlock do not satisfy. The four conditions : 

                1. Mutual Exclusion 
                2. No preemption (Preemption)
                3. Hold and wait (Collective Requests)
                4. Circular wait (Ordered Requests)

                mutual exclusion is not used for deadlock prevention because managing this condition leads to other problems, and most resources can't handle mutual exclusion intrinsically. This condition is necessary for correct functioning of the user processes.

                - Collective Requests : The resource requesting a resource should not hold any resource at the time of request. Resource allocation policies are as follows :
                    - a) Request before execution : Request for all resources before execution
                    - b) Request during execution : Needs to release resources in order to acquire more resources. The request should be made for new resources plus the released resources.

                    a vs b : Most processes don't know the required resources at the time of execution. Also, in many cases, some resources are required only at the end. This would decrease resource utilisation, since their idle time will increase. \

                    Problems :  

                    - Low resource utilisation
                    - Accounting issues
                    - Starvation : If a process needs many resources, it is possible that some or the other resource is always not available, hence the process always keeps waiting.
                - Ordered Requests : Each resource type is assigned a number, based on usage pattern (The resource at a higher number will only be required if the one lower than that is done).
                    - The allocation policy works like : The process can't request for a resource type that has a number lower than the one with the maximum number that is currently holding. To access the requested resource, it needs to relieve all resources with numbers higher than it. To request multiple units of the same request, it can be done via single request. Proven to not have cycles.
                    - Jobs aligned to the ordering, show higher efficiency.
                    - Reordering is not an easy job, since its coded into the system, and would require reprogramming, compilation and build.
                    - One of the most efficient methods to handle deadlocks
                - Preemption :
                    - Preemptable resource :  Resource whose state can be saved and recovered later.
                    - Allocation policies
                        - If a resource requested by a process is not available, all its resources are preempted, and it is blocked. Unblocked when the requested and preempted resources become available.
                        - If a resource requested not available with system, then check is made with a blocked or waiting resource. If available, the resource is taken from the process and granted to the requesting process. Else it is blocked, and it also becomes a part of the process pool, whose resources are available to be picked. The process is unblocked, when all resources are available for use.
                        - Limited applicability : Only some resources can be preempted.
                    - Availability of global timestamps and atomic transactions makes this approach attractive in distributed database systems.
                        - A mechanism is used to assign global timestamps to transactions (processes), like Lamport's algorithm.
                        - Prevention schemes : Differ in handling of younger process requesting resources.
                            - Wait - die :
                                - Younger process requests from older → dies
                                - Older process requests from younger → waits
                                - Younger process is restarted immediately, and killed again if the older process is still there. Can be restarted once the resource it needs is available.
                            - Wait - wound :
                                - Younger process requests from older → waits
                                - Older process requests from younger → younger dies
                                - Younger process started after a predetermined time.
            - Deadlock detection and recovery
                - Detection approaches
                    - Centralised approach
                    - Hierarchical approach
                    - Fully distributed approach
                        - WFG-based distributed algorithm
                        - Probe-based distributed algorithm
                - Recovery approaches
                    - Asking for operator intervention
                    - Termination of process
                    - Rollback of process
                - Issues in recovery
    - Election Algorithms*
        - Bully algorithm
        - Ring algorithm
        - Bully algorithm vs Ring algorithm
- Resource Management
    - Resource manager
    - Desirable features of a good scheduling algorithm*
    - Task assignment approach*
    - Load balancing approach*
    - Load balancing algorithms
        - Static vs Dynamic
        - Deterministic vs Probabilistic
        - Centralised vs Distributed
        - Cooperative vs Non-cooperative
    - Issues in designing load balancing algorithms
        - Load estimation policies
        - Process transfer policies
        - Location policies
        - State information exchange policies
        - Priority assignment policies
        - Migration limiting policies
    - Load sharing approach*
    - Issues in designing load sharing algorithms
        - Load estimation policies
        - Process transfer policies
        - Location policies
        - State information exchange policies
- Process Management
    - Process Management*
    - Process Migration*
    - Desirable features of a good Process Migration Mechanism
    - Process Migration Mechanisms
        - Freezing the process
            - Immediate and delayed blocking of the process
            - Fast and slow I/O operations
            - Information about open files
            - Reinstating the process on its destination node
        - Address space transfer mechanism
            - Total freezing
            - Pre-transferring
            - Transfer on reference
        - Message forwarding mechanism
            - Mechanism of resending the message
            - Origin site mechanism
            - Link traversal mechanism
            - Link update mechanism
        - Mechanisms for handling co-processes
            - Disallowing separation of co-processes
            - Home node or origin site concept
    - Process Migration in Heterogeneous Systems
        - Handling the exponent
        - Handling the mantissa
        - Handling signed-infinity and signed-zero representations
    - Advantages of Process Migration
        - Reducing average response time of processes
        - Speeding up individual jobs
        - Gaining higher throughput
        - Utilising resources effectively
        - Reducing network traffic
        - Improving system reliability
        - Improving system security