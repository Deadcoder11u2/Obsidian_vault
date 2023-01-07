# Internal Detail about application for Message passing
### Message Queueing Model
The basic idea behind a message-queuing system is that applications communicate by inserting messages in specific queues. These messages are forwarded over a series of communication servers and are eventually delivered to the destination, even if it was down when the message was sent. In practice, most communication servers are directly connected to each other. In other words, a message is generally transferred directly to a destination server. In principle, each application has its own private queue to which other applications can send messages. A queue can be read only by its associated application, but it is also possible for multiple applications to share a single queue. An important aspect of message-queuing systems is that a sender is generally given only the guarantees that its message will eventually be inserted in the recipient's queue. No guarantees are given about when, or even if the message will actually be read, which is completely determined by the behavior of the recipient. These semantics permit communication loosely-coupled in time. There is thus no need for the receiver to be executing when a message is being sent to its queue. Likewise, there is no need for the sender to be executing at the moment its message is picked up by the receiver. The sender and receiver can execute completely independently of each other. In fact, once a message has been deposited in a queue, it will remain there until it is removed, irrespective of whether its sender or receiver is executing.
![[Pasted image 20221009133000.png]]

![[Pasted image 20221009133029.png]]

### General architecture of message passing system
Let us now take a closer look at what a general message-queuing system looks like. One of the first restrictions that we make is that messages can be put only' into queues that are local to the sender, that is, queues on the same machine, or no worse than on a machine nearby such as on the same LAN that can be efficiently reached through an RPC. Such a queue is called the source queue. Likewise, messages can be read only from local queues. However, a message put into a queue will contain the specification of a destination queue to which it should be transferred. It is the responsibility of a message-queuing system to provide queues to senders and receivers and take care that messages are transferred from their source to their destination queue. It is important to realize that the collection of queues is distributed across multiple machines. Consequently, for a message-queuing system to transfer messages, it should maintain a mapping of queues to network locations. In practice, this means that it should maintain a (possibly distributed) database of queue names to network locations, as shown in Fig. 4-19. Note that such a mapping is completely analogous to the use of the Domain Name System (DNS) for e-mail in the Internet. For example, when sending a message to the logical mail address steen@cs.vu.nl, the mailing system will query DNS to find the network (i.e., IP) address of the recipient's mail server to use for the actual message transfer.

![[Pasted image 20221009133150.png]]

Queues are managed by queue managers. Normally, a queue manager interacts directly with the application that is sending or receiving a message. However, there are also special queue managers that operate as routers, or relays: they forward incoming messages to other queue managers. In this way, a messagequeuing system may gradually grow into a complete, application-level, overlay network, on top of an existing computer network. This approach is similar to the construction of the early MBone over the Internet, in which ordinary user processes were configured as multicast routers. As it turns out, multicasting through overlay networks is still important as we will discuss later in this chapter. Relays can be convenient for a number of reasons. For example, in many message- queuing systems, there is no general naming service available that can dynamically maintain qneue-to-Iocation mappings. Instead, the topology of the queuing network is static, and each queue manager needs a copy of the queue-tolocation mapping. It is needless to say that in large-scale queuing systems. this approach can easily lead to network-management problems. 

One solution is to use a few routers that know about the network topology. When a sender A puts a message for destination B in its local queue, that message is first transferred to the nearest router, say Rl, as shown in Fig. 4-20. At that point, the router knows what to do with the message and forwards it in the direction of B. For example, Rl may derive from B's name that the message should be forwarded to router R2. In this way, only the routers need to be updated when queues are added or removed. while every other queue manager has to know only where the nearest router is. 

Relays can thus generally help build scalable message-queuing systems. However, as queuing networks grow, it is clear that the manual configuration of networks will rapidly become completely unmanageable. The only solution is to adopt dynamic routing schemes as is done for computer networks. In that respect, it is somewhat surprising that such solutions are not yet integrated into some of the popular message-queuing systems.
![[Pasted image 20221009133339.png]]


# What type of communication is used?
### > Message passing

# What protocols are used for communication in your application?
### > RPC in internal communication between database server, file server and web servers, HTTP/HTTPS in communication between client and api gateway.

# How group communication takes place?
### > Finally, relays can be used for multicasting purposes. In that case, an incoming

# How security and Privacy used in communication?
### > Reverse Proxy, data encryption public/private key, CORS.