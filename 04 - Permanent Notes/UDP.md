---
tags:
  - Network
---
User Datagram Protocol (UDP) is one of the communication protocols for devices to send/receives messages through the network.

UDP does not require prior communication to set up communication paths, which may lead to security issues. Because UDP does not need handshaking, there is no guarantee of delivery as well, making it unreliable compared to the likes of [[TCP]], but some services still use UDP, such as DHCP.

Below is the UDP format:
![[udp-packet-3856695253.png |600]]
Checksum is calculated by using what's called a Pseudo Header, and the structure differs depending on which [[Internet Protocol]] is being used. for example, if run over IPv4, the pseudo header looks like the following:
![[스크린샷 2024-05-03 174541.png|600]]


## References

Created: 2024-05-03