---
title: Building Streaming API with gRPC
type: blog
sidebar:
  open: true
date: 2025-02-21
comments: true
---

In this article, I'll guide you through implementing streaming APIs using gRPC in Java.
We'll look at various types of streaming. Then, we'll create a practical example to show real-time flow.

### Introduction
Many developers know about traditional request-response APIs. Yet, modern apps often need real-time
data streaming. gRPC provides powerful streaming capabilities that can transform how your services communicate.
Whether you're making chat apps, real-time analytics, or IoT systems, knowing gRPC streaming is key.
Let's create a weather monitoring service. It will stream temperature updates to clients.

### Types of gRPC streaming
Before we start coding, let's understand the three types of streaming gRPC offers:
Server streaming: the server sends multiple responses to a single client request.
Client streaming: the client sends many messages to the server.
Bidirectional streaming: both the server and multiple messages at the same time.

We'll use server streaming for our weather monitoring service. This method suits our needs well.
The client sends one request to start monitoring. Then, the server provides continuous temperature updates.

### Access full article
{{< cards cols="3" >}}
{{< card icon="medium" title="Medium" subtitle="Follow & read" link="https://vrnsky.medium.com/building-streaming-api-with-grpc-94f4a745ab8f" >}}
{{< card icon="substack" title="Substack" subtitle="Subscribe & read" link="https://open.substack.com/pub/vrnsky/p/building-streaming-api-with-grpc?r=3ypfws&utm_campaign=post&utm_medium=web&showWelcomeOnShare=true"  >}}
{{< card icon="paper-airplane" title="Ghost" subtitle="Subscribe & read" link="https://vrnsky.ghost.io/building-streaming-api-with-grpc/"  >}}
{{< /cards >}}
