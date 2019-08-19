# spring-reactive-webflux



### MONO
A Mono is a specialized Publisher that emits at most one item and then optionally terminates with an onComplete signal or an onError signal. In short, it returns 0 or 1 element.

           Mono<String> just = Mono.just("foo");

![Alt Text](https://i0.wp.com/blog.knoldus.com/wp-content/uploads/2019/05/mono.png?w=903&ssl=1)

### FLUX
A Flux is a standard Publisher representing an asynchronous sequence of 0 to N emitted items

               Flux<String> just = Flux.just("1", "2", "3");
     
![Alt Text](https://i1.wp.com/blog.knoldus.com/wp-content/uploads/2019/05/flux.png?w=833&ssl=1 )

### Backpressure in WebFlux

In order to understand how Backpressure works in the current implementation of the WebFlux framework, we have to recap the transport layer used by default here. As we may remember, the normal communication between browser and server (server to server communication usually the same as well) is done through the TCP connection. WebFlux also uses that transport for communication between a client and the server. Then, in order to get the meaning of the backpressure control term, we have to recap what backpressure means from the Reactive Streams specification perspective.

The basic semantics define how the transmission of stream elements is regulated through back-pressure.

So, from that statement, we may conclude that in Reactive Streams the backpressure is a mechanism that regulates the demand through the transmission (notification) of how many elements recipient can consume; And here we have a tricky point. The TCP has a bytes abstraction rather than logical elements abstraction. What we usually want by saying backpressure control is the control of the number of logical elements sent/received to/from the network. Even though the TCP has its own flow control (see the meaning here and animation there) this flow control is still for bytes rather than for logical elements.

In the current implementation of the WebFlux module, the backpressure is regulated by the transport flow control, but it does not expose the real demand of the recipient. In order to finally see the interaction flow, please see the following diagram:

![Alt Text](https://i.stack.imgur.com/cJIEk.png )


For simplicity, the above diagram shows the communication between two microservices where the left one sends streams of data, and the right one consumes that stream. The following numbered list provides a brief explanation of that diagram:

This is the WebFlux framework that takes proper care for conversion of logical elements to bytes and back and transferring/receiving them to/from the TCP (network).
This is a starting of long-running processing of the element which requests for next elements once the job is completed.
Here, while there is no demand from the business logic, the WebFlux enqueue bytes that come from the network without their acknowledgment (there is no demand from the business logic).
Because of the nature of TCP flow control, the Service A may still send data to the network.
As we may notice from the diagram above, the demand exposed by the recipient is different from the demand of the sender (demand here in logical elements). It means that the demand of both is isolated and works only for WebFlux <-> Business logic (Service) interaction and exposes less the backpressure for Service A <-> Service B interaction.

All that means that the backpressure control is not that fair in WebFlux as we expect.



- https://stackoverflow.com/questions/52244808/backpressure-mechanism-in-spring-web-flux\
- https://stackoverflow.com/questions/47240836/reason-for-using-reactive-programming-in-simple-cases
- https://stackoverflow.com/questions/55773465/how-to-implement-back-pressure-for-a-reactive-network-library
- https://stackoverflow.com/questions/46787315/reactive-pull-based-backpressure-using-reactive-streams
- https://stackoverflow.com/questions/1216380/what-is-a-stream
- https://softwareengineering.stackexchange.com/questions/352873/what-are-reactive-streams-and-whats-so-special-in-them

------------------------


- https://dzone.com/articles/reactive-programming-with-spring-webflux
- https://dzone.com/articles/spring-reactive-programming-in-java


## Run it with...
```
mvn test
