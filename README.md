Some useful commands:
   - Running server(on local mac): sudo /usr/local/sbin/rabbitmq-server (On server run crash a probable error link: https://stackoverflow.com/questions/42895634/rabbitmq-server-boot-failed-on-mac-os-x-el-capitan/42898348#42898348)
   - List queues: sudo rabbitmqctl list_queues
   - Check queue contents: rabbitmqadmin get queue=<queue_name> requeue=true count=10
   - Check unacknowledged messages(not acknowledged by consumer): rabbitmqctl list_queues name messages_ready messages_unacknowledged
   
Experiments:
   - Tutorial 1 (https://www.rabbitmq.com/tutorials/tutorial-one-python.html): sender and reciver task, start a consumer(receive.py), which will run continuously waiting for deliveries.  Start the producer(send.py). The producer program will stop after every run.
   - Tutorial 2: working with workers, how to work with multiple workers, how rabbitmq handle situation when one worker dies(using help of acknowledgement), and how to handles cases when rabbitmq itself stops (https://www.rabbitmq.com/tutorials/tutorial-two-python.html): related files in current codebase - new_task.py, worker.py


Production checklist recommended by Rabbitmq: https://www.rabbitmq.com/production-checklist.html

Additional Important links:
 - How the memory limit works: https://www.rabbitmq.com/memory.html
 - How the disk limit works: https://www.rabbitmq.com/disk-alarms.html
 - How clients can determine if they are blocked: https://www.rabbitmq.com/connection-blocked.html
 - Networking guide: https://www.rabbitmq.com/networking.html
 
Create admin user on rabbitmq
  - rabbitmqctl add_user <username> <password>
  - rabbitmqctl set_user_tags <username> administrator
  - rabbitmqctl set_permissions -p / <username> ".*" ".*" ".*"

Setup:
 - installation :brew install rabbitmq
 - start server: brew services start rabbitmq
 - Server location: /usr/local/opt/rabbitmq/sbin/rabbitmq-server

For issue: "Error: Failure while executing; `git config --local --replace-all homebrew.private true` exited with 1."
Refer this link: https://saurabhbuddha.blogspot.com/2018/10/rabbit-mq-issues-and-fixes-setup-issue.html


#### Important points about rabbitmq:
 - It accepts, stores and forwards binary blobs of data ‒ messages. 
 - Producing means nothing more than sending. A program that sends messages is a producer
 - A queue is the name for a post box which lives inside RabbitMQ. Although messages flow through RabbitMQ and your applications, they can only be stored inside a queue. A queue is only bound by the host's memory & disk limits, it's essentially a large message buffer. Many producers can send messages that go to one queue, and many consumers can try to receive data from one queue. 
 - Consuming has a similar meaning to receiving. A consumer is a program that mostly waits to receive messages
 - Producer, consumer, and broker do not have to reside on the same host; indeed in most applications they don't. An application can be both a producer and consumer, too. 
 - RabbitMQ speaks AMQP 0.9.1, which is an open, general-purpose protocol for messaging. There are a number of clients for RabbitMQ in many different languages
 - In RabbitMQ a message can never be sent directly to the queue, it always needs to go through an exchange. 
 - When a consumer (subscription) is registered, messages will be delivered (pushed) by RabbitMQ using the basic.deliver method. The method carries a delivery tag, which uniquely identifies the delivery on a channel. Delivery tags are therefore scoped per channel. 
 -  Depending on the acknowledgement mode used, RabbitMQ can consider a message to be successfully delivered either immediately after it is sent out (written to a TCP socket) or when an explicit ("manual") client acknowledgement is received. Manually sent acknowledgements can be positive or negative and use one of the following protocol methods:
    ```basic.ack is used for positive acknowledgements
    basic.nack is used for negative acknowledgements (note: this is a RabbitMQ extension to AMQP 0-9-1)
    basic.reject is used for negative acknowledgements but has one limitation compared to basic.nack
    ```
 - 
  

 
#### Important Pika(python library for interacting with rabbitmq) commands:
 - Installing pika: pip install pika
 - Establish a connection with RabbitMQ server:
   ```
   #!/usr/bin/env python
   import pika

   connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
   channel = connection.channel()
   ```
 - Create a queue to which the message will be delivered, Creating a queue using queue_declare is idempotent ‒ we can run the command as many times as we like, and only one will be created.
   ```
   channel.queue_declare(queue='<queue name>')
   ```
 

