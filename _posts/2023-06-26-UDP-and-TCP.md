---
layout: post
title: A Look at TCP & UDP
subtitle: A Deep Dive Into The 2 Most Common Transport Protocols
tags: [tcp, udp, networking, transport]
---
Transmission Control Protocol (TCP) and User Datagram Protocol (UDP)

Both TCP and UDP are protocols in layer 4 (transport layer) of the OSI reference model. They both serve more or less the same purpose - transport data. However, both protocols accomplish that in different ways. The main differentiation is that TCP, or the Transmission Control Protocol is a connection-oriented protocol meaning that it establishes a connection, making it reliable, but slow for data transfer. UDP, or the User Datagram Protocol on the other hand is a connectionless protocol, meaning that it does not establish a connection, making it unreliable, but faster for data transfer.

TCP - connection-oriented. Reliable, but slow.
<br>
UDP - connectionless. Unreliable, but fast.

# Transmission Control Protocol
TCP, as mentioned above, is a connection-oriented protocol. Therefore, it establishes a connection before any data exchange can occur. 
A TCP connection is established through the TCP three-way handshake, a three step connection intiation process, which we will look at shortly.
<br><br>
Before we dwelve too deepp into the nitty gritty details of the three-way handshake, let's look at the TCP header.
The TCP header consists of 11 fields, that I will break down below.
- **Source port**: this is a 16 bit field that specifies the port number of the sender.
- **Destination port**: this is a 16 bit field that specifies the port number of the receiver.
- **Sequence & Acknowledgment** Numbers: The sequence number is a 32-bit integer that the client uses to keep track of the data that it has sent. This sequence number is included on each transmitted packet, and acknowledged by the opposite host as an acknowledgement number to inform the sending host that the data was received successfully. This is what makes TCP reliable. When a connection is first established, the sequence number is set to a random integer, which can be between 0 and 4,294,967,295. Protocol/packet inspection, or sniffing tools like wireshark will often use a relative sequence number of 0 for simplicity. 
- **DO**: this is the 4 bit data offset field, also known as the header length. It indicates the length of the TCP header so that we know where the actual data begins.
- **RSV**: these are 3 bits for the reserved field. They are unused and are always set to 0.
- **Window**: the 16 bit window field specifies how many bytes the receiver is willing to receive. It is used so the receiver can tell the sender that it would like to receive more data than what it is currently receiving. It does so by specifying the number of bytes beyond the sequence number in the acknowledgment field.
- **Checksum**: 16 bits are used for a checksum to check if the TCP header is OK or not.
- **Urgent pointer**: these 16 bits are used when the URG bit has been set, the urgent pointer is used to indicate where the urgent data ends.
- **Options**: this field is optional and can be anywhere between 0 and 320 bits.
- **Flags**: there are 9 bits for flags, more commonly called control bits. TCP uses flags to indicate a particular state of connection, or to provide additional information.

Throughout the connection TCP uses flags to indicate a particular state of connection, or to provide additional information.

There are many different TCP flags, but the most common ones are SYN, ACK, RST and FIN.

- **SYN** (Synchronise) - The SYN flag synchronises sequence numbers to initiate a TCP connection. The syn flag will (should) only ever be seen during the three-way handshake. 
- **ACK** (Acknowledgment) - This flag is used to acknowledge any packets that are successfully received by the recipient, which can either be the server or client.
- **RST** (Reset) - This flag is used to completely tear down the connection instantly. This flag is mostly used with something unexpected happens. For example, if you send an ACK packet to a random server that you have not established a connection with, you will likely receive an RST from the server.
- **FIN** (Finish) - This flag is used to request connection termination. Unlike RST, FIN doesn’t immediately terminate the connection. You can think of it as a graceful/polite way of closing a connection.
