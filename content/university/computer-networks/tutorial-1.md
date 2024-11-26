---
title: Tutorial 1
type: docs
sidebar:
  open: true
prev: transport-layer
math: true
---

## Chapter 1 - Computer networks and the internet
### Question 1
Compare and contrast packet switching and circuit switching.

#### Answer
**Packet switching** and circuit switching represent two fundamentally
different approaches to data transmission in networks.
In packet switching, as used in the Internet data is 
broken into smaller packets that can travel independently through
the network. These packets share network resources with other users' data,
making efficient use of available capacity.When I send an email,
for example, the message might be split into several
packets, each finding its own path to the destination.

**Circuit switching**, on other hand, establishes a dedicated path
between sender and receiver before any data transfer begins - much like
traditional telephone calls. This path remains reserved for the entire
duration of the communication, whether data is being transmitted
or not. Think of it as having private highway lane reserved just for you,
even if you are not using it continuously.

The key differences manifest in several ways. **Packet switching** tends to be
more efficient for bursty data traffic, as resources are only used when needed.
However, this can lead to variable delay and possible packet loss during **congestion**.
**Circuit switching** provides guaranteed quality once a connection is established
but can be less efficient since resources remain allocated 
even during silent periods.

From a cost perspective, packet switching generally proves more
economical for data networks because it allows statistical multiplexing - essentially
sharing resource among many users. Circuit switching, while
more expensive due to dedicate resource allocation, excels
in applications requiring constant data rates and minimal 
delay variation, like traditional voice calls.

### Question 2
Do you agree that a traffic intensity of greater than 0.8
indicates congestion? Explain your answer.

#### Answer
No, I wouldn't necessarily agree that a traffic intensity above 0.8
automatically indicates congestion. While it is true
that 0.8 is often used as a warning threshold in network planning.

### Question 3
This elementary problem begins to explore propagation delay and
transmission delay, two central concepts in data networking. Consider two hosts, $A$ and $B$, 
connected by a single lik of rate $R$ bps. Suppose that the two hosts are
separated by $m$ meters, and suppose the propagation
speed along the link is $s$ meters/sec. Host A is to send a packet of size $L$
bits to Host $B$

#### Question 3a
Express the propagation delay, $d_{drop}$, in terms of $L$ and $R$

##### Answer 
The propagation delay $d_{prop}$ is time taken for a bit to travel from
source to destination over a distance $m$ at propagation speed $s$.
Therefore,
$$
d_{prop} = \frac{m}{s}
$$

#### Question 3b
Determine the transmission time of packet, $d_{trans}$, in terms of $L$ and $R$

##### Answer
The transmission time $d_{trans}$ is the time needed to push all $L$ bits
of the packet into the link at rate $R$ bits per seconds.
Therefore,
$$
d_{trans} = \frac{L}{R}
$$

#### Question 3c
Ignoring processing and queuing delays, obtain an
expression for the end-to-end delay.

##### Answer
The total end-to-end delay is simply the sum of propagation delay
and transmission time $d_{total} = d_{prop} + d_{trans} = \frac{m}{s} + \frac{L}{R}$

#### Question 3d
Suppose Host $A$ begins to transmit the packet at time $t = 0$. 
At time $t=d_{trans}$, where is the last bit of the packet?

##### Answer
At the time $t = d_{trans}$, the last bit has just been transmitted
and is at the beginning of the link at Host $A$'s end. It hasn't
started its propagation journey yet.

#### Question 3e
Suppose $d_{prop}$ is greater than $d_{prop}$. At time $t = d_{trans}$,
where is the first bit of the packet

#### Answer
When $d_{prop} > d_{trans}$, the first bit is still traveling along
the link and hasn't reached Host $B$ yet. The exact position would be at ($s \cdot d_{trans}$) meters
from the source.

#### Question 3f
Suppose $d_{prop}$ is less than $d_{trans}$. At the time $t = d_{trans}$, where
is first bit of the packet?

#### Answer
When $d_{prop} < d_{trans}$, at the time $t = d_{trans}$, the first bit has
already arrived at the Host $B$, while the last bit is just begging its journey
from Host $A$

#### Question 3g
Suppose $s = 2.5 \cdot 10^{8}, L = 120 \: bits,\:and\:R = 56\:kbps$. Find the distance
$m$ so that $d_{prop}$ equals $d_{trans}$.

#### Answer
Since we want $d_{prop} = d_{trans}$, we can write $\frac{m}{s} = \frac{L}{R}$.
Solving for $m$:
$$
m = \frac{(s \cdot L)}{R}
$$
Substitute values:
$$
m = \frac{2.5 \cdot 10^{8} \cdot 120}{56 \cdot 10^{3}} = \text{535714.285714 meters or 536 km}
$$

### Question 4
Suppose that there a ${M}$ client-server pairs. Denote $R_s, R_c$ and $R$ for the rates of the
server links, client links, and network link. Assume all other links have abundant
capacity and that there is no other traffic in the network
besides the traffic generated by $M$ client-server pairs. Derive general expression
for throughput in terms of $R_c, R_c$ 

#### Answer
The key here is to understand that bottleneck could occur at three different points:
1. The server's upload link ($R_s$)
2. The client's download link ($R_c$)
3. The network link that all traffic must share $\frac{R}{M}$ since ${M}$ pairs share it

The throughput will be limited by the minimum of three rates
$\min({R_s},{R_c},{\frac{R}{M}})$
This is because:
- Each server can upload at rate $R_s$
- Each client can download at rate $R_c$
- The network link with capacity $R$ must be share among $M$ pairs, so each pair gets $\frac{R}{M}$


### Question 5
Suppose two host, $A$ and $B$, are separated by 20 000 kilometers and connected by a direct
link of $R = 2\:Mbps$. Suppose, the propagation speed over link is $2.5 \cdot 10^{8}$ meters/sec

#### Question 5a
Calculate the bandwidth-delay product, ${R \cdot d{prop}}$

##### Answer
First, let's calculate $d_{prop}$
$$
d_{prop} = \frac{distance}{speed}
$$
therefore
$$
d_{prop} = \frac{20\,000\,000}{2.5 \cdot 10^{8}} = \text{0.08 seconds}
$$