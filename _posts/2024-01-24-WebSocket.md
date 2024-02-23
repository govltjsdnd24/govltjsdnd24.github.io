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
Within the folder you will be able to see two folders: one, an already complete version and two, a barebone model. The tutorial directs us to start with the initial folder, so let's go start over there.
You can begin by using Spring Initializer or just use the content of the initial folder, but I knew how to use the Initializer already so chose the latter. If you are curious what a Spring Initializer is, it's just a tool used to initialize your Spring project with all the necessary dependencies and settings already configured for you.

Initializer image

Now, before you move on, you should check you Java version, and make sure they are in accord with the version set in the project. I had JDK 21 and this caused the version mismatch error because the one configured in the project was 17. 

Anyways, now that's past us, we must create a Resource Representation Class. STOMP messages are in a JSON format, and with the use of Jackson JSON library, Spring can turn JSON into objects, if corresponding objects are found, that is. We come up with two classes: one for the name, and one for the content. Remember that using Lombok for getter, setter, and the constructor will be able to shorten the code.
For a short instruction on the implementation of Lombok (on IntelliJ). First, you add dependencies for Lombok.

Lombok Image 1

Then, enable annotation processing.

Lombok Image 2

Below is the example of a STOMP message for name:
```JSON
{
    "name": "Fred"
}
```
Of a representation class:
```Java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class HelloMessage {
    private String name;
}
```

And of a controller:
```Java
@Controller
public class GreetingController {
    @MessageMapping("/hello")
    @SendTo("/topic/greetings")
    public Greeting greeting(HelloMessage message) throws Exception {
        Thread.sleep(1000);
        return new Greeting("Welcome, " + HtmlUtils.htmlEscape(message.getName()));
    }
}
```
The controller receives messages sent to the <i>/hello</i> topic, turns the JSON message into an object, and propates the data to <i>/topic/greetings</i>.  

The last component of Back-end is configuration file. 
```Java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {
    @Override
    public void configureMessageBroker(MessageBrokerRegistry config) {
        config.enableSimpleBroker("/topic");
        config.setApplicationDestinationPrefixes("/app");
    }
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/gs-guide-websocket");
    }
}
```
As you can see from the annotation, this configuration enables WebSocket brokers. Other than that, greeting messages are routed to <i>/topic</i> and messages to @MessageMapping will start with <i>/app</i>.

That's it for the Back-end composition. In the tutorial, we use static website for the client side. An html file and javascript file are provided in the tutorial, but I won't cover the former because there's nothing special about it.

The javascript file is as followed:

```Javascript
const stompClient = new StompJs.Client({
    brokerURL: 'ws://localhost:8080/gs-guide-websocket'
});

stompClient.onConnect = (frame) => {
    setConnected(true);
    console.log('Connected: ' + frame);
    stompClient.subscribe('/topic/greetings', (greeting) => {
        showGreeting(JSON.parse(greeting.body).content);
    });
};

stompClient.onWebSocketError = (error) => {
    console.error('Error with websocket', error);
};

stompClient.onStompError = (frame) => {
    console.error('Broker reported error: ' + frame.headers['message']);
    console.error('Additional details: ' + frame.body);
};

function setConnected(connected) {
    $("#connect").prop("disabled", connected);
    $("#disconnect").prop("disabled", !connected);
    if (connected) {
        $("#conversation").show();
    }
    else {
        $("#conversation").hide();
    }
    $("#greetings").html("");
}

function connect() {
    stompClient.activate();
}

function disconnect() {
    stompClient.deactivate();
    setConnected(false);
    console.log("Disconnected");
}

function sendName() {
    stompClient.publish({
        destination: "/app/hello",
        body: JSON.stringify({'name': $("#name").val()})
    });
}

function showGreeting(message) {
    $("#greetings").append("<tr><td>" + message + "</td></tr>");
}

$(function () {
    $("form").on('submit', (e) => e.preventDefault());
    $( "#connect" ).click(() => connect());
    $( "#disconnect" ).click(() => disconnect());
    $( "#send" ).click(() => sendName());
});
```

It just seems really long and daunting at first sight, but to put it simply, by using StompJS library, we initialize the StompClient with the provided brokerURL. The client is subscribed to <i>/topic/greetings</i> , and will be publishing JSON messages over to <i>/app/hello</i>. As simple as that.

This is the resulting screen you will get upon success:

success Image

## Conclusion
Today I described the process I took while trying to implement the WebSocket. It wasn't really a complicated work, so I didn't have any problem along the way. Of course, there were some minor troubleshooting involved, which have been omitted for the sake of the length of the article. I'll cover that along with the developement of the said project in the next post if possible. 

## Reference
[https://spring.io/guides/gs/messaging-stomp-websocket](https://spring.io/guides/gs/messaging-stomp-websocket)
