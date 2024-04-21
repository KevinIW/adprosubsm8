
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
Spike yang terjadi dibawah ini karena sangat byk user yang mengakses tetapi process queue yang terjadi berlangsung lambat karena ditambahkan thread sleep. Sehingga process nya akan terjadi secara perlahan lahan oleh consumer.
![alt text](image.png)

</details>