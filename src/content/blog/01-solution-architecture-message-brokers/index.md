---
title: "Architect Handbook: Message Brokers"
description: "Detailed exploration of message brokers"
date: "Sep 18 2024"
---

In this module, you will learn about the role of message brokers in system design. We will start with foundational concepts and gradually move towards more advanced topics. By the end of this module, you will have a solid understanding of what message brokers are, when and why we should use them.

## How Services Communicate

...

- Overview
- History of Message Brokers
- What is a Message Broker?
- Why Use a Message Broker?
- Types of Message Brokers
- Use Cases
- Patterns and Best Practices
- Conclusion
- References

### Terms and Definitions

- **Software architecture** - The high-level structure of a software system, defining its components and their relationships
- **Component** - A modular part of a system that encapsulates a set of related functions (e.g. Microservice, Lambda function)


### Components communication

Imagine that you are working on system that contains two components: a web application and a server. The web application needs a way to
communicate with the server in order to save or modify user's data. As it was discussed in the previous section, there are several ways
to achieve this communication we can use HTTP or WebSockets protocols. In both cases, the web application sends a request to the server and waits for a response. We call this synchronous communication, where the client waits for the server to respond before continuing its process.

![Web application and server communication](/blog/01/ah-mb-web-to-serv.png)

Now think about a different scenario where you have two components: a server and a worker. The server needs a way to start a long-running task, such as
video processing, without waiting for the task to complete. In this case, the server can send a message to the worker to start the task and then continue processing other requests. To complete this communication worker can send a message back to the server when the task is done. This is an example of asynchronous communication, where the server can continue its process without being blocked by the notification worker's response.

![Server and worker communication](/blog/01/ah-mb-serv-to-notif.png)

Important to note that technically in second scenario we still will have a synchronous response from worker. However, do not confuse this with the synchronous communication. In this case, the **server does not wait** for the worker to complete the task before continuing its process.

The right use of synchronous and asynchronous communication is crucial for building scalable and responsive systems. And as architects, we need to understand the trade-offs between these two approaches. With synchronous communication, we can achieve simplicity and ease of use, but it can lead to bottlenecks if one component is slow to respond and by that can affect the overall system performance. On the other hand, asynchronous communication allows for better resource utilization and responsiveness, but it can introduce complexity in managing the state and handling failures. One of such potential problems is that the worker need to know how to communicate back to the server when the task is done. With system growing in size and complexity, it becomes harder to manage these interactions and trace the flow of communication. This understanding is essential, because this is where message brokers come into play.


### What is a Message Broker?

In modern software architecture, components often need to communicate with each other. This communication can take various forms, such as synchronous or asynchronous messaging. Message brokers play a crucial role in facilitating this communication by acting as intermediaries between services.

### References

- https://www.confluent.io/learn/message-broker/