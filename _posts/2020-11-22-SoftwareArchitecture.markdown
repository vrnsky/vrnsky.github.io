---
title: Software Architecture
published: true
description: In this article describe some software architecture
tags: programming, architecture, software, java
//cover_image: 
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/rpm5oszc1weogwc7o2d9.jpg)

Introduction
In this article, I will try to explain what architecture and clean architecture is, and architecture's role in projects.

Examples of web architecture application
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/tulofphvlpo28ngrfrao.jpeg)

Let's consider an example of a service with one architectural level (Single Tier)

In an application with one architectural level, the user interface, business logic, that is, the backend part of the application and the database are on the same server

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/gw5b65ldm2s3j020vfwk.jpeg)

An example of an application with one architectural level are applications such as MS Office, GIMP

Benefits of using a single-layer architecture

1. Very little or no delay in the interaction of components due to the fact that the components are located on the same server
2. Although it largely depends on the machine's power and software hardware requirements, to measure the real performance of a single-tier application
3. In addition, the user's data remains on his machine and does not need to be transferred over the network. This ensures data security at the highest level. Client data cannot be intercepted, since data exchange will occur within the same server

Disadvantages of this architecture

1. The impossibility of changing the code or functions after delivery to the production server. For example, in the 90s, if the game was shipped with an erroneous code, the studios could do nothing
2. Code in peer-to-peer applications is also vulnerable to rework and reversal. Business security is minimal, because in the case of reverse engineering, an attacker or competitor can gain access to your codebase, which can lead to financial losses. Example - your application works with finances, attackers have exposed part of your system's code and can now bypass some of your checks and thus use your application for fraud

### Two-tier architecture
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/g6gnaiojx8vyxbf0r2qw.jpg)

A two-tier application includes a client and a server. The client will contain the user interface and business logic on the same machine. And the server will be a backend application deployed on another computer.

There are times when you need to use a two-tier architecture, such as to-do list applications.

### Three-tier architecture

Three-tier architecture is quite popular and often used. Most simple websites like blogs, news sites use this architecture

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/uhz1m7br2iejbido1y5e.jpg)

Let's consider an example of a simple blog - the client interface will be written using HTML, JavaScript, CSS and the backend application will be launched on a server, for example Apache, and the backend part will use the PostgreSQL database as storage

### N-tier architecture

This term is used to describe an architecture that uses more than three components. Examples of these components

- Cache - an example of this technology JCache, Caffeine. This technology is used for the following things - 1. Reduce the response time from the application without requesting any data in the database, 2. Also save some responses from third-party systems, since this can take a very long time
- Message broker - examples are Apache Kafka, RabbitMQ. This tool is necessary to save any messages, a message can mean some kind of request to a third-party system, for example, in Kafka you can store messages that will have to be sent to the tax system or the fiscal data operator
- Load balancer - examples are Nginx, Ribbon, Eureka. This tool is required to distribute the load on the application. Imagine the following situation - you have a distributed application, which means there are several instances or nodes, and in order to optimize the speed for the end user, all requests go through the balancer, which chooses a less loaded instance / node
- Search services - to search for information in huge amounts of data
- Components responsible for processing data arrays
- Components using heterogeneous technologies, commonly known as web services

All modern social applications - Instagram, Facebook and scalable services like Uber, Airbnb, as well as games with a huge number of players like Pokemon Go, for example, use an N-tier architecture


### Clean architecture
The center of your application is not the database. An architecture is also not one or more frameworks that you can use. The center of your app is the use cases for your app. The center of the application is the functionality for which the business gets paid, that is, what problem / what value does your application bring to the business - this place is the center of the application

Clean architecture is a set of practices, techniques, design patterns that enable you to create an extensible and reliable application. Designed to prevent the following problems that may arise:

- Decisions are made very quickly - hasty decisions can lead to problems when the application is on the production server
- Difficult to make changes
- Stuck on a certain framework - one day an organization / person may decide that he / she does not have the strength to support this framework. Accordingly, you should not be strongly tied to the framework
- Focusing only on technical aspects - it is important to understand that when developing, you should focus not only on technical aspects, but also on what business value the development of new functionality will bring
- It's hard to find the right places in the project
- Business logic is scattered throughout the code - if some requirements change, the programmer will have to find all the places in the code and change the functionality in each place. If the business logic is isolated in one place, then the programmer only needs to change the code in one place
- Lack of tests
- Infrequent updates
Clean architecture also provides the following benefits when used
- Effective testing strategy
- Code for using frameworks is isolated
- Database independence
- All business logic is contained in the application use cases
- Hard to do wrong
- The application is always ready for output to the production
 environment

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ex7iwwba2ocgd2y3hcvq.png)
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ex7iwwba2ocgd2y3hcvq.png)

Let's analyze these figures in more detail:

The core of the application is:

- Entities representing the domain area or subject area. Subject area for payment gateway application - Internet finance
- At this level is the code that is applicable to the entire object as a whole (for example, checking the format of the hostname)
- Java Plain Objects: no frameworks or annotations required

Core:

- Represents the business actions of your application - this is what your application can do.
- Pure business logic, Java code without using any frameworks, but using utilitarian libraries such as Apache Commons
- Defines the interfaces for the data that are needed to apply the logic. One or more data providers implement the interface, but in case of use it is not known where the data is coming from
- At this level, business exceptions are thrown - exceptions that are directly related to the application domain

Data providers (dataproviders):

- Receiving and storing data from multiple sources of information (database, network devices, file system, etc.)

Application entrypoints:

- This application layer describes the way to interact with the application and usually includes a delivery mechanism (for example, REST API, scheduled tasks, GUI, other systems)
- Launching a use case and converting the result into a format that matches the delivery mechanism

Configuration

- Connects all components together
- Dependency Injection is isolated here
- Contain "dirty details" - such as Main class, web server configuration, database configuration, etc.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/imzgb7rlhtu01z1u78zh.png)
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/imzgb7rlhtu01z1u78zh.png)

# Architectural Application Templates

An architectural pattern is a repetitive and generic solution to a problem arising from an application architecture problem within a given context.

Let's take a look at 10 popular architectural patterns

- Multilevel
- Client - server
- Leading - slave
- Channels and filters
- Mediator template
- Peer-to-peer template
- Event bus
- Model - View - Controller
- Board
- Interpreter

### Multilevel

It is used to structure programs that can be decomposed into groups of certain subtasks located at certain levels of abstraction. Each layer provides services for the next higher layer.

Most often, there are 4 layers in common information systems:

- Presentation layer (also known as user interface layer)
- Application layer (also known as service layer)
- Business logic layer (also known as domain layer)
- Data access layer (also known as data storage layer)

### **Usage**

* Common desktop applications.

* Web applications e-commerce.

### Client - Server

This template consists of two parts: server and many clients . The server component provides services to the client components. Clients request services from the server, and it, in turn, provides these very services to clients. Moreover, the server continues to "eavesdrop" on client requests.

### **Usage**

Online applications (email, document sharing, banking).

### Master - Slave

This pattern also involves two participants - master and slaves. The Leader distributes tasks to identical Followers and calculates the final result based on the results received from its "Subordinates".

### **Usage**

* In database replication. There, the main database is considered an authoritative source, and the subordinate databases are synchronized with it.

* Peripheral devices connected to the bus in the computer (master and slave devices).

### Channels and Filters

This pattern is suitable for systems that generate and process data streams. Each processing step takes place inside a filter component. Data for processing is transmitted via channels. These channels can be used to buffer or synchronize data.

### **Usage**

* Compilers. Sequential filters perform lexical, parsing, semantic analysis, and code generation.

* Workflows in bioinformatics.

### Mediator template

This pattern is needed to structure distributed systems with disconnected components. These components can communicate with each other through a remote service call. The mediator component is responsible for coordinating the interaction of components.

The server hosts its capabilities (services and characteristics) with an intermediary (broker). The client requests a service from the broker. The broker then redirects the client to the appropriate service from its registry.

### **Usage**

· Message brokers by type [Apache ActiveMQ] (https://en.wikipedia.org/wiki/Apache_ActiveMQ), [Apache Kafka] (https://en.wikipedia.org/wiki/Apache_Kafka),  [RabbitMQ] (https://en.wikipedia.org/wiki/RabbitMQ) and [JBoss Messaging] (https://en.wikipedia.org/wiki/JBoss_Messaging).

### Peer-to-peer template

There are separate components in this template, the so-called  peers. Peers can act as a client requesting services from other peers (peers), and a server providing services to other peers. A peer can be a client or a server, or all at once, and can dynamically change its role over time.

### **Usage**

*  File sharing networks (Gnutella and G2)

* Multimedia Protocols (P2PTV and PDTP)

* Proprietary multimedia applications (Spotify)

### Event Bus

This template mainly interacts with events and has 4 main components: event source, event listener, channel and event bus. Sources place messages for specific channels on the event bus. Listeners subscribe to specific channels. Listeners are notified of the appearance of messages posted on channels from their subscription.

### **Usage**

Android development

Notification services

### Model - View - Controller

This pattern is also known as the MVC pattern. It divides interactive applications into 3 parts:

1. model - contains key data and functionality;

2. view - shows information to the user (more than one view can be specified);

3. controller - deals with the processing of data from the user.

This is done in order to differentiate the internal presentation of information from the way it is presented and received from the user. This design isolates components and allows for efficient code reuse.

### **Usage**

* Architecture of WWW-applications written in the main programming languages.

* Web frameworks (for example, Django and Rails)

### Board

This pattern is suitable for problems for which there are no clear deterministic solutions. The Board template has 3 main components:

* board is a structured global memory containing objects from the space of possible solutions;

* source of knowledge - specialized modules with their own presentation;

* control components - selects, configures and executes modules.

All components have access to the board. Components can produce new data objects that are added to the board. Components look for specific kinds of data on the board. One way to search is to match patterns against an existing source of knowledge.

### **Usage**

* speech recognition;

* Identification and tracking of vehicles;

* Determination of protein structures;

* Interpretation of signals Sonar.

### Interpreter

It is suitable for developing a component that must interpret programs written in a special programming language. Basically, it describes how to evaluate strings (in other words: "sentences" or "expressions") written in some particular programming language. The point is to assign a class to each character in the language.

## **Usage**

* Languages ​​of queries to the database (SQL);

* Languages ​​that are used to describe data transfer protocols.

# **Comparison of architectural patterns**

Below are the pros and cons of each of the architectural patterns.

### **Layered Template**

**Pros:**

- One low layer can be used by different layers of a higher rank.
- Layers make standardization easier because we clearly define the levels.
- Changes are made within one layer, while the other layers remain unchanged.

**Cons:**

- Not universal.
- In some situations it is possible to skip some layers.

### **Client / Server Template**

**Pros:**

- A set of services that clients can request is suitable for modeling.

**Cons:**

- Requests are usually executed in separate threads on the server.
- Interaction between processes increases resource consumption, because different clients have different views.

### **Master-Follower Template**

**Pros:**

- Accuracy, because service execution is delegated to different slaves with different implementations.

**Cons:**

- All slaves are isolated, they have no general condition.
- The waiting period in the master-slave communication is a significant disadvantage. For example, in real time systems.
- Suitable only for those problems whose solution can be decomposed into parts.

### **Template "Channels and Filters"**

**Pros:**

- They can implement parallel processes, when input and output consist of streams, and filters begin calculations after receiving data.
- Simple addition of filters. The system can be easily expanded.
- Filters are suitable for reuse. They can build different pipelines, creating all kinds of combinations of the existing set of filters.

**Cons:**

- The efficiency is reduced by the slowest filtration processes. When moving from one filter to another, data transformation is performed, which leads to increased resource consumption.

### **Mediator Template**

**Pros:**

- It is possible to dynamically change, add, delete and move objects. This pattern makes the distribution process transparent to the developer.

**Cons:**

- Need to standardize service descriptions.

### **Peer-to-Peer Template**

**Pros:**

- Supports decentralized computing. Extremely resilient to failures at any node.
- High scalability in terms of resource and computing power.

**Cons:**

- There is no guarantee of the quality of services; nodes cooperate spontaneously.
- It is difficult to guarantee security.
- Performance depends on the number of nodes.

### **Event Bus Template**

**Pros:**

- Easily add new subscribers, publishers and connections. Works well for highly distributed applications.

**Cons:**

- Problem with scalability, because all messages go through one event bus.

### **Model-View-Controller Template**

**Pros:**

- Facilitates the creation of different representations of the same model; they can be enabled or disabled at run time.

**Cons:**

- The complexity of the algorithm increases. Can lead to many unnecessary adjustments to user actions.

### **Board Template**

**Pros:**

- Easy adding of new applications.
- You can easily expand the data space structures.

**Cons:**

- Editing data structures is really difficult because such changes affect all applications.
- Synchronization and access control may be required.

### **Template "Interpreter"**

**Pros:**

- Highly dynamic behavior possible.
- An excellent solution for end users in terms of programming convenience.

**Cons:**

- Performance problems as an interpreted language is slower than a compiled one.
