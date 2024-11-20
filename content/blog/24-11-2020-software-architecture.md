---
title: Software architecture
type: blog
sidebar:
  open: true
date: 2020-11-24
---

Introduction
In this article I will try to explain what is architecture, clean architecture, architector role in project

Examples of web architecture application
![Software architecture](software-architecture-1.png)
Let’s consider an example of a service with one architectural level (Single Tier)

In an application with one architectural level, the user interface, business logic, that is, the backend part of the application and the database are on the same server
![Software Architecture 2](software-architecture-2.png)
An example of an application with one architectural level are applications such as MS Office, GIMP

### Benefits of using a single-layer architecture

1. Very little or no delay in the interaction of components due to the fact that the components are located on the same server
2. Although it largely depends on the machine’s power and software hardware requirements, to measure the real performance of a single-tier application
3. In addition, the user’s data remains on his machine and does not need to be transferred over the network. This ensures data security at the highest level. Client data cannot be intercepted, since data exchange will occur within the same server

### Disadvantages of this architecture
1. The impossibility of changing the code or functions after delivery to the production server. For example, in the 90s, if the game was shipped with an erroneous code, the studios could do nothing
2. Code in peer-to-peer applications is also vulnerable to rework and reversal. Business security is minimal, because in the case of reverse engineering, an attacker or competitor can gain access to your codebase, which can lead to financial losses. Example — your application works with finances, attackers have exposed part of your system’s code and can now bypass some of your checks and thus use your application for fraud

### Access full article
{{< cards >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://medium.com/@vrnsky/software-architecture-7a3630d66f0d">}}
{{< /cards >}}