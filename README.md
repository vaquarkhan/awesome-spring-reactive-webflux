# spring-reactive-webflux



### MONO
A Mono is a specialized Publisher that emits at most one item and then optionally terminates with an onComplete signal or an onError signal. In short, it returns 0 or 1 element.

           Mono<String> just = Mono.just("foo");

![Alt Text](https://i0.wp.com/blog.knoldus.com/wp-content/uploads/2019/05/mono.png?w=903&ssl=1)

### FLUX
A Flux is a standard Publisher representing an asynchronous sequence of 0 to N emitted items

               Flux<String> just = Flux.just("1", "2", "3");
     
![Alt Text](https://i1.wp.com/blog.knoldus.com/wp-content/uploads/2019/05/flux.png?w=833&ssl=1 )


------------------------


- https://dzone.com/articles/reactive-programming-with-spring-webflux
- https://dzone.com/articles/spring-reactive-programming-in-java


## Run it with...
```
mvn test

********************************************************************************
     __  ___       __                           _____
    / / / (_)___ _/ /_ _      ______ ___  __   / ___/___  ______   _____  _____
   / /_/ / / __ `/ __ \ | /| / / __ `/ / / /   \__ \/ _ \/ ___/ | / / _ \/ ___/
  / __  / / /_/ / / / / |/ |/ / /_/ / /_/ /   ___/ /  __/ /   | |/ /  __/ /
 /_/ /_/_/\__, /_/ /_/|__/|__/\__,_/\__, /   /____/\___/_/    |___/\___/_/
         /____/                    /____/

********************************************************************************

```

https://ualterazambuja.com/2018/04/22/reactive-programming-with-spring-webflux/
