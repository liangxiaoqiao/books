## 传输层

### 运输层服务

1. 运输层协议：TCP UDP
1. 运输层协议为运行在不同主机上的应用进程之间提供了 **逻辑通信** 功能。运行不同进程的主机好像直接相连一样。
1. **运输层协议是在端系统中而不是在网络路由器中实现的**。

    ```
    在发送方，运输层将接收到的来自发送应用进程的报文转换成运输层分组，报文段（segment）。
    可能的方法是，将应用报文划分为较小的块，并为每块加上一个运输层首部来创建运输层报文段。
    在发送方端系统中运输层将这些报文段传递给网络层，网络层将其封装成网络层分组（一个数据报）并向目的地发送。

    网络路由器仅作用于该数据报的网络层字段，即他们不检查封装在该数据报的运输层报文段的字段。

    接收方，网络层从数据报中提取运输层报文段，并将该报文段向上交给运输层。运输层则处理接收到的报文段，使得接收方应用进程可以用该报文段中的数据。
    ```

1. **运输层为运行在不同主机上的进程之间提供了逻辑通信，而网络层则提供了主机之间的逻辑通信。这种差别虽然细微，但很重要。**

    ```
    运输层是与应用层交互的，对应的是不同的进程，所以运输层为运行在不同主机上的进程之间提供了逻辑通信。
    网络层是传递运输层报文段，不针对每一个主机的某个进程，所以是网络层提供的是主机之间的逻辑通信。
    ```

1. 简单介绍网络层

    ```
    IP协议全称网际协议。IP为主机之间提供了逻辑通信。IP的服务模型是尽力而为交付服务（并不做任何确保）。因此，IP被称为不可靠服务。
    ```

1. 将主机间交付扩展到进程间交付，称为 **运输层的多路复用** 和 **多路分解**。
1. TCP为应用提供的附加服务：

    ```
    可靠数据传输 :通过使用流量控制、序号、确认和定时器等技术。
    拥塞控制：防止任何一条TCP连接用过多流量来淹没通信主机之间的链路和交换设备。
    ```

### 多路复用与多路分解

1. 多路复用与多路分解 也就是将网络层所提供的主机到主机交付服务扩展到为主机上运行的应用程序所提供的进程到进程交付服务。

    ```
    多路分解：每个运输层报文段中设置了接字段。在接收端，运输层检查这些字段并标识出接收套接字，然后将报文段定向到该套接字，将运输层报文段中的数据交付到正确的套接字的工作称为多路分解。

    多路复用：从源主机的不同套接字中收集数据块，并为每个数据块封装上首部信息从而生成报文段，然后将报文段传递到网络层的工作称为多路复用。
    ```

    ```
    套接字有唯一标识符。
    每个报文段有特殊字段（源端口号字段 和 目的端口号字段）来指示该报文段所要交付的套接字。
    ```

    *0-1023范围的端口号是 周知端口号。是受严格限制的。*

    ```
    工作原理：主机上的每个套接字被分配一个端口号，当报文段到达主机时，运输层检查报文段中的目的端口号，并将其定向到相应的套接字。
    ```

1. 无连接的多路复用和多路分解

    ```
    创建一个UDP套接字时，运输层自动地为该套接字分配一个端口号（运输层从范围1024-65535内分配一个主机尚未使用的UDP端口号）。也可以为UDP套接字指派一个特定的端口号。
    典型的情况是：应用程序的客户机端让运输层自动地（并且透明）分配端口号，而服务器端则分配一个特定的端口号。
    ```

    UDP套接字是由一个包含**目的IP地址和目的端口号** 的**二元组**来全面标识的。

    *因此，如果两个UDP报文段有不同的源IP地址和/或源端口号，但是具有相同的目的IP地址和目的端口号，那么这两个报文段将通过相同的目的套接字定向到相同的目的进程。*

1. 面向连接的多路复用与多路分解

    ```
    TCP套接字与UDP套接字的细微差别：
    ```

    TCP套接字是由一个**四元组（源IP地址，源端口号，目的IP地址，目的端口号）** 来标识的。
    *因此，两个具有不同源地址或源端口号的到达的TCP报文段将被定向到两个不同的套接字，除非TCP携带了初始创建连接的请求。*

    ```
    新创建的套接字通过这4个值来标识，所有后续到达的报文段，如果他们的 四元组 都与这4个值匹配，则被多路分解到这个套接字。
    ```

