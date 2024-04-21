
<details>
<summary>Module 8</summary>


1. what is _**amqp**_?
The term "amqp" stands for Advanced Message Queuing Protocol. It is an open standard messaging protocol that enables communication between applications or services. AMQP provides a reliable and efficient way to exchange messages between different systems, regardless of the programming languages or platforms they are built on.




2. what it means? guest:guest@localhost:5672 , what is the first _**guest**_, and what is the second _**guest**_, and what is _**localhost:5672**_ is for?

The string "amqp://guest:guest@localhost:5672" is a connection string for an AMQP (Advanced Message Queuing Protocol) service.

The first guest is the username for the AMQP service.
The second guest is the password for the AMQP service.
localhost:5672 is the host and port where the AMQP service is running. "localhost" means the service is running on the same machine, and "5672" is the default port for AMQP.
In the provided code, CrosstownBus::new_queue_listener("amqp://guest:guest@localhost:5672".to_owned()).unwrap(); is creating a new listener for a queue on the AMQP service. The listener will listen for messages on the "user_created" queue. The QueueProperties are set to not auto-delete the queue, not make it durable, and to use a dead letter queue.

Commit 3 : 
The spike that occurred below is because there are so many users accessing it, but the queue process is slow because a thread sleep is added. So the process will occur slowly by the consumer. The total number of queues is only 2.

The number of queues in RabbitMQ can vary based on several factors:

1. **Number of Producers**: If there are more producers on one machine sending messages, more queues might be created to handle the load.

2. **Number of Consumers**: If there are fewer consumers on a machine, messages might accumulate in the queues, leading to more queues being created.

3. **Configuration**: The configuration of RabbitMQ can affect the number of queues. For example, some configurations might create a new queue for each type of message, while others might use a single queue for all messages.

4. **Load Balancing**: In a distributed system, the load might be balanced differently across different machines. Some machines might handle more messages and therefore have more queues.

5. **Manual Intervention**: Queues can be manually created or deleted by users. If someone manually created more queues on one machine, that machine would have more queues.

Remember, the number of queues is not necessarily an indicator of system performance or efficiency. What's more important is how effectively the messages are being processed. If messages are being produced faster than they can be consumed, it can lead to a buildup of messages in the queues, regardless of the number of queues.

![alt text](image.png)

Commit 4 :

When you have multiple subscribers (or consumers) as opposed to just one, the processing of messages from the queue can happen in parallel. Each subscriber can independently take a message from the queue and process it.

In the case of three subscribers, they can collectively process three messages at the same time, while a single subscriber can only process one message at a time.

So, if you run the publisher multiple times and it adds many messages to the queue, having more subscribers will allow those messages to be processed faster. This is because the work of processing the messages is being distributed among multiple subscribers, rather than being handled by just one.

This is a common pattern in distributed systems, where work is divided among multiple workers to increase throughput and reduce the time it takes to process large amounts of data.

in this picture, each subcriber handle one so it can get faster
![alt text](image-5.png)

in this picture the message quicker drop quickly than only using one subcriber
![alt text](image-4.png)

</details>