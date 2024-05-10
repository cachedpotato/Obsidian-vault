Transmission Control Protocol (TCP) is one of the main protocols of the Internet protocol suite. It is often called TCP/IP because of its close connection to internet protocol. Unlike UDP which doesn't have innate error handling (checking if the packets have been received properly), TCP is reliable in that it provides ordered and error checked delivery. To establish connection, TCP must do what's called a 3-way handshake.
### TCP Segment Header
![[스크린샷 2024-05-07 094845.png]]
TCP Header is more sophisticated than the UDP header, as it needs more information to establish a reliable connection.
- Sequence Number: This is where the SYN value is set.
- Acknowledgement Number: This is used if ACK bit is set.

TCP headers also contains flags besides SYN and ACK:
- CWR: **Congestion Window Reduced**. Indicates TCP segment received with ECE flag set and responded in Congestion Control Mechanism.
- ECE: if SYN bit is set, the TCP peer is ECN capable. if not, it means a normal packet with Congestion Experience flag set has been received.
- URG: Urgent. If set, the information in Urgent Pointer field is used.
- ACK
- PSH: Push. Push the buffered data to receiving application.
- RST: Reset Connection.
- SYN
- FIN: Last Packet from Sender.

### Three Way Handshake
the three way handshake is split into three parts:
- SYN
- SYN-ACK
- ACK
![450](https://media.geeksforgeeks.org/wp-content/uploads/TCP-connection-1.png)
1) SYN: The client sends a SYN (Sync) request to the server. Within the packet a SYN sequence is set, which is then used to check connection status once it received SYN-ACK.

2) SYN-ACK: Server sends a TCP packet back to the client, this time with ACK bits set to the SYN value sent by the client +1. If it does not match with the SYN value, this means the ACK packet was either erroneously given or it's from a different connection request. a new SYN value is also set by the server, but it will be completely different from the one sent by the client.
 
3) ACK: Once the Client receives the packet from the server and it's checked, client then sends a packet to the server with ACK bit set to the SYN bit sent by server +1. After the server receives the ACK package, a reliable connection is set.

To make packet exchanges as reliable as possible, TCP/IP does what's called a [[Flow Control]] and [[Congestion Control]]. Flow control limits/manages the amount of data sent by the sender using buffer size and window size, ACK, etc. and congestion control is used to minimize packet loss and network congestion.

### TCP connection termination
Once transmission is complete TCP connection is terminated. the termination process is similar to the likes of TCP handshake used to initialize the connection.
![[EN-tcp-verbindungsabbau-4054690810 1.png]]
The only difference is that FIN flag is set instead of SYN.