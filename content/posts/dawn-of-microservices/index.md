---
title: "Dawn of microservices"
draft: false
date: 2016-02-22T09:16:45.000Z
description: "Learn the basics of Microservices architecture, including what it is, why it's beneficial for web applications, and how to design and implement it effectively with considerations and potential challenges."
categories:
  - Tech
tags:
  - Tech
  - Microservices
---

Nowadays, when you start building a web application, you have dozens of architecture decisions to make. Moreover, industry is now moving towards a new architectural pattern – Microservices. This post will give you a basic overview on Microservices. In a nutshell, answering the what, why, and how of microservices.

**What is a Microservice ?**

A microservice is an independent loosely-coupled unit of code, that can be run to serve a single purpose. Often, it is built to serve single feature of a bigger monolithic application. These microservices, then function together to serve the complete application functionality. They can be heterogeneous services communicating via a protocol like HTTP. A lot of us would relate microservices to SOA, but they’ve their own differences. Service-oriented Architecture (SOA) allows communication between different applications via APIs. Microservices also has the same pattern with one major difference – Microservices own their databases. A traditional monolithic or a SOA application will have one centralized, preferably relational, database. If we divide our application into 10 microservices, then each service will have its own micro database. Frequently NoSql but also MySQL.

**Why Microservices ?**

You might wonder, why on earth would you want to setup such a loosely-coupled system. Its because, it now allows us to separate responsibilities and enabling greater maintenance. It also helps with horizontal scaling. Instantly we now have an open-mind to choose different technology stacks for different services. For instance, one could easily setup an Authentication service using MySQL database based on LAMP Stack. At the same time, a complex profiling system can be set up using the MEAN (Mongo, Ember, Angular, Nodejs) Stack. Though a word of caution, if an effort is not made to follow the best practices for designing such a system, you’ll find yourself lost in the dark world. A world full of error-prone race conditions, payload contracts and communication failures.

**How do I setup a Microservices Architecture ?**

Now, that’s the most important question where most of the developers fail to answer. We tend to make each microservice as a mini-monolithic application. This is allowed to an extent but not at the cost of an architectural flaw.

I’d like to explain the how using a real-life example. Let’s assume that we are building a Restaurant Food Ordering Application. Our first task is to identify different microservices.

{{< img
src="use-case-restaurant-app.png"
alt="Use case restaurant app"
style="margin: 0 auto;"
caption="Basic Use-case for Food Ordering App" >}}

Considering the above use case diagram, a possible decomposition of the system could be:

{{< img
src="microservices-breakdown.png"
alt="Microservices Breakdown"
align="center"
caption="Microservices Breakdown of the Food Ordering Application" >}}

Each functional area of the application is now implemented by its own microservice. This makes it easier to deploy distinct experiences for specific users, devices, or specialized use cases. This also makes a lot of our code resuable. Because our services are system agnostic, we can now reuse them as is with little to no change in the implementation. For instance, the same payment processing or push notification system can be added to another web application.

**Considerations to design**

1. Each service communicates with each other via REST. In Microservices, the services may or may not be on the same server. For that reason, we use REST or Socket communication between the services.

2. Each service serves a single purpose of the use-case. For instance, our order management will only deal with create, update, cancel and track order. It won’t handle anything related to Billing, Invoicing or Payment processing.

3. Each service owns its database. All the microservices have their own databases. All the joins performed on the data are done at the application level. All the data is referenced usually via a global unique identifier.

4. Client never connects to the Microservices directly. We usually setup a front-end Web app for the client to interact with. This webapp handles sending requests to microservices setup via proxies. Moreover, it also consolidates responses from different services and sends it to the Client UI. In an enterprise application, we also use API Gateway. I will try to write a separate post for the addons required in a microservices framework.

5. Each microservice may or may not run on the same server. Apart from that, we can run many instances of a single microservice. This allows us to scale the application horizontally, with less efforts.

**The other side of the story:**

If microservices is so brilliant, shouldn’t we all move to microservices? The answer is ‘No’. Each architecture has its pros and cons. Microservices has its own share of limitations.

1. Too much of anything is good for nothing. I have seen developers fine graining microservices to the extreme level. This increases the complexity of the application and also affecting its performance. Microservices advocates building single usable service that covers a feature in the application. It shouldn’t be 2 controllers interacting with 1 model in the database.

2. The fact that microservices is distributed in nature, imposes a lot of complexity in the structure. Race conditions, partial failures, communication failures have to be tested thoroughly for fault tolerance.

3. Testing a microservices-based application is much more complex task. Already the features were killing you, that they added inter-process communication, load balancing, service availability, proxy securities.

4. Deployment of microservices can also turn into a nightmare. Especially if you host them on a single server. At my workplace, we have 21 microservices (still a smaller number). With monolithic application, all you had to do was install once and image the deploy. But now you have to deploy 21 services and test them thoroughly with all the sanity checks. You can tackle the deployment problems using Continuous Integration and hosting services in Containers.

I’d like to sum up the post with basic word of advice. Microservices pattern is an amazing architecture as long as it is designed and implemented using best practices. Whether or not to use microservices depends on a lot of factors such as product, tech, support, business, etc.
