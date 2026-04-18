Open System Interconnection (OSI) model, the standard of computer network

## L7 Application Layer
L7 directly interacts with the data (i.e. regulate the format, usage and so on) from user. e.g. user request content & network return content **in required format**

L7 protocols examples: HTTP, SMTP
## L6 Presentation Layer
L6 is responsible for translation, encryption and compression of data before delivering to L5 and L7 (i.e. minimize the amount of data transferring, and increase the security)
## L5 Session Layer
L5 manages the communication to ensure the session stays open long enough for all data exchanging, and close on time to avoid wasting. Sometimes checkpoint will be used to ensure synchronizing and resuming (in other cases L7 will do check).

L5 does not need to know the exactly data length (in this case, L5 closes session when there is no data coming in).

The time between open and close the communication is **session**.
## L4 Transport Layer
L4 takes data from L5, breaks it up into segments (sender side) AND reassembles those segments into data for L5 to use (receiver side).

L4 handles flow control (keep sending speed close to receiving speed) and error control (ensure complete data and request retransmission for uncomplete data)

L4 does not in charge of all data (i.e. user send a 100mb file), instead this file will split into different part in L7 (for resuming download purpose), L4 only manages this small part.

L4 Protocols examples: TCP, UDP
## L3 Network Layer
L3 takes segments from L4 and encapsulates into packets (sender side) AND reassembles those into segments (receiver side).

L3 also finds the best **physical** path for data reaching, such path searching process is **routing**

L3 Protocols examples: IP, IPsec, Internet Control Message Protocol
Physical device: Router
## L2 Data Link Layer
L2 does similar things as L4 and L3, but in the LAN(local area network). It takes packets, then break and encapsulates into frames. 
L2 is also responsible for flow control and error control.

Physical device: Switch
## L1 Physical Layer
Data gets converted into a bit stream in this Layer

Physical device: Cable