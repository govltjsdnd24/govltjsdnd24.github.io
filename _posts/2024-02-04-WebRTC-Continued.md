---
categories: [ Study, WebRTC ]
tags: [ webrtc ] 
---

Last post, I talked about what WebRTC is and what STUN and TURN are in general. I want to continue with the flow and move on to talk about the specificalities of them, and also, their contemporary, open-source implementation called OpenVidu. I wish to also talk about the problems and the troubleshooting process I experienced while trying to make it work in my project.
## STUN, TURN, and ICE
A recap on STUN and TURN. They both serve the purpose of being the broker between two clients, establishing a connection between them. They both enable the clients to bypass NAT during their attempt to reach one another, while TURN having the upper hand in dealing with symmetric NATs and firewalls. I believe I failed to give a clear, definite reasoning on why TURN is better than the other in these situations, so please allow me to elaborate.
STUN does allow connection between clients and it does so by revealing the public IP address of each. However, this action is instantaneous and it fails to persist throughout the entire process. TURN on the other hand stays in the path connecting the two devices even when the initial connection has been made. In a situation where firewalls or any restrictive components are present, regular messages may fail to reach one another, and might even fail to discover each other's IP addresses because of the secretive and concealing nature that firewalls have; TURN relays all the data sent from the clients and helps them navigate through/bypass all the impediments that exist in the path. 
Of course, contemporary WebRTC systems don't just use one of either but seeks to implement both. Below is a more precise version of the WebRTC layout:
![Client](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/0c32cca7-a28a-40da-993c-240f13c57ced)

Okay, so that was the difference in the roles of TURN and STUN. Now let's talk about what ICE is. ICE (Interactive Connectivity Establishment) is basically a framework that routes the optimal path between two clients. Among all the available paths that is given to the clients, ICE will handpick the most direct and efficient connection while bypassing NATs and other communication barriers. Of course, this kind of functionality cannot be done by ICE alone, but also TURN and STUN. ICE will open NAT ports required for the interaction and acquire the necessary address and port information for connection.
  
## OpenVidu
Now that we are done talking about the fundaments of WebRTC, let's move on to OpenVidu. OpenVidu is a free, open-sourced platform that uses WebRTC to enable building of video and audio chat applications with ease through the usage of several APIs provided to its users. Openvidu is well-known for its flexible and facile implementability, even being available in environments such as AWS or on premise servers. This factor rendered me to select this certain framework in an attempt to implement WebRTC; since I was a complete novice in this area, popularity and ease of use were very essential for me.
The method I followed for the implementation of OpenVidu can be generalized to these series of steps:
```bash
# Updates the environment
sudo apt update 
sudo apt upgrade 

# Install Openvidu
sudo su 
cd /opt curl https://s3-eu-west-1.amazonaws.com/aws.openvidu.io/install_openvidu_latest.sh | bash 

# Configure Openvidu 
cd ./openvidu 
nano .env 

//Altered Lines
//DOMAIN_OR_PUBLIC_IP={Server's domain/Public IP address}
//OPENVIDU_SECRET={Openvidu Password} 
//CERTIFICATE_TYPE=letsencrypt 
//LETSENCRYPT_EMAIL={email} 
//HTTPS_PORT={HTTPS Port number}

# Run Openvidu 
./openvidu
```
 Nonetheless, never has a process been able to be followed without any hiccup. Despite my ardent attempt to implement OpenVidu--a so-called EASY framework--I had to struggle for hours trying to figure out what the problem was. How did I overcome it? Of course, it would be exhilarating to cover the troubleshooting process in this post, but I fear that the post will turn out to be overwhelmingly long and will pass the topic on to the next entry.
## Conclusion 
Today, I finished the explanation on the basis of WebRTC, covering not only TURN and STUN but also--although shortly--ICE. I also introduced OpenVidu and gave a short description on the method I followed for the implementation. I know that this article left more questions than solutions, but please, I did it for the sake of the next post, where I will cover the entirety of the troubleshooting process I followed in order to make OpenVidu work. Thanks for reading my humbly post.

## Reference
[https://gh402.tistory.com/45](https://gh402.tistory.com/45)

[https://www.digitalsamba.com/blog/stun-vs-turn](https://www.digitalsamba.com/blog/stun-vs-turn)



