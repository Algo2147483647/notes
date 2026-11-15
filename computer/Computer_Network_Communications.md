# Computer Network Communications

[TOC]

## Context

超大规模的计算机网络之间的通信模型.

## Resolution

### Computer network layering models

**Computer network layering models** employ a design philosophy of layered abstraction, achieving inter-layer decoupling, independent encapsulation of functionality within each layer, and promoting standardization.

- **Layered abstraction**: Single responsibility principle, each layer only solves one type of problem. Each layer interacts only with adjacent layers via well-defined interfaces, hiding implementation details. Lower layers provide services to upper layers. Breaks down complex networking tasks into smaller, manageable layers, with each layer handling a specific function.
- **Inter-layer decoupling**: Layers can be updated or replaced independently. This enables flexibility and fosters innovation.
- **Peer-to-Peer Communication**: The $N$-th layer of the sender only talks to the $N$-th layer of the receiver. Data must be passed down layer by layer, transmitted through the physical medium, and parsed up layer by layer at the receiving end.
- **Standard interface**: Protocols at each layer adhere to standardized specifications, ensuring interoperability between diverse hardware and software vendors.
- **Encapsulation**: When data is passed from top to bottom, each layer adds its own control header to form a new data unit.



Detailed description of each layer in computer network layering model:

- **Application Layer**: Provides service required by users. This lawyer directly addresses user needs, offering interfaces  for applications to assess network service. It encompasses network application protocols directly used by users (e.g., HTTP, FTP, SMTP).
- **Presentation Layer**: Ensures data can be correctly interrupted. This layer resolves data compatibility issues between heterogeneous systems (e.g., communication between a Windows program and a Linux server). It handles the syntax and semantics of information exchanged between communication systems, performing data format transformation (e.g., encryption, compression, encoding conversion), ensuring data sent from the source host's application layer can be correctly by the destination host's application layer. 
- **Session Layer**: Organizes and manages communication sessions. This layer is responsible for establishing ,managing and terminating sessions between application processes. It manages long term interactive tasks, Prize session Synchronization and dialogue control.
- **Transport Layer**: Ensures end-to-end communication between processes. This layer is responsible for implementing reliable or unreliable data transfer, flow control, and error control between application processes on the source and destination hosts, compensating for the potential unreliable of the network layer below.
- **Network Layer**: Facilitates packet transmission across networks. This layer is responsible for the path selection (routing) and logical addressing of packets traveling from a source host across multiple networks to a destination host. It handles the interconnection and interpretability between different networks.
- **Data-link Layer**: Ensures reliable data transmission over a single network link. This layer provides reliable data transmission between two directly connected nodes on the same physical network segment. It organizes the raw bit stream received from our physical layer into frame, performing frame delimitation, synchronization, error detection, flow control, and media access control. It shields the upper layer from the differences in the underlying physical media.
- **Physical layer**:  Transmits raw bit streams over physical media. this layer defines electrical, mechanical, timing, and functional interface specifications, handling the sending and receiving of bits.

> Open Systems Interconnection (OSI) (7 Layers): A theoretical reference model proposed by the International Organization for Standardization (ISO). It defines a complete framework for network communication, divided into seven layers. Although there are few protocol stacks that fully follow OSI in practice, it is the gold standard for understanding network concepts and protocol functions.
> * Application Layer
> * Presentation Layer
> * Session Layer
> * Transport Layer
> * Network Layer
> * Data-link Layer
> * Physical layer
>
> Transmission Control Protocol/Internet Protocol (TCP/IP) (4 Layers): The protocol stack that actually runs on the Internet. It was developed by the US Department of Defense ARPANET project and is the cornerstone of the Internet. It is simpler and more implementation-focused than the OSI model.
> * Application Layer
> * Transport Layer
> * Network Layer
> * Local Access Layer
>
> Comprehensive Model: A compromise model that combines the clear layering idea of the OSI model and the practical protocol stack of the TCP/IP model is formed to facilitate teaching and understanding.
> * Application Layer
> * Transport Layer
> * Network Layer
> * Data-link Layer
> * Physical layer

### Physical Layer

Equipment: Hub

### Data-link Layer

* MTU
* MAC Address: (每个设备都有唯一且不变的MAC Address)

Equipment: Switch

只发给目标 MAC地址指向的那台电脑.

### Network Layer

Equipment: Router

作为一台独立的拥有 MAC 地址的设备, 并且可以帮助把数据包做一次转发. (Router每一个端口, 都有独立MAC地址)

* 子网划分、子网掩码

Protocol

  * **IP (Internet Protocol)**

  * **ICMP (Internet Control Message Protocol)**

  * **ARP (Address Resolution Protocol)**

  * **RARP (Reverse Address Resolution Protocol)**

### Transport Layer

Protocol

- UDP (User Datagram Protocol)
- TCP (Transmission Control Protocol)

UDP (User Datagram Protocol)

* UDP datagram header

  | Bit   | 意义             |
  | ----- | ---------------- |
  | 0-15  | Source port      |
  | 16-31 | Destination port |
  | 32-47 | Length           |
  | 48-63 | Checksum         |
  |       |                  |

* Application: 使用UDP的协议

  * DNS
  * TFTP
  * SNMP
  * NFS

TCP (Transmission Control Protocol)


### Application Layer

* 数据传输基本单位为报文

Protocol

  * **FTP (File Transfer Protocol)**

  * **Telnet**

  * **DNS (Domain Name System)**

  * **SMTP (Simple Mail Transfer Protocol)**

  * **POP3 (Post Office Protocol - Version 3)**

  * **HTTP (Hyper Text Transfer Protocol)**


HTTP (Hyper Text Transfer Protocol)

* Format

  - GET：请求读取由URL所标志的信息
  - POST：给服务器添加信息（如注释）
  - PUT：在给定的URL下存储一个文档
  - DELETE：删除给定的URL所标志的资源

* HTTP 状态码  

  | Code | Description                                    |
  | ---- | ---------------------------------------------- |
  | 1**  | 信息, 服务器收到请求, 需要请求者继续执行操作   |
  | 100  | Continue                                       |
  | 101  | Switching Protocols                            |
  |      |                                                |
  | 2**  | 成功, 操作被成功接收并处理                     |
  | 200  | OK                                             |
  | 201  | Created                                        |
  | 202  | Accepted                                       |
  | 203  | Non-Authoritative Information                  |
  | 204  | No Content                                     |
  | 205  | Reset Content                                  |
  | 205  | Reset Content                                  |
  |      |                                                |
  | 3**  | 重定向,需进一步操作以完成请求                  |
  | 301  | Moved Permanently                              |
  |      |                                                |
  | 4**  | 客户端错误,请求包含语法错误或无法完成请求      |
  | 400  | Bad Request                                    |
  | 401  | Unauthorized                                   |
  | 403  | Forbidden                                      |
  | 404  | Not Found                                      |
  | 404  | Method Not Allowed                             |
  |      |                                                |
  | 5**  | 服务器错误, 服务器在处理请求的过程中发生了错误 |
  | 500  | Internal Server Error                          |
  |      |                                                |


  * **HTTP (Hyper Text Transfer Protocol over Secure Socket Layer)**

  * **Cookie / Session**

***Q: What happens when you click on a URL in your browser?***

[TCP](./TCP.md)

## Include

- [Remote_Procedure_Call](./Remote_Procedure_Call.md)

- [Message_Queue](./Message_Queue.md)

- [Transmission Control Protocol](./Transmission Control Protocol.md)

