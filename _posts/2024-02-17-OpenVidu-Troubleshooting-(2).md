---
categories: [ Development, OpenVidu ]
tags: [ webrtc ] 
---
It took me some time in order to return to this topic. Not only because I was organizing the steps I took into a presentable format. I did say that I would immediately return to the topic, but alas, t'was a time of transition--a period of wrapping up the former project and initiating a new one--and with the influx of workload piling in front of me, I couldn't return to the topic that I was planning on finishing last post. Nonetheless, here I am, and now, I would like to talk about SSL certificates and how to apply them to our project.
## SSL Certificate
You know the difference between HTTP and HTTPS, right? In HTTPS, requests and respsonses are encrypted and require a digital signature. TLS and SSL are the protocols responsible for the encryption of requests and responses, and digital signatures are required for the SSL and TLS certificates.

The how do these SSL/TLS certificates really work? Upon initial connection between the server and the client, the client tries to verify the Certificate Authorities (CA) that issued the SSL/TLS certificate. If it is in fact legitimate, then secure connection can be made between them. In Openvidu, this certificate is utilized to prove the authenticity of the server for the transmission of audio and video requires a reliable and secured connection.


## Troubleshooting


## Conclusion 


## Reference
[https://docs.openvidu.io/en/stable/tutorials/openvidu-vue/](https://docs.openvidu.io/en/stable/tutorials/openvidu-vue/)



