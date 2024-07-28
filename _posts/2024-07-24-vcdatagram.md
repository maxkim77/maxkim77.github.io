---
layout: single
title:  "[CS] Understanding the Role of the Network Layer and Virtual Circuits&Datagram"
categories: CS
tag: [CS, Knowledge, Quiz, Network, VirtualCircuits, Datagram]
toc: true
---


![CSQuiz]({{site.urls}}/assets/images/2024-07-11-CSQuiz1/quiz.png)


# Understanding the Role of the Network Layer and Virtual Circuits & Datagram


### Quiz Question

**Question:**
Which of the following statements accurately describes the difference between virtual circuit networks and datagram networks?

A. Virtual circuit networks do not require a call setup before data transmission, whereas datagram networks require a call setup.

B. Datagram networks guarantee sequential delivery and minimum bandwidth, whereas virtual circuit networks do not provide these guarantees.

C. Virtual circuit networks require a call setup and teardown process, and involve cooperation between routers and hosts, whereas datagram networks treat each packet independently and do not require a setup process.

D. In virtual circuit networks, each packet is routed independently with no fixed path, whereas in datagram networks, a fixed path is established for the duration of the connection.

**Answer:**
C. Virtual circuit networks require a call setup and teardown process, and involve cooperation between routers and hosts, whereas datagram networks treat each packet independently and do not require a setup process.

### Explanation:
- **Option A** is incorrect because it reverses the requirements for call setup between virtual circuit and datagram networks.
- **Option B** is incorrect because datagram networks do not guarantee sequential delivery or minimum bandwidth; these are characteristics that can be provided by virtual circuit networks.
- **Option D** is incorrect because it reverses the routing method of virtual circuit and datagram networks.
- **Option C** is correct as it accurately describes the fundamental differences between virtual circuit networks and datagram networks.


## Understanding the Role of the Network Layer and Virtual Circuits

The network layer's primary role is to deliver transport layer segments from the sending host to the receiving host. This layer is crucial in ensuring that data travels from one host to another efficiently and accurately.

## Network Layer Functions

### Sending and Receiving Data

On the sending side, the network layer encapsulates transport layer segments into datagrams by adding headers and then passes them down to the data link layer. On the receiving side, it receives these datagrams, removes the headers, and delivers the segments to the transport layer.

### Presence in Hosts and Routers

Network layer protocols are not only present in hosts but also in routers, which play a pivotal role in routing and forwarding data across networks.

### Basic Functions: Routing and Forwarding

1. **Routing**: This involves determining the path that data packets should take to reach their destination. It is the process of path calculation for each destination.
2. **Forwarding**: When a packet arrives at an input port, forwarding determines which output port the packet should be sent to next.

### Interplay Between Routing and Forwarding

Routers use routing algorithms to compute the routes to all destinations and store this information in a forwarding table. This table maps header values to output ports, ensuring efficient data packet forwarding.

## Network Service Models

When discussing network service models, it's essential to consider whether we're dealing with individual datagrams or a flow of datagrams. 

## Datagrams
![Datagram]({{site.urls}}/assets/images/2024-07-24-vcdatagram/1.png)

- **Guaranteed Delivery**: Ensures that each datagram is delivered.
- **Guaranteed Delivery Time**: Ensures delivery within a specified time frame (e.g., 40 milliseconds).

### Flow of Datagrams

- **Sequential Delivery**: Ensures datagrams arrive in the order they were sent.
- **Minimal Bandwidth Guarantee**: Ensures a minimum transmission capacity.
- **Bounded Delay**: Limits the variation in packet delivery times.

## Virtual Circuit and Datagram Networks

Packet switching can be categorized into virtual circuit and datagram networks.

### Datagram Networks

- **Connectionless Service**: Each packet is treated independently, and no setup is required before sending data.

### Virtual Circuit Networks

- **Connection-Oriented Service**: Requires a call setup before data transmission. It is similar to the concept of connections in the transport layer but involves cooperation between all routers and hosts within the network core. 

### Comparison with Transport Layer

- **Transport Layer (TCP/UDP)**: Operates end-to-end between hosts (process-to-process communication).
- **Network Layer**: Operates from host to host, involving all routers along the path.

## Virtual Circuits
![Virtual Circuits]({{site.urls}}/assets/images/2024-07-24-vcdatagram/2.png)

### Call Setup and Teardown

Before data is transmitted, a call setup phase is required to establish the path and resources. Similarly, a teardown phase is required to terminate the connection.

### Virtual Circuit Implementation

A virtual circuit comprises:

1. **Path Information**: From source to destination.
2. **VC Numbers**: Virtual Circuit numbers for each link.
3. **Forwarding Table Entries**: Information on which output port to use for each VC.

### Forwarding Example

When a datagram is sent from the source to node 1, node 1 will use VC1 for subsequent transmissions to the same destination. Each intermediate node (e.g., nodes 2, 3) and the final destination will follow a similar process, using specific VC numbers for each link.

### VC Signaling Protocols

Virtual circuits require signaling protocols for setup, maintenance, and teardown (e.g., ATM, X.25, Frame Relay). While the internet today does not commonly use virtual circuits, these protocols are crucial in certain applications.

## Data Forwarding in Datagram Networks

In contrast to virtual circuits, datagram networks do not require call setup. Packets are simply pushed into the network. Forwarding tables in datagram networks do not store destination-specific information due to the vast number of possible destinations (e.g., billions in IPv4). Instead, they use hierarchical addressing to manage forwarding more efficiently.

### Example: Hierarchical Addressing

Consider traveling from A to B. You follow general signs towards B, and as you get closer, you see more specific signs guiding you to your exact destination. Similarly, network routers use hierarchical addressing to forward packets more efficiently.

## Datagram or VC Networks: Why?

The internet uses datagram networks, whereas ATM uses virtual circuit networks. Simplifying the network core allows for faster packet transmission by reducing processing overhead. Intelligent endpoints (computers) can handle complex tasks, while simpler endpoints (like telephones) benefit from the guaranteed services of virtual circuit networks.


Understanding the role of the network layer and the distinction between virtual circuit and datagram networks is crucial for grasping how modern networks operate. Whether it's ensuring efficient packet forwarding or setting up reliable virtual circuits, the network layer plays a fundamental role in the seamless operation of communication systems.
