---
categories: [ Development, OpenVidu]
tags: [ webrtc ] 
---

This post, I will explain the steps I followed in order to make OpenVidu work. Mind you, this process can seem simple and actually prove to be so if you follow the correct guideline. Nevertheless, it is nigh impossible to tell which part of the method you did wrong if and when you receive an error message. Of course, this is something of a hyperbole, because the reason for my retardation could have been derived solely from my lack of intellect. Any way, I sincerely hope that whoever's reading this will not come across the problems I had while trying to implement this damned piece of technology.
## Testing on Local Machine
You know what the surprising thing is? OpenVidu is incredibly easy to use in a local domain. You can simply follow the documentation provided by OpenVidu itself. Here, we are trying to mimic the procedure for 'openvibe-vue' turorial. Firstly, you  run a docker container with the docker image provided by the company.
```bash
docker run -p 4443:4443 --rm -e OPENVIDU_SECRET=MY_SECRET openvidu/openvidu-dev:2.29.0
```
Here, the *'-p 4443:4443'* option maps Docker's port 4443 to the device's port 4443.  '--rm' option automatically deletes image upon the container's termination, and '-e *OPENVIDU_SECRET=MY_SECRET'* sets the environmental variable called *OPENVIDU_SECRET* to the provided string; OpenVidu has environmental options manipulated by the '.env' file, which is currently inaccessible to us (because it's a docker image). The image is automatically downloaded from the archive and deleted accordingly.
The next step makes us follow these instruction:
```bash
git clone https://github.com/OpenVidu/openvidu-tutorials.git -b v2.29.0  
cd openvidu-tutorials/openvidu-basic-java
mvn spring-boot:run
```
Here, we clone the OpenVidu tutorial into our local repository and run it. To my surprise, everything runs fine without any problem as long as the docker is setup correctly. If you can see this screen after connecting to the OpenVidu deployment server, you've done it correctly. 
![openvidu_screen](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/9918eb18-99a4-43de-83bd-b764ed6c61fd)

Remember to run both vue--or any of its counterparts--and spring because OpenVidu necessitates  both client and server.
Openvidu-vue result screen:
![openvidu_vue](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/c13a97a4-6b6b-40c1-8599-66f124ceac7c)

Now, you were able to successfully run OpenVidu, but do you understand what's going on under the hood? Let's briefly go over the steps.
The process proceeds in such steps:
 - Initialize session -> Session ID created
 - Establish connection with the session ID -> Token provided
 - Connect to session with the token
 - Traffic data in a publish/subscribe format
![Web Application Server](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/51c6ec52-f598-4a50-b050-a45bb791ccb9)


  Each user has to make connection with the session ID in order to join the session, and session ID is invalid as long as it's created by OpenVidu server. The session is opened when the first user comes in and the last user leaves. This means that the session can be seen as perpetual as long as there's a user in it. Tokens, too, are theoretically ever-lasting.
## Testing on the Premise
The real problem comes when one proceeds to deploy OpenVidu on the server. In the OpenVidu documentation page, there are some options for how you can deploy OpenVidu: local, AWS, and on-premise. Running it on the local machine doesn't really mean anything, and not everyone has access to AWS--one can be using another cloud service or just plainly wish to use their own server--which leaves us with the choice of on-premise.
We just simply have to follow the documentation for the first part of the deployment. Firstly, we download the on-premise version of OpenVidu. Remember not to use the old one we used on the local machine.
```bash
curl https://s3-eu-west-1.amazonaws.com/aws.openvidu.io/install_openvidu_latest.sh | bash
```
The docker containers have the following components:
 - OpenVidu Server: In charge of signaling
 - Kurento Media Server: Mediates data
 - Coturn: STUN/TURN
 - Redis: Manages users
 - Nginx: Allows Openvidu Server to utilize HTTPS port
 - Video Conference App: Video Chat Application

We then move on to set up the .env file within the openvidu folder.
```bash
cd ./openvidu
vim .env
```
Once you open the .env file, you'll be greeted with several options that require allotment. As aforementioned in the previous post: the options that require attention are: 
- DOMAIN_OR_PUBLIC_IP
- OPENVIDU_SECRET
- CERTIFICATE_TYPE
- LETSENCRYPT_EMAIL
- HTTPS_PORT

For the first option, you should just assign the domain name or the public IP address of your server, as simple as that. OPENVIDU_SECRET, too, is simple; you should regard it as a password for you OpenVidu admin account. Now, CERTIFICATE_TYPE is the tricky one. This attributes the certificate that OpenVidu is going to utilize. Which certificate you say? It's the SSL certificate which enables the website to establish encrypted connection. This is important because OpenVidu transmits/receives visual and audio stream, and in order to do that it must utilize HTTPS's secure protocol, which requires SSL certification. By default, it should be assigned to something like: "self-signed", but this cannot be maintained, because if you use self-signed certificate, while you can connect to the OpenVidu server, a glaring red page will first pop up saying that the connection is private, and also association with the WAS and web server is hampered, which is a MAJOR setback. 
![ssl_error](https://github.com/govltjsdnd24/govltjsdnd24.github.io/assets/38126462/4fd5390e-a9f3-4ebf-93d3-263bc01e7be5)

So, what must we do?  We must set the CERTIFICATE_TYPE to letsencrypt and attribute appropriate email address in the LETSENCRYPT_EMAIL option. Anddd... we could go on about the detail of letsencrypt, but it would be too overwhelming to fit in one page, so I'll continue on the next article. Before we finish, if you are curious about what HTTPS_PORT is, it's just used to define which port OpenVidu server will use; by default it's set as 443, which is the standard port for HTTPS.

## Conclusion 
Gosh... it was just plainly too much information to fit in one article, so I'll pass it on to the next post. I'm really sorry that I keep deferring the important part to later date, but there's just so many things I want to mention in the process; every bit of information is essential for the deployment of the program! They say that "the journey is the destination", right? Let's take things one at a time, and slowly move on towards our goal. I promise I'll finish this topic on the next post. 

## Reference
[https://docs.openvidu.io/en/stable/tutorials/openvidu-vue/](https://docs.openvidu.io/en/stable/tutorials/openvidu-vue/)



