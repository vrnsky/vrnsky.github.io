---
title: Spring Cloud Config, Spring Cloud Bus & Kafka - How to set up automatic updates of your configuration
type: blog
sidebar:
  open: true
date: 2023-12-21
comments: true
---

### Introduction
In this article, I will show you how to achieve automatic updates with Spring Cloud Bus and Kafka

The Spring Cloud Bus, according to documentation:

> Spring Cloud Bus links nodes of a distributed system with a lightweight message broker.
> This can then broadcast state changes (e.g., configuration changes) or other management instructions.
> AMQP and Kafka broker implementations are included in the project.
> Alternatively, any [Spring Cloud Stream](https://spring.io/projects/spring-cloud-stream) binder on the classpath will work out of the box as a transport.

I will start from common practice nowadays without a message broker.

First, we need to create a repository with your app’s configuration. There is no rocket science to create a new repository.
After that, we can edit with web IDE, clone, add, commit, and push the app’s configuration to the remote repository.

### Start building
```yaml {filename="application.yml"}
echo:
  message:
    text: 'Hello, World!'
```

The second part is to create a cloud config server and set up the correct configuration for this server.
We must set up a remote repository and credentials to make the configuration accessible.

### Access full article
{{< cards cols="2" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/spring-cloud-config-spring-cloud-bus-kafka-how-to-set-up-automatic-updates-of-your-96999930bc2b" >}}
{{< /cards >}}

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/J3J416GZA5)

### Status Hub
Status Hub is simple uptime monitoring for your business. Start your free trial today!
Have a question? We are ready to answer!
{{< cards cols="2" >}}
{{< card link="https://statushub.app?utm_source=https://vrnsky.dev&utm_medium=blog" title="Start your 2 weeks free trial" icon="beaker" subtitle="No credit card required" >}}
{{< card link="mailto:support@statushub.app" title="Have a question?" icon="mail" subtitle="Ask us" >}}
{{< /cards >}}
