---
tags:
  - Network
---
## Overview

TCP Congestion Control is an algorithm used to minimize network congestion and packet loss. Both congestion control and flow control serves the same purpose, but whereas the Flow control is managed in per client-server level, congestion control acts on the network level, which means it serves to minimize packet loss of all send requests sent by client within the network.
![[tcp-congestion-control1-n.jpg|500]]

## Congestion Policy
Congestion Policy in TCP is divided into 3 parts
- Slow Start Phase
- Congestion Avoidance Phase
- Congestion Detection Phase
### Slow Start
As the name suggests, TCP packets are initially sent slow (the window size is small), then it **exponentially** gets faster (window size doubles) until a certain the first **packet loss** occurs. A threshold, called _ssthreshold_ (slow start threshold) is set.

### Congestion Avoidance
Unlike slow start, where the growth in window size is exponential, congestion avoidance is linear. This continuous increase in window size stops when a packet loss event happens.

### Congestion Detection
There are two types of packet loss:
- Triple duplicate ACK
- Timeout
Triple duplicate is indicative of a congestion, however it is not as severe as a timeout. Therefore, different measures must be taken.
1) Triple Duplicate: cut the congestion window size in half. set this window size as the new ssthreshold value. Fast Retransmit and Fast Recovery states are used to reduce waiting time for senders to retransmit lost packet, and to keep the loss of "network flow" as low as possible.

2) Timeout: Set the congestion window size back to 1, and start the Slow start phase again. Slow start phase will stop at the current ssthreshold value.

### Fast Retransmit and Fast Recovery
when three duplicate ACKs are received, the sender assumes packet loss has occured, and instead of waiting for timeout it will resend the lost packet (the octet starting with the sequence number received in ACK). This is called fast retransmit.

Fast recovery is the way in which congestion window gets increased after fast retransmit occurs. despite the name, the growth in cwnd is not exponential. Rather, it is linear, just like congestion avoidance. Indeed, Fast Retransmit and Fast Recovery is considered to happen during the Congestion Avoidance phase. Congestion Detection quite literally means the detection of congestion, and is not an actual "phase".

![[tcpcongestion-1502814677.jpg]]

While the overall mechanism of congestion control is universal, there are several algorithms to optimize bandwidth/minimize packet loss, etc. Examples include Reno, Vegas, CUBIC, etc.

## References
https://www.slideserve.com/eden-best/tcp-tutorial-part-ii
https://courses.washington.edu/ee565/handouts/TCP_Fast_Retransmit_and_Recovery.pdf

Created: 2024-05-07