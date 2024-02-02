---
categories: [ Study, WebRTC ]
tags: [ webrtc ] 
---

This is another huge topic in the scheme of various web projects. WebRTC allows its users to be able to communicate in real-time with whoever is connected to the same session that the users are located in, allowing the utilization of cameras and microphones, without the need to implement external software. This changed things in a way that small teams of developers and students didn't have to implement things on their own and could just choose to adopt this certain technology into their projects. In fact, it was so efficient and well-built that all of the major real-time communication software like Zoom, Google Meet, and Facebook utilize this piece of innovation.

## Explanation
Let's move on to the essential topic. You might ask : "I get that WebRTC is good and all but... what is WebRTC?" WebRTC is a technology that establishes peer-to-peer-like connection between browsers and maintains it steadfastly, allowing users to trade various types of data with complete ease and reliability. By peer-to-peer-like, I mean that it involves a certain server that initially connects you to your friend, and after that inceptive interception , you can maintain the connection by yourself. This is important because it removes the centralized format of previous communication and also deters the server from being overloaded with traffic, thus failing to keep its users up-to-date with the messages/data that they have to be informed about. WebRTC was a giant leap client/browser-wise, also; in a regular HTTP interaction, a user had to quit the connection after a request-response life-cycle, but in WebRTC, users can maintain connection as long as he/she likes, granting much fluidity to the interchange of data one can have with its peer.

## STUN and TURN
As good as WebRTC sounds, there are some restrictions that exist inherently. In order for peers to communicate with each other, they must have each others' IP addresses. Before we go on to talk about STUN or TURN, let's clear up on what a NAT is. Most people would already know, but there's a thing called private IP address and a public one. In order for a person to access the public network, one must go through Network Address Translation, and this technology translates private address to the public address that is shared among devices connected within the same private network. It is a handy feature that allows limited number of public address to be distributed to multiple devices, and also has benefits security wise for obvious reasons.
![Client](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/2c0087c0-c4dc-4534-a65a-362642a658be)

However, this is bad for WebRTC, because WebRTC is basically a communication between two browsers, and in order for that to happen, NAT must STOP translating private addresses to public ones. Basically, in a regular server-client communication, this won't be a problem because server's address is already known to the client. However, in a P2P connection, neither of the side actually know the address of another; even if one is aware of the other's IP address at one moment, both the public and private IP addresses tend to be dynamic, and such information will no longer be valid in a few moment. This is where STUN comes in. STUN ( Session Traversal Utilities for NAT ) works in a way that it reveals the clients their public IP address that they can use for external communication. This allows clients to communicate directly with their public addresses. Now this sounds really nice doesn't it? As long as there are no multiple clients in the same network, that is.
![Client (1)](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/1a19a18e-cc4f-4b25-a321-ba3eaccaf643)

Then, what if there ARE multiple clients in a network? Remember when I mentioned TURN? This is the moment this guy jumps in. TURN ( Traversal Using Relays around NAT ) is similar to STUN in a way that it accesses a server in the public network for address confirmation. The differing aspect is that a TURN server will send the public IP address and port number that the client is allocated to, which will be processed by the NAT to forward the message to the client. 
![Client (2)](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/5e7d023b-5813-4d1d-b1f2-58c7abcf6c2a)

However, the truth is that, there isn't really a distinct difference between the two technologies. What sets them apart is that they have different purposes: STUN is used to identify the presence of NAT and the public IP address of the clients, and TURN is used to actually establish the P2P connection. Despite the difference in their usage, the important thing is that they are both vital components of WebRTC and should be used regardless of situation. 
 
## Conclusion 
Today, I covered the topic of WebRTC, STUN, and TURN. I really had a lot to say actually, since WebRTC is such a big topic. I could go on to explain the concept of ICE, OpenVidu, , the steps I followed to implement the software, and troubleshooting methods I used to resolve problems and errors. Nonetheless, I believe this is it for today's post. I'll come back with even more information on WebRTC as soon as possible.


## Reference
[https://andonekwon.tistory.com/59](https://andonekwon.tistory.com/59)
[https://www.techtarget.com/searchunifiedcommunications/definition/WebRTC-Web-Real-Time-Communications](https://www.techtarget.com/searchunifiedcommunications/definition/WebRTC-Web-Real-Time-Communications)


