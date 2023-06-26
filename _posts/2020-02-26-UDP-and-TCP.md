---
layout: post
title: A Look at TCP & UDP
subtitle: a deep dive into two transport layer protocols
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [tcp, udp, networking, transport]
---
Transmission Control Protocol (TCP) and User Datagram Protocol (UDP)

Both TCP and UDP are protocols in layer 4 (transport layer) of the OSI reference model. They both serve more or less the same purpose - transport data. However, both protocols accomplish that in different ways. The main differentiation is that TCP, or the Transmission Control Protocol is a connection-oriented protocol meaning that it establishes a connection, making it reliable, but slow for data transfer. UDP, or the User Datagram Protocol on the other hand is a connectionless protocol, meaning that it does not establish a connection, making it unreliable, but faster for data transfer.

TCP - connection-oriented. Reliable, but slow.
UDP - connectionless. Unreliable, but fast.

# Transmission Control Protocol
