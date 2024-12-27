---
categories: [ Study, MessageQueue]
tags: [ mq ] 
---

I stumbled upon the concept of message queues while trying to implement AWS cloud architecture; there were multiple services that I wished to utilize but data transmission among them was too frequent--and highly likely to be asynchronous. That's when I realized what message queues are--and that they are available in AWS--and I decided to create this post for both my enlightenment and the readers'.

## What are message queues and messages?

Message Queue is the component of a messaging middleware solution which enables transit of data between isolated applications and services. Message Queue is a "message", data packet created from one application for the purpose of being utilized on another one, that is stored according to the order that they arrive, and are saved until they are processed. Message Queues are very often utilized in the contemporary companies; according to the 2022 Forbes Global 2000, 90% of the top 100 companies utilized this technology.

## Utilization

Let's say that there is a web service that automatically revises and corrects faults in videos. We want 50 concurrent requests to be able to be processed, but only 10 files can be worked on simultatneously in a single machine. If the services are embedded in a single batch, this problem is solved by multiplicating the device count by 5. 

![Java Appliaction](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/ec1bd74d-9c57-46ae-82db-ee0d22d7ca50)

However, let's see that the Web Application Server is implemented in Java while the automatic correction module is written in C++. The OS is also different; the former works in Windows while the latter in Linux. We know that we can't be running the entire process in a single machine. This is the circumstance where message queues can be useful. Because of message queue's asynchronous nature, it ensures execution of the request even if it is not concurrent.

Let's take a look at a more theoretical example: Monolith and Microservices. Monolith has all components of a service in a single group, while in Microservice, each service is seperated. This makes communication among various services in Microservices very important.

What if I want to  utilize HTTP for message exchange? HTTPs are composed of quite heavy structure; it has a size five times bigger than AMQP(Advanced Message Queuing Protocol). Therefore, it would be a complete overkill if short messages are forwarded frequently.

That's why in MSA(MicroService Architecture), message queues are utilitized. Sending and receiving of high traffic data packets are supported, with the quality of messages being promised, MQs are excellent means of link among services.

## Characteristics of Message Queues

- Message Queue works as message buffers to transmit messages asynchronously. 
- It allows servers to be loosely coupled.
- It ensures the integrity of messages.
- It is even suitable for messaging between different devices.

## Process of Message Queues

1. Message Queue is initialized.
2. Producer publishes a message to the queue. Often, messages are divided into a header and a payload. The header contains metadata of the message such as receipient and sender info. The payload of the mssage, on the other hand, contains desired information.
3. Message is buffered in queue and synchronized
4. When a message becomes availabe, it is sent to the receiver. The retrieval process may be blocking or non-blocking, depending on the type of message queue being used.

## Sync/Async && Block/Non-Block

When talking about the essence of MQs, we cannot mention the concept of synchronization and blocking. So, let's clarify their definitions.

In sync, the called function takes care of both the commence and termination of the calling function. In async, the called function is responsible for the execution and ending of itself.

Let's move on blocking.

What is blocking? In a blocking operation, the calling process will wait until the operation completes before it can proceed with further execution.

What about non-blocking? In a non-blocking operation, the calling process will not wait for the operation to complete, but will receive an indication immediately and can continue with other tasks.

Hence, it is about the order that a process is execute; in non-blocking, a calling program can be immedately executed, but in blocking, such is impossible.

I know that the concept is very vague and complicated. I will make another post about this concept later on if I have time.

## RabbitMQ

A recommendation of available Message Queue available to the public is RabbitMQ. It is very simple and even has advantages with even the most basic manipulation. It enables the scaling-out of discrete services with ease.

Some advantages of this tool is:
- Several client library
- Saving in message disks
- Ensure Message integrity
- Cluster options for igh scalability 
- Web UI with good usability

## Conclusion

Today we covered the topic of message queues. It was done rather abrubtly, amidst the articles on database, but with the memory of message queues fresh in my brain, I assumed this was the best timing to conduct the recording.

What is important with using tools such as message queues is not just the utilization experience, but the reason for why you would try to implement it in a given environment.

Anyways I will try to leave any inspiration I acquired during my way like today's post. Take care and see you again.

## Reference

[https://www.rabbitmq.com/docs/queues](https://www.rabbitmq.com/docs/queues)

