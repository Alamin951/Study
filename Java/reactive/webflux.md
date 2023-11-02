# WebFlux
A non-blocking web stack to handle concurrency with a small number of threads and scale with fewer hardware resources. It is a functional programming. 

The tern "reactive" refers to programming models that are build around reacting to change, non-blocking.

Reactor is a reactive library of choice for spring WebFlux. It provided the Mono and Flux API types to work on data sequences of 0..1 (MONO) and 0..N (Flux) through a rich set of operators aligned with ReactiveX.  Reactor is a reactive stream library.

### Programming models
The spring-web module contains the reactive foundation that underlies Spring WebFlux, including HTTP abstractions, Reactive Streams adapters for supported servers, codecs and core WebHandler API comparable to the Servlet API but with non-blocking contracts.

Spring WebFlux provides a choice of two programming models:
- **Annotated Controllers:** 
- **WebFlux-fn:** Lambda based lightweight and functional programming model. Its a small library or set of utilities that an application can use to route and handle requests. The big difference with annotated controllers is that the application is in charge of request handling from start to finish versus declaring intent through annotations and being called back.

## Applicability

Spring MVC and Spring WebFlux works together to expand the available options. Designed for continuity and consistency with each other. 

![MVC-VS-WebFlux](../../images/spring-mvc-and-webflux-venn.png)


### ***Important Points***
- If MCV application works fine then there is no need to change to webFlux
- Provides a choice of servers (Netty, Tomcat, Jetty, Undertow, and Servlet containers), a choice of programming models (annotated controllers and functional web endpoints), and a choice of reactive libraries (Reactor, RxJava, or other).
- If use persistence APIs ( JPA, JDBC) or networking APIs then Spring MVC is the best choice. 
- If we need to make remote service call then better to use reactive webClint. 

### Servers
Spring WebFlux is supported on Tomcat, Jetty, Servlet containers, non-Servlet container like Netty and Undertow. 

Spring WebFlux does not have build in support doe starting or stopping a server. 

	It is strongly advised not to map Servlet filters or directly manipulate the Servlet API in the context of a WebFlux application. For the reasons listed above, mixing blocking I/O and non-blocking I/O in the same context will cause runtime issues.

### Concurrency Model
Both The Spring MVC and Spring WebFlux supports @Controllers but the main difference is the concurrency of model and the default assumptions dor blocking and threads.

In Spring MVC, It is assumed that thee applications can block the current thread. Fot this reason servlet containers have great thread pool to absorb potential  blocking on request handling.

In Spring WebFlux its assumed that applications do not block. Therefore, non-
