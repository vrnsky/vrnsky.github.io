---
title: Tutorial 2
type: docs
sidebar:
  open: true
prev: tutorial-1
math: true
---

## Network Layer

### Question 1
Consider the following network. With the indicated link costs, use Dijkstra’s shortestpath algorithm to compute the shortest path from x to all network nodes. Show how the
algorithm works in a table. 

### Answer
With indicated link costs, use Dijkstra's shortest path algorithgm to all compute the shortest path from x to all network nodes.



### Question 2
Consider the network shown below, and assume that each node initially knows the costs
of each of its neighbors. Consider the distance-vector algorithm and show the distance
table entries at node z.

### Answer


### Question 3
Consider the network shown below. Suppose, RIP is used for intra-AS protocol, and
BGP is used for inter-AS protocol. Initially suppose there is no physical link between
AS2 and AS4.

a. Router 3c learns about prefix x from which routing protocol?

b. Router 3a learns about prefix x from which routing protocol?

c. Router 1c learns about prefix x from which routing protocol?

d. Router 1d learns about prefix x from which routing protocol?
### Answer

BGP - Border gateway protocol, i - internal, e - external

a. eBGP
b. iBGP
c. eGCP
d. iBGP


### Question 4
Referring to the previous problem, once router 1d learns about x it will put an entry (x,I)
in its forwarding table.

a. Will $I$ be equal to $I_1$ or $I_2$ for this entry? Explain why in one sentence. (2 marks)

b. Now suppose that there is a physical link between AS2 and AS4, shown by the
dotted line. Suppose router 1d learns that x is accessible via AS2 as well as via
AS3. Will I be set to I1 or I2? Explain why in one sentence. (2 marks)

c. Now suppose that there is another AS, called AS5, which lies on the path
between AS2 and AS4 (not shown in diagram). Suppose router 1d learns that x
is accessible via AS2 AS5 AS


### Answer

a. $L_1$ becuase it begin the least cost route from $L_d$ to $L_c$.

b. $L_2$ because both routes have similar AS-PATH length, and $L_2$ begins
the route that hast the cosst NEXT-HOP route.

c. $L_1$ because it begins the route with the shortest AS-PATH.

##  Link layer

### Question 1
Suppose the information content of a packet is the bit pattern as shown below, and an
even parity scheme is being used. What would the value of the field containing the parity
bits be for the case of a two-dimensional parity scheme?

| 1 | 1 | 1 | 0 |
|---|---|---|---|
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 0 | 1 |

### Answer

### Question 2
Consider the following two-dimensional even parity matrix
| 0 | 0 | 0 | 0 |
|---|---|---|---|
| 1 | 1 | 1 | 1 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 1 | 0 |