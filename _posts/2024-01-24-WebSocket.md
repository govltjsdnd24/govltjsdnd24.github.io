﻿---
categories: [ Development, Study, WebSocket]
tags: [socket] 
---

I'm starting a project that has a heavy emphasis on WebRTC technology, which provides consistent text, audio, and video data transmission between among clients. Then I thought, "what's the difference between WebSocket and WebRTC if both of them allow communication between clients?", and proceeded to dig deeper into the topic.

## What is WebSocket?
Why would we need to use WebSocket? WebSocket is used in the fulfillment of a truly simulatneous Web service; it is used to automatically take a certain action when a Server-Side Event is received. Okay, that seems really useful... but then again, what is WebSocket?

WebSocket is a bidirectional communication protocol that resides over TCP. It allows transmission of data between a client and a server, and requires STOMP (Simple/Streaming Text Oriented Messaging Protocol) running atop it since STOMP defines the specification and interoperable format of messages being transferred. WebRTC, the API that I want to implement, is a direct interaction among multiple clients with little to no mediator in between; the presence of a server between clients is the difference between the two technologies.

## General Process

Now that we briefly went over the definition of WebSocket, we must know learn how to implement it. "But, wait" you ask, "if it's not related to WebRTC, why would you want to use it?" The reason is: the asynchronous trigger that WebSocket brings is really useful in many situations (for example: chat session or notification functions). 

I followed a guide provided in the Spring website for implementation. 

Firstly, I cloned a tutorial project.
```bash
git clone https://github.com/spring-guides/gs-messaging-stomp-websocket.git
```
Within the folder you will be able to see two folders: one, an already complete version and two, a barebone model. The tutorial directs us to start with the initial folder, but 
## Troubleshooting

## Reference

