# Transmission Control Protocol (TCP)

[TOC]

## Context

Transmission Control Protocol 的核心是在不可靠的IP网络层之上，为应用层提供一种可靠、有序、面向连接的字节流传输服务，解决了应用层对数据传输可靠性和有序性的核心需求，并有效地管理了网络流量和拥塞。目标就是让上层应用可以像读写本地文件流一样简单地进行网络通信，而无需关心底层网络的复杂性和不可靠性。

数据包网络.

## Problem

IP协议，其设计核心是“尽力而为”（Best-Effort Delivery）。它只负责将数据包从源主机路由到目标主机，但不保证送达、不保证顺序、不保证不重复、不保证不损坏。这对于需要可靠通信的应用（如文件传输、远程登录、电子邮件）来说是灾难性的。

网络资源有限且易拥塞： 早期的网络链路带宽低、路由器处理能力和缓存有限，非常容易发生拥塞。需要一种机制来协调众多主机共享网络资源，防止少数主机独占带宽导致网络瘫痪。当网络路径上的路由器或链路负载过重（拥塞）时，继续高速发送数据只会加剧拥塞，导致更多丢包和性能急剧下降。

- **Flow Control**: 发送方发送数据的速度可能远超过接收方处理数据的速度，导致接收方缓冲区溢出，数据丢失。
- **Packet Loss**: IP网络不保证数据包一定能送达目的地。路由器可能因拥塞而丢弃数据包，物理链路可能出错。
- **Packet Reordering**:  IP网络中的数据包可能选择不同的路径传输，导致后发送的数据包先到达接收方。
- **Packet Duplication**: 网络中的某些机制（如不恰当的ACK处理或重传）可能导致同一个数据包被多次送达接收方。

SYN泛洪攻击

TCP粘包

TCP心跳包



**Flow Control vs. Congestion Control**

| 特性         | Flow Control                                                 | Congestion Control                                           |
| :----------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **目标**     | **防止发送方淹没接收方**。确保接收方有足够的缓冲区处理到达的数据。 | **防止发送方淹没网络**。避免网络链路和路由器因过载而出现拥塞崩溃。 |
| **关注点**   | **接收端的能力** (接收缓冲区大小和处理能力)。                | **网络的承载能力** (链路带宽、路由器缓冲区等资源)。          |
| **作用域**   | **端到端** (Point-to-Point)。在单个发送方和单个接收方之间进行。 | **网络范围** (Network-Wide)。影响共享同一网络路径的*所有*数据流。 |
| **触发原因** | 接收方缓冲区即将或已经耗尽。                                 | 网络中出现数据包丢失、延迟显著增加（排队延迟）或显式拥塞通知（ECN）。 |

## Resolution

### Connection process

**Connections**: The reliability and flow control mechanisms described above require that TCPs initialize and maintain certain status information for each data stream, The combination of this information, including *sockets, sequence numbers, and window sizes*, is called a connection.

#### Connection Establishment: Three-way Handshake

*The principle reason for the three-way handshake is to prevent old duplicate connection initiations from causing confusion.* Meanwhile, the initial sequence numbers of both parties will be synchronized during the connection process, and the design of connection creation should avoid wasting resources. If a historical request initiated by A is received by B, it will be detected by A in the second step and notified to B in the third step to terminate this erroneous connection attempt. Therefore, B must wait for A’s acknowledgment to complete the connection establishment.

1. A initiates a connection request to B, carrying A's initial sequence number ($Seq=a$).
2. B responds to A's request, carrying B's initial sequence number and the sequence number of A + 1 received from A ($Seq=b, Ack=a+1$).
3. A responds to B's request and changes to the established state, carrying the received sequence number of B + 1 ($Ack=b+1$). B changes to the established state after receiving A's confirmation message.

#### Connection Termination: Four-way Handshake

1. A sends a termination request to B

2. B immediately responds that it has received the request of A, but does not sends the termination request to A. Because the server application may have more data to send, control of sending the FIN message is given to the server application.

3. completes sending the remaining data.

4. B sends the termination request to A. 

5. A immediately responds that it has received the request of B and waits for $2$ MSL time before entering the suspension. B changes to the close state after receiving A's confirmation message.

需要 TIME-WAIT 状态，主要是两个原因：防止历史连接中的数据，被后面相同四元组的连接错误的接收；保证「被动关闭连接」的一方，能被正确的关闭；

If "there is no data to send" and "the TCP delayed acknowledgment mechanism is enabled", then the second and third steps of the connection termination handshake will be combined into a single transmission, resulting in a three-step handshake. The TCP delayed acknowledgment mechanism was developed to address the inefficiency of transmitting standalone ACK packets without data. When there is no response data to send, the acknowledgment (ACK) will be delayed for a period to allow any potential response data to be sent together. If, during this delay period waiting to send the ACK, the peer's second data packet arrives, the ACK will be immediately transmitted.

### Retransmission Timeout

### Flow Control: Sliding Window

**防止发送方淹没接收方**。确保接收方有足够的缓冲区处理到达的数据。**接收端的能力** (接收缓冲区大小和处理能力)。**端到端** (Point-to-Point)。在单个发送方和单个接收方之间进行。**触发原因**接收方缓冲区即将或已经耗尽。

- 滑动窗口，接收端所能提供的缓冲区大小, 发送方根据这个数据来计算自己最多能发送多长的数据. 
- 流量控制，主要是接收方传递信息给发送方，使其不要发送数据太快，是一种端到端的控制。主要的方式就是返回的ACK中会包含自己的接收窗口的大小，并且利用大小来控制发送方的数据发送

### Congestion Control

**防止发送方淹没网络**。避免网络链路和路由器因过载而出现拥塞崩溃。**网络的承载能力** (链路带宽、路由器缓冲区等资源)。**网络范围** (Network-Wide)。影响共享同一网络路径的*所有*数据流。网络中出现数据包丢失、延迟显著增加（排队延迟）或显式拥塞通知（ECN）。

 实现复杂的拥塞控制算法（如慢启动、拥塞避免、快速重传、快速恢复）。TCP发送方通过感知丢包（视为拥塞的信号）和测量往返时间（RTT）来动态调整其发送速率（拥塞窗口大小），以在公平性和网络效率之间取得平衡，避免压垮网络。

拥塞窗口 cwnd (congestion window)
当cwnd < ssthresh时，使用慢开始算法。
当cwnd > ssthresh时，改用拥塞避免算法。
当cwnd = ssthresh时，慢开始与拥塞避免算法任意。

* 慢开始  , 不要一开始就发送大量的数据，先探测一下网络的拥塞程度，也就是说由小到大逐渐增加拥塞窗口的大小。
* 拥塞避免  , 加法增大, 乘法减小
* 快重传, 快恢复  



