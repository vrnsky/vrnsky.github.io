---
title: Transport layer
type: docs
sidebar:
  open: true
next: information
math: true
---

### Transport layer
- Provide logical communication between processes running on different hosts
  - Sender host: Break message into segments
  - Destination host: Reassemble segments into message, and pass to application layer
- Rely on network layer services
  - _network layer_
    - Provide logical communication between hosts
- Two types of protocol
  - Transmission Control Protocol (TCP)
  - User Datagram Protocol (UDP)

### Reliable data transfer protocol: pipelined protocols
#### Go-back N
- Sender
  - Can send N unacknowledged packets in pipeline
- Receiver
  - Only send cumulative acknowledgment
    - This means an acknowledgment for packet n indicates all packets with sequence number up to and including n have been received correctly
    - No buffer
- Timeout
  - Sender has a single timer for oldest unacknowledged packet
  - When timer expire, retransmit all sent but unacknowledged packets
    - If window size is large
      - There can be many unacknowledged packets in pipeline, so a single packet loss can cause sender to retransmit many packets

#### Selective repeat
- Sender
  - Can send N unacknowledged packets in pipeline
- Receiver
  - Send acknowledgment for each packet
  - Has buffer
- Timeout
  - Sender has timer for each unacknowledged packet, so it has many timers
  - When timer expire, retransmit the unacknowledged packet only
    - Address the disadvantage of Go-back-N

### Go-back-N
Maintain a window with size N. A sender can send N unacknowledged packets in pipeline.
When sender receive an unacknowledged packet, it slide forward window so that a sequence number
change from not usable to usable, not yet sent. Each packet has sequence number.

##### Receiver
Always send ACK for correctly-received packet with the highest in-order sequence number.
Generate duplicate ACK when receive out-of-order packet, discard out-of-order packet because receiver
does not have a buffer

##### Re-acknowledge packet with the highest in-order sequence number
- Receiver
  - Expect to receive packet n
  - However, it receives packet n + 1. This means that packet n is lost.
  - Discard packet n + 1
  - Resend acknowledgment for packet n - 1
- Sender
  - Receive duplicated ACKs
  - Resend packet n and n + 1

### Selective repeat
#### Sender
- If there is usable, not yet sent in window, sent it
- Resend packet n, restart timer of packet n
- When sender receive an acknowledgment for send_base packet, it slide forward window so that a sequence number change from not usable to usable, not yet sent.
#### Receiver
- Send acknowledgment for packet n
- If
  - Out-of-order packet
    - Buffer the packet
  - In-order packet 
    - Deliver (also deliver buffered, in-order packets) to upper layer


### Flow control
Control a source host's sending rate so that is does not overflow receive host's buffer.
Inform sender the received window value `rwnd`
- `rwnd`
  - Unit type: `byte`
  - Indicate the buffer space availability at receiver
- Sender
  - Send packets of size < `rwnd` bytes to receiver

### TCP congestion control
- End-to-end
- Destination host infer congestion from observed packet loss and end-to-end delay
- End-to-end delay = $\frac{RTT}{2}, $ where RTT is **Round Trip Time** 
- Control a source host's sending rate so that each connection traversing a congested link get an equal share link of bandwidth
- Sender
  - Send packets of size < min { **rwnd**, **cwnd** } bytes to receiver
     - **rwnd** - is receive window
     - **cwnd** - is congestion window
  - Sending rate $ \frac{cwnd}{RTT} bytes/second $
    - This means, sender send **cwnd** bytes, wait RTT for ACK, then send more
- Two main concept
  - Slow start
  - Congestion avoidance
