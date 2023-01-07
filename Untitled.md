- Telegram has a feature of creating new channels. 
- These groups can be accessed by any individual who is necasaarily not in the contact list of the creator or the admins.
## Internal detail of message passing
Client initiates a RPC call to the Api Gateway of the telegram.
The api gateway adds clients request to the message broker server.
The message broker identifies to which service the message has to be sent and adds the request to that queue which belongs to that set of servers.
The message broker maintains a lookup table and has a pool of queues.
Each queue maps to a servers IP address and it is stored in a database.
When the server requests the message broker to poll a request message broker find the queue of the server and returns the request.
Similarly server adds the response for the same in the same manner.
This system can scale as we can add more nodes and we have to update only the lookup database.
Another approach can be that instead of a message broker we can use a advanced router which knows the details about the server in its network and maintains a queue and there will be no overhead for fetching the location of server for each operation in the queue performed.
If we have to scale this kind of architecture then after adding more nodes we have to reconfigure all the routers.

## What type of communication is used
Telegram uses asyncrhonouse communication.
- Client sends the request to the server and waits for acknowledgement.
- When server recieves the request it immediately sends the response to the client and client continues some other process. 
- When server completes processing the request it sends response to the client and doesn't wait for the acknowledgement and becomes inactive.
## How group communication takes place
The type of group communication used in the telegram app is broadcast communication . It's main feature is to be able to create a channel in which anyone can join the channel and send a message which is then broadcasted to all the members of that channel . Since it does not require any processing whatsoever, communication is very fast in comparison to other modes of communication. However, it does not support a large number of processes and therefore it has to keep a cap on the maximum number of people that can join a channel.

## What protocals are used
Communication between client and the telegram api gateway is https
and internal communication between various micro services is through RPC protocol. Since in a channel people can share various types of files and images. Clients will send the files to api gateway through https and ftp is used to save it to a file server. Communication between the databases and the main application will be gRPC since we can keep a single driver to connect to the database from various languages.

## Security and privacy used in communication?
End to end encryption is used in telegram.
Each user is provied with a private and a public key pair and a group has a public and private key pair.
Every message is encrypted using the public key of the group and private key of the sender and encryption is done in the client side.
When someone tries to fetch the message it is decrypted using the private key of reader and the public key of the group.