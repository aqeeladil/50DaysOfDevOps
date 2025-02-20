## Asterisk Basics

1. SIP Routing:
o How can you configure Asterisk to route calls between multiple SIP trunks in 
sip.conf?
o What is the role of the context parameter in sip.conf, and how does it affect call 
routing?

2. Dial Plan Creation:
o How do you create a basic dial plan in extensions.conf that directs incoming calls 
from a SIP trunk to a set of internal extensions?
o How do you implement pattern matching in the dial plan to handle multiple phone 
numbers?
o How can you design a dial plan to support both internal calls and outbound calls to 
the PSTN via a SIP trunk?

3. Peer Creation:
o What are the steps to create a SIP peer in sip.conf for internal extensions and 
external SIP trunk connections?
o What is the difference between friend, peer, and user in Asterisk’s SIP 
configuration, and when should each be used?
o How do you configure a secure SIP peer that uses TLS and SRTP for encrypted 
signaling and media

4. SIP Connection Troubleshooting:
o How would you troubleshoot SIP registration issues, such as a peer failing to 
register with Asterisk?
o What could cause one-way audio during SIP calls, and how can you resolve it?
o How do you handle SIP NAT traversal issues, especially when Asterisk is behind a 
NAT?

5. SIP Debugging and Monitoring:
o How can you use sip set debug on and sip show peers to monitor and troubleshoot 
SIP traffic?
o How do you debug SIP 403 Forbidden errors when a peer tries to make a call?
o What role does the qualify parameter play in peer monitoring, and how does it affect 
SIP connection health



