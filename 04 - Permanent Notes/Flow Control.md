---
tags:
  - "#Network"
---
### Flow Control 

When Data that exceeds the size of a normal packet is used, it must be split into multiple packets. Then whoever's on the receiving end must know the proper sequence of packets. This is where the Sequence number, ACK and FIN flags are used. 

TCP also needs to assure no packets are lost, and that the receiver gets only a manageable amount of data at any given time. To make all of this happen, TCP must do what's called a flow control.
![[tcp-flow-control-l-608786602.jpg]]
The crux of Flow control is the fact that the sender **CANNOT** send any packets unless they receive ACK from the receiver. Receiver also sends the window info of its buffer to the sender so that they know which data octets to send, and how much.

The basic flow is as follows. Suppose the buffer size for receiver is 2500.
1) The client advertises its window size to be 2500.

2) sender receives this info, and sequentially sends data octets up to 2500. whenever a packet is successfully received, client will send ACK with updated window size.

3) once the client's window size reaches zero, in other words once the client's buffer is full, it will send another ACK packet with window size set to 0. The sender **Halts** sending data octets until further ACK is received.

4) Client will start processing the data and free up buffer space. Once a certain size is reached, it will send an ACK with the updated window size. The sequence number will be the **starting octet** of the new "batch" of data. The client in this example now needs data octets 2501 and onwards. Therefore, the sequence number will be 2501, and because the window size is 2000, the sender will send octets 2501 ~ 4501.

5) This process is repeated until it reaches the end of data transmission. TCP connection termination will commence.

---
Categories: [[Computer Network]]
References:
https://www.slideserve.com/aglaia/transport-layer-tcp-and-udp
https://www.youtube.com/watch?v=4l2_BCr-bhw

Created: 2024-05-07