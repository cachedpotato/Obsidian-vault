---
tags:
  - Network
---
Dynamic Host Configuration Protocol (DHCP) is a service that automatically assigns IP addresses to devices hooked up to a network.

Devices need IP address to access the outside world. However, upon initial boot, they do not have any IP address. There are two ways of doing thigs: 1) assign IP address manually, or 2) Let DHCP do it automatically. DHCP is almost always the preferred method as it not only assigns IP address, it also **takes back** IP addresses from disconnected devices so that others can use it.

DHCP takes 4 steps:
- DHCPDiscover (Client > Server)
- DHCPOffer (Server > Client)
- DHCPRequest (Client > Server)
- DHCPAck (as in "ack"nowledge)(Server > Client)

Here's how the DHCP Packet Format looks like:
![[스크린샷 2024-05-03 171050.png|500]]
OP: Operation Code - 1 if sent by client, 2 if sent by server
HTYPE: Hardware Type. As in the Ethernet
YOUR IP ADDRESS: Clients IP address given by server

Note that DHCP packets and offers are sent in [[UDP]], with clients using port 68 and servers using port 67.

Some things of note:
- During the Discover phase, the client will send the packet with source IP 0.0.0.0, and destination to 255.255.255.255. The destination address is what's called the broadcast IP address.
- All packets regarding DHCP will have the destination set to the broadcast IP address. This is to let other routers know which IP is being offered and being taken.
- IPs are **LEASED**, not given - the client needs to renew its lease if they want to keep using it.


## References
https://www.youtube.com/watch?v=WztEbO0uiiQ
https://www.youtube.com/watch?v=e6-TaH5bkjo

Categories: [[Computer Network]]
Created: 2024-05-03