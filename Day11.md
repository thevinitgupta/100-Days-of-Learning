# Message Queues for Beginners
Message queues are basically another Queue system that handles messages. 
The messages could be something simple like `data` to be sent or even some `procedure calls`.

<img src="https://www.cloudamqp.com/img/blog/thumb-mq.jpg"/>

The system that sends the message is called `Producer` and the system that receives the message is called a `Consumer`.

The task of a message queue is to store these messages from a `producer` until the `consumer` is ready.

## Why Message Queues?
Since, messages are simply instructions or data that needs to be transferred, why store it?
The important task of a message queue is to ensure that the `consumer` is free to receive the message and work on it. 
If the `producer` just keep on sending instructions, they will be put on hold until the consumer is free. 

This might cause the consumer to crash, as it is not able to handle so many tasks at a time. 
This is where the message queues come in. 

## How do they work?
Well, the producers send messages which are stored in a queue - `data structure that follows the First In, First Out(FIFO) princple`.
Upon receiving the message from the consumer, the `message queue` informs the producer that their request have been registered. 
This `enables the producers to use their resources to work on tasks` that can be done while the consumer processes this message.

The message queue then sends the messages or tasks to the consumer one by one after the consumer `notifies the queue` that it is free to do something.
Once a message is processed, the `data is sent to the producer` so that they can process it.

![Message Queue](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/ed9cb845-1cde-459e-9516-a2e4ab2b9f20)


## Ordering a Domino's Pizza
Who doesn't love ordering Pizzas from Domino's right?

<img src="https://media.giphy.com/media/jn2iXu2HRpMuovBrrV/giphy.gif"/>

Well without a message queue like system, no one would. Let's understand how.

Let's say the Domino's near to you has the capacity to make 5 pizzas at a time. 
When you open their app to order, the ovens are all occupied. 
You click on order and the screen says you have to wait 45 minutes before you can order as their kitchen is full.

![Loading-PNG-Images-HD](https://us.123rf.com/450wm/lishchyshyn/lishchyshyn1904/lishchyshyn190403199/132862735-vector-loading-icon-futuristic-progress-design.jpg?ver=6)

Would you still like to order or will you uninstall their app?

But in reality, what happens is your order is registered and you get a confirmation. 
You just sit and wait until your order is delivered at your door. 
This is exactly how a message queue works.

## Advantages of using Message Queues
 - Make a system `easy to maintain and scale`
 - Develop different parts of a system and `evolve separately`
 - Develop different parts using `different tech stacks and different teams`

## Examples of Message queue services
 - Kafka
 - RabbitMQ
 - IBM MQ
 - Zero MQ
 - Redis provides a service
   
