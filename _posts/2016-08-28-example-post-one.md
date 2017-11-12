---
title: Demystifying Microservices
category: Java/Spring Technology
feature_image: "https://unsplash.it/1200/400?image=200"
---

If we have spent a decent amount of time in the Information Technology industry, one thing is sure to cross our path multiple times, and that is jargons/short abbreviated forms of complex concepts. The Microservices movement is not an exception. Coupled with Cloud migration and Containerization it continues to amaze (and sometimes overwhelm) us. However, if concepts are to be adequately understood, we must relate to them using our existing knowledge. To understand what is genuinely new, we must clearly understand what is not. Whenever some new concept is introduced to us as the unique and novel piece of technology, we must apply our common sense, to reveal the truth from the "completely new" perception. This can be done by looking at the new technology through our current knowledge and skills as well as the standard English word meanings. This current knowledge could come from our existing capabilities. They could even come from daily life experiences outside work. Thus, before, we master these skills in Microservices conceptualization, design, development, deployment, and operations; we must simplify them. Following is an attempt to simplify some of the Spring Cloud Microservice design paradigms to some extent.


<!-- more -->

Microservices Still are services.If you have developed REST services in Java / .NET / Ruby etc. a lot of that knowledge will still be useful. The development model changes a little, and the deployment model varies a lot.

 **What does not change**

**1**. Still, Microservices are REST APIs having the same request/response model.

**2.** Earlier we used to deploy 20 different services together in a single app. In Microservices, we deploy each one separately. 

**3.** The dependency management mechanism is same between Monolithic application and Microservices, i.e., Maven / Gradle. In other words, the way Monolithic applications and Microservices leverage someone else’s work, i.e., third-party libraries, is same.

**4.** Same build/deploy / continuous integration tools can be used to deploy monolithic applications and microservices.

**5.** Same IDEs, same compilers, same code repositories, same third-party libraries (some new) and the same developers. A lot of things won’t change. 

**Service Discovery Eureka**

**1.** We do it all the time in our daily lives. Even the ones among us that do not know a thing about Microservices does use service discovery.

**2.** Think of using Google a centralized service registry of services (legal/restaurants/food distribution/laundry/hair salons/malls / entertainment centers and what not).

**3.** These services come up, open shop/website online, Google finds them through web crawling and indexes them in its centralized registry.
	
**4.** When we search the google web client, Google searches its index in the service registry and returns the result to us.
	
**5.** This model of service discovery is pull based. Google web crawler pulls location data from the websites of the services.

**6.** The Microservices Service discovery is same. The only difference is that it is push based. Let me explain.

**7.** There is a central Microservice Service Registry Cluster. More than one Service Discovery Microservices are running in the cluster. More than one instances are run to provide High Availability.

**8.** Other Microservices, when they come up, push their location information using a logical name, to the Service Discovery cluster.
	
**9.** In a non-Microservice world, clients have the IP of the service they are calling and call them directly. If the service is down, the client is impacted as well.

**10.** Each Microservice has a logical name with which it registers with the Service Discovery cluster.

**11.** Several instances of the product search service, for example, will have the same logical name. Naturally, when several services register with the same logical name, the service discovery will have many items, i.e., a Set, against one logical name.

**12.** Service instances are required to send health checks every few seconds, and if not, they are considered not healthy by the Service egistry.

**13.** In a Microservices service discovery scenario, clients first call the Service Discovery cluster with the same logical name of the service, to retrieve a healthy set of service contact information IPs / port, etc.

**14.** The Service discovery returns a set of robust instances, and client calls one of the instances.

**15.** Multiple running instances eliminate the single point of failure and make services and their clients loosely coupled.

**Configuration Service**

**1.** Properties such as database URL password queue/topic name etc. are stored in Git repository and follow the same development workflow 1. code 2. commit to local 3. push to remote.

**2.** There is configuration service cluster that serves the properties to Microservice clients. The configuration is another Microservice.

**3.** When Microservice comes up, they are configured to ask properties from the configuration service using their logical name.

**4.** The configuration service returns the properties.
	
**5.** The Microservice starts up.
 
**Intelligent Proxy ZuuL**

**1.** All Front End clients call the intelligent proxy microservice which in turn call others.

**2.** Designed to prevent massive CORS configuration for a verity of Microservices deployment for Web / Mobile clients.
	
**3.** Other functions that the intelligent proxy can perform are
	
**4.** Security using OAuth2
	
**5.** API Service Security using Jason Web Token(JWT)
 
**Circuit Breaker Hystrix**

**1.** Suppose, a person has a regular daily commute from his/her home to the train station, which we can say from Point A to Point B.
	
**2.**  If there is a roadblock on certain days, on the road from Point A to Point B, we take an alternate route from Point A to Point C and from Point C to Point B.
	
**3.** Circuit Breaker is doing the same thing for Microservices.
	
**4.** If service A calls service B and service B is slow for some reason, a circuit breaker annotated method in Service A that calls service B will be told to either stop before calling or find a fallback method, preventing the failure from moving up the calling chain up to the user.
	
**5.**  The idea is to make services self-resilient and loosely coupled.
 
**Declarative Client Feign**

**1.**  Feign makes it easy to call another service without writing code. Think of AngularJS Resource plugin.
	
**2.**  The developer provides the logical name of the service to be called,  the API endpoint and Declarative Client Feign makes the call.
 
**Client Side Load Balancing Ribbon**

**1.**  The client receives many service endpoints from Service Discovery Registry.

**2.**  Ribbon calls one of the least loaded APIs.

 **Centralized Tracing Zipkin**

**1.** Wires logs from the various Microservices calling each other into a logical call trace to aid better troubleshooting. 

