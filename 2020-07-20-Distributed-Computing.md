# Distributed Systems

- Fundamentals
    - Definition
        - Loosely coupled vs Tightly coupled systems
            - Tightly : share clock, memory and bus.
            - Loosely : donot share clock, memory and bus. connected to each other using high speed network. Computation and processing distributed through systems.
    - Advantages of Distributed Systems
        - Resource sharing
        - Computation speedup
            - The process can be broken into different parts and computed on different systems, and then compiled. Parallel processing would allow for a computation speedup.
            - Load sharing / Load balancing
        - Reliability
        - Communication
    - Network OS vs Distributed OS
        - Network OS
            - Each system has own OS. User has information about other systems, and has to manually perform operation by logging in remotely. Example telnet, ftp
        - Distributed OS
            - Abstraction layer, that allows for performing operations even without information about the underlying systems, and their structure. Entire distributed system is viewed as a single entity.
    - Types of migration :
        - Data Migration :
            - Andrew file system : whole file
            - Sunmicrosystem network file system : part of the file needed, better for bigger files.
            - Data translation (converting data from one format to another, appropriate for functioning dependent on the system being migrated to) is the responsibility of the distributed OS.
        - Computation Migration :
            - Process initiated on one system, and part of computation performed on another system. For example a heavy procedure called on a machine with better GPU configuration. Done using RPC.
        - Process Migration :
            - Process itself is migrated. Used to achieve load balancing.
    - Models of Distributed OS
        - Minicomputer model
            - Interconnected mini-computers. Each mini-computer can have multiple terminals.
        - Workstation model
            - Minicomputers upgraded to workstations (high-end machines). These workstations are diskfull.
        - Workstation-server model
        - Processor pool model
        - Hybrid model
    - **Issues with Distributed Systems**
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
        - Data is sent in the form of message. Needs to be efficient for good overall performance.
    - Desirable features of a good message-passing system
        - Simplicity : Easy to use for developer. Easy to integrate into new apps, and be able to interact with existing ones.
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
        - Address : Identify both receiver and sender
        - Sequence Number : Message identifier
        - Structural information : Types, and actual data/pointer.
    - Synchronisation
        - Types of message semantics for primitives (send, receive)
            - Blocking : Sender is in block state till it receives ack.
            - Non-blocking : Asynchronous process.
        - Receiver blocking
            - The receiver is blocked till the message is completely received after receive primitive is added.
        - If both client and server follow block mode of message passing, then the communication is called synchronous, else called asynchronous.
        - Use of timeouts is important in blocking messages, else failure of other machine would lead to the other machine staying in blocked state.
        - Polling and interrupts (when message received in buffer, kernel generates an interrupt) are used to check whether the message is completely received while the local system is busy in computing some other process.
        - Buffering
            - The process of storing the messages received by a server, giving it opportunity to work on other tasks, when it is not specifically in receive mode.
            - Types :
                - Null buffer : Equivalent to having no buffer. Used in time generating system. **Single copy operation**. From sender address space to receiver address space. Synchronous process.
                - Single message buffer : Contains a single message. If buffer is full, message will be dropped. **2 copy operations**. Useful when the communication is minimum.
                - Bounded buffer : Size of buffer fixed. Overflow messages will be dropped, and the sender retransmits the message at a later time, once there is some space in the buffer. **2 copy operation.**
                - Unbounded buffer : No limit on no. of messages to be stored. Stored till the memory allows for it. **2 copy operation.** Not used as two communicating processes may occupy the entire memory.
    - Deciding the message size → **MTU (Maximum Transmit Unit).** Can be sent as a single message, and can have multiple-datagram approach (when message size > MTU).
    - Failures in message passing
        - Request message lost
        - Response message lost
        - Unsuccessful execution.
    - Protocols to follow to manage message passing failure
        - Four message reliable comm.
            - Request msg lost → No ack to sender, retransmit by sender
            - Response msg lost → No ack to receiver, retransmit by receiver
            - Unsuccessful execution → No response from receiver, request sent again
        - Three message reliable comm.
            - First ack removed, response acts as acknowledgment.
        - Two message reliable comm. **(Atleast one semantics, last one semantics)**
            - Sender, response ack removed. Next request acts as implicit ack.
        - Exactly one semantics
            - Can't afford to execute the procedure on the server again and again. For example bank transactions. That would lead to havoc. Hence we need to make sure, that the server executes the procedure only once per request. Unique id for each request, and the result if already executed can be returned.
    - Encoding and Decoding of Message Data
        - The address space for each system is different, and objects operating on pointer values, can't be passed to remote procedures, or migrated. They would lead to no use. They need to be referenced and encoded in stream format, and then decoded on the receiver end, to have the objects, etc. in the same form as was on receiver end, to maintain uniformity through out the system.
        - Methods :
            - Tagged repr : Type of object sent with value.
            - Untagged repr : No labels about the object are sent to the receiver, the system should share a common encoding and decoding philosophy for this to work.
    - Process Addressing :
        - Explicit addressing : process to comm with is specified as a parameter
        - Implicit addressing (functional addressing) : not the process but the service required is sent as parameter, and the process offering that service, has its id returned to the client.
        - Addressing mechanism : machine_id @ local_id. This mechanism is not good for migration purposes. (Link based process addressing) Alternative is to include source machine's id, along with id of the machine that the process currently resides on, i.e. machine_id, local_id, machine_id. Not location transparent
        - Two level naming for transparency.
    - Group Communication
        - Group types (may overlap)
            - Closed group : Only members can take part in comm.
            - Open group : Any process in the system can send a message to the group. Broadcast happens in open group.
        - Group addressing
            - Two level naming : High level → ASCII based name, Low level → Information of nodes in group. If message is sent to multi-cast address, then all processes listening to that address will receive information.
            - Broadcast address → 0 multicast address.
            - Multi-cast and broadcast should be supported by the systems.
        - Modes
            - One-many (multicast), if sent to all, then is called broadcast. A centralised server takes message and transmits to the group. It stores mapping of high level to low level addresses. To send, one specific process, we can send the message to the group server identifying the particular process.

                Multicast comm. is async, since sender has to wait for all processes to receive the message. 

                - Send to all / Bulletin board semantics
                    - Send to all : Message is sent to all processes part of the group, and is buffered until received.
                    - Bulletin board : Message addressed to channel. All receivers can make a copy of the message. This message is available on the channel till all processes receive it.
                - Flexible reliability : In ideal case the group comm. must be designed in a manner, that all nodes receive the message. But that is not the case, and might not even be required by the application.
                    - 0 - reliable : broadcast messages
                    - 1 - reliable : service fetch messages
                    - m out of n reliable : polling mechanisms.
                    - all reliable : consistency maintenance of offline copies of data
            - Many to one : Concept of receiver. Selective and non-selective
            - Many to many : a supercase of one-many and many-one. Ordered message delivery, important for correct functioning of apps. Not trivial for many to many applications. Type of ordering :
                - Absolute ordering : Global timestamps
                - Consistent ordering : Sequencer is used.
                - Casual ordering :
- Remote Procedure Calls
    - Introduction
        - RPC are required to call functions which are not in the same address as the host process. A different but familiar model as compared to that of IPC.
    - The RPC model*
        - Extension on the call response model for local procedure calls.
    - Transparency of RPC*
        - Local procedures and remote procedures are indistinguishable. These needs two types of transparencies :
            - Syntactic transparency (Not very difficult to achieve) : Remote procedure call should have the same syntax as that of the local procedure call.
            - Semantic transparency (Almost impossible to achieve) : Semantics of a remote procedure call should be the same as that local procedure call.
                - Disjoint address space
                - RPC much more suspectible to failure
                - RPCs take longer
    - Implementing RPC mechanism*
        1. Client
        2. Client Stub
        3. RPCRuntime
        4. Server Stub
        5. Server
    - Stub generation*
        - Manual : RPC implementor provides a set of translation functions, which a user can use to implement the stub for the procedures needed.
        - Automatic : Uses Interface Definition Language (IDL)
            - Interface defn : List of support procedures along with types of parameters and return variables. Enough information for server and client to separately perform compile time checks
            - Server that implements procedure exports, client imports. Need to include header file to support the datatypes defn.
    - Writing a distributed application
        1. Interface defination using IDL
        2. Next, client program that imports the interface and server program and exports the interface.
        3. Compilation using IDL Compiler
    - Marshalling : The process of encoding arguments and results in the different formats of the systems involved
    - RPC messages*
        - Call :
            1. Id of remote procedure
            2. Arguments
            3. Message id → Sequence Number
            4. Message type
            5. Client id
        - Reply :
            1. Message id
            2. Message type
            3. Reply status
            4. Result / Reason for failure
        - Differernt possible reasons for failure :
            1. Protocol violation error
            2. Authentication error
            3. Remote procedure not available
            4. Argument decode problem
            5. Exception on execution
    - Parameter passing semantics*
        - Call by value

            Parameters copied to the message and are sent over the network. Done for parameters which are passable (small singular value parameters). But hard for composite types, example multi dimensional array. 

        - Call by reference
            - Need distributed shared memory.
        - Call by object reference → Call by move
    - Call semantics*
        - Possible issues with RPC ops (handled by RPC Runtime)
            - Comm. link may fail
            - Call msg may get lost
            - Caller, callee crashed
            - Response message lost
        - Possibly or maybe call semantics
            - Caller waits indefinitely for response, till timeout
            - Another call is not made i.e. exactly one call is made
        - Last one call semantics
            - Retransmission of call messages based on timeout.
            - Orphan calls : calls made by nodes who have failed. Causes issues in nested calls.
        - Last of many call semantics
            - handles orphan calls using call identifiers. Unique identifiers for every call.
        - Atleast one call semantics
            - Multiple executions can happen, first return message considered.
            - Orphans handled
        - Exactly one semantics
            - Only one time execution.
    - Communication protocols for RPCs*
        - Request Protocol

            Doesn't check for delivery or reception of request. 

            Should use TCP vs UDP in Transport Layer to guarantee delivery of message.

        - Request/Reply Protocol
            - Waits for reply to send another request. Might lead to multiple executions. Exactly one semantics preferred.
        - Request/Reply/Ack Protocol
            - When ack is received by receiver of safe delivery of response, it removes the cache memory corresponding to that request id.
        - Complicated RPCs
            - Involves long duration calls : Periodic probing of the server after the request
            - Argument/result too large : Multiple RPCs, or data fragmentation
    - Client-server binding*

        Handling issues related to client - server binding. 

        - Server Naming : Client provides interface name, has two parts → type, instance id
        - Server Locating :
            - Broadcasting : Client broadcasts the interface name, and the server responds
            - Binding Agent : All Servers registered at the binding agent (Named Server). Provides information about the requested server, by querying in its mapping database.
        - Binding Time :
            - Compile Time : All server information available to client. Server address fixed.
            - Link Time : Registering to binding agent on starting.
            - Run Time : Run time binding when the RPC starts.
        - Changing Binding during execution : Can be changed at both sides. If server not available, it informs binding agent, which fetches a different server with the same service.
        - Multiple Simultaneous Bindings : Through multi cast. One client can contact multiple servers.
    - Server management
        - Two types of servers → Stateful and Stateless
        - Stateful server maintains information about the client and variables related to the procedure executed previously. Functions → open(filename, mode) : returns file id, read(fid,no. of bytes to read, buffer), write(fid, n, buffer), close(fid), seek (fid, pos)

            Benefits include easy implementation, less traffic, availability of data on server side.

        - Stateless server doesn't maintain information related to client processes. Client is responsible for maintaining the information as per its operations. Functions → read(filename, position, n , buffer), write(filename, position, n , buffer).

            Benefits include server crashes don't impact the client information. Client failure doesn't affect other clients ops. 

            This is the method of choice for server implementation. 

        - Creation of server instances :
            - Instance per call : One instance is created per server call. Stateless
            - Instance per session : One instance is created per session of requests from client. Done through the binding agent, which keeps track of servers and the services they provide. The server process id is returned, so that the client knows which server process to contact in the same session. Stateless
            - Persistent server : Stateful.
- Synchronisation
    - *Clock synchronisation**
        - Centralised Algorithms
            - Active
            - Passive
        - Decentralised Algorithms
            - Global averaging
    - Event ordering*
        - Happened before relation for partial ordering
            - Concurrent processes don't have a sense of happened before relation, hence this way of ordering of events is partial ordering. Since all global events are not ordered. Ordering happens with respect to only related processes.
        - Logical clocks
            - A clock type variable maintained by the processors or the system, that is not entirely dependent on the physical time, but is used just as an intuition to order events properly, since that is our primary aim.
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
        - No a priori knowledge of the processes
        - Dynamic scheduling ability
        - Quick decision making capability
        - Balancing system performance and scheduling overhead
        - Stability
            - Processor thrashing

                A scheduling algorithm is said to be unstable if it can enter a state in which all the nodes of the system are spending all of their time migrating processes without accomplishing any useful work in an attempt to properly schedule the processes for better performance. This form of fruitless migration of processes is known as **processor thrashing**.

        - Scalability
        - Fault tolerance
        - Fairness of service
    - Task assignment approach*
        - Process is assumed to be comprising of different individual tasks, and works around strategy to assign these tasks
    - Load balancing approach*
        - Load balancing algorithms (Taxonomy)
            - Static vs Dynamic
            - Deterministic vs Probabilistic
            - Centralised vs Distributed
            - Cooperative vs Non-cooperative

                Scheduling decisions made indepenedently or with a sense of other nodes load. 

        - Issues in designing load balancing algorithms
            - Load estimation policies
                - No of processes on processor
                - Resource demand of processor
                - CPU Utilisation
            - Process transfer policies
                - Whether to transfer the process to a different system or not. This is done if workload > threshold value. Absolute. Concept of low, normal and high load.
            - Location policies
                - Which node the selected process should be transferred to
                    - Threshold : Randomly select node, and check its threshold. If its state doesn't go in prohibit zone, then we can send it over.
                    - Shortest : A given number of distinct nodes are selected. The one with least threshold is picked.
                    - Bidding : Manager, and Contractor. Manager broadcasts a message. Each contractor returns with their bids corresponding to their load value. If in process of bidding, the winner gets overloaded, then it can reject the process, and the bidding process can start again.
            - State information exchange policies

                State here refers to the information about the load on the system in sense of CPU Utilisation or No. of processes active on system

                - Periodic broadcast
                - Broadcast when state changes
                - On-demand exchange
                - Exchange by polling
            - Priority assignment policies
                - Decides the priority of execution of local and remote procedures.
                    - Selfish : Local
                    - Altruistic : Remote
                    - Intermediate : Priority given to group which has higher share of requests.
                - Performance order → Artuistic > Intermediate > Selfish
            - Migration limiting policies
                - Determines the no of times a process can migrate.
                    - Uncontrolled
                    - Controlled : Some designers keep it at 1, some keep it dynamic.
    - Load sharing approach*
        - Issues in designing load sharing algorithms
            - Load estimation policies
                - Just make sure that when a node is active and working, other nodes are not idle. Estimated using CPU Utilisation or Processes on System
            - Process transfer policies
                - All or nothing. The receiver should be idle, and sender should have more than 1 process. Caveat : Transfer process to servers that are expected to be idle, to save processing power.
            - Location policies
                - Sender initiated policy : Sender decides where to send the policy. Broadcasts  message in need of help.
                - Receiver initiated policy : Receiver search for heavy nodes. Broadcasts message about it being ready to help.
            - State information exchange policies
    - Difference between load sharing and load balancing
- Process Management
    - Process Management*
    - Process Migration*
        - Preemptive and non-preemptive.
        - Steps involved :
            1. Selection of process to be migrated
            2. Selection of destination node
            3. Actual Transfer
    - Desirable features of a good Process Migration Mechanism
        - Transparency :
            - Object access level
            - System call and IPC level
        - Minimal Interference
        - Minimal Residual Dependencies
        - Efficiency
        - Robustness
        - Communication between coprocesses
    - Process Migration Mechanisms (Moving houses for employees)
        - Freezing and restarting the process
            - Immediate and delayed blocking of the process
            - Fast and slow I/O operations
            - Information about open files
            - Reinstating the process on its destination node
        - Address space transfer mechanism
            - Total freezing : Process's execution stopped while address space is being transferred. May lead to long time suspension.
            - Pre-transferring : Transfer as the process is being executed. After that transfer modified pages ( dirty bits)
            - Transfer on reference
        - Message forwarding mechanism

            Type of messages → Received at source after execution stopped, Received at source post execution of new node, Messages sent to migrant process post execution on new node 

            - Mechanism of resending the message
                - Dropped, or unavailable status returned. Broadcast used to locate process.
            - Origin site mechanism
            - Link traversal mechanism
            - Link update mechanism
                - Comm via location - independent links. Capable of duplex comm. channels.
        - Mechanisms for handling co-processes
            - Disallowing separation of co-processes
                - Concept of logical host
            - Home node or origin site concept
    - Process Migration in Heterogeneous Systems

        External data representation

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