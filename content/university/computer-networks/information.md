---
title: Information flow
type: docs
sidebar:
  open: true
prev: basis
---

### How information transferred
When you send information over a network - let's say you are sending email to a friend - it doesn't
travel as one big chunk of data. Instead, it gets broken down into smaller pieces called packets.
Think of it like sending a long letter that is too big for one envelope - you might split it into several smaller
envelopes - you might split it into several smaller envelopes, each carrying part of the message.

Each packet contains not just message, but also important information about where it came from and where 
it is going, much like how an envelope has both a sender's and recipient's address. This addressing information helps the packet find
its way through the network.

Now, here is where protocols become really interesting. Different protocols works together in layers, each handling
a specific job. This layered approach is similar to how a postal service works:
1. At the highest level (called the Application Layer), protocols handle specific applications - like email, web browsing, or file sharing. When you write an email. An email protocol formats your message properly
2. The next layer (Transport layer) is like the postal service's packaging department. It breaks your message into those smaller packets we talked about and makes sure they all arrive correctly. There are two main approaches:
   1. TCP: This is like sending registered mail - it ensures everything arrives correctly and in order
   2. UDP: This is more like regular mail - faster but without guarantees
3. Below that (Network layer), protocols handle addressing and routing - like the postal workers figuring out the best route for you mail to reach its destination
4. At the bottom (Link Layer), protocols deal with actual physical transmission - like the trucks and planes that carry mail

What is fascinating is how these layers work together. When you send that email, your message travels down through these layers
on your computer, with each layer adding it own information (like wrapping a gift in multiple layers, of packaging). 
Then it travels across the network, and up through the same layers on your friend's computer, unwrapping each layer until they receive your original message.

### Multiplexing
Think about watching TV or listening to the radio. Have you ever wondered how multiple channels can reach your device 
simultaneously through the air. This is where multiplexing comes in. There are two main traditional approaches:
Frequency division multiplexing (FDM) and Time division multiplexing (TDM).

#### Frequency division multiplexing (FDM)
Imagine a highway with multiple lanes. Each lane represents a different frequency band, and different signals 
travel on different lanes without interfering with each other. This is exactly how radio stations work - each station broadcasts on its own frequency
For example, one radio station might broadcast at 88.5 MHz, while another uses 96.5 MHz. They don't interfere with each other
because they are using different "lanes" in the frequency spectrum.

##### Time division multiplexing
Now imagine a single - lane road where cars take turns using the road based on a strict schedule. TDM works similarly - instead of diving by frequency, 
it divides time into slots. Each user gets their own time slot to transmit data. Think of it like a conversation in a meeting where each person
is given a specific time to speak. While one person is speaking (or one device in transmitting), others wait for their turn.

The main difference between these approaches is:
- FDM lets everyone communicate at the same time using different frequencies
- TDM lets everyone use the same frequency but at different times

A real-world example might help: In older mobile phone systems, FDM was used to allow multiple phone calls
simultaneously. Each conversation was assigned its own frequency band. Modern digital systems often use combinations 
of both FDM and TDM to maximize efficiency