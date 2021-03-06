#### Netty
##### 基本组件
* Channel  
    传入或者传出数据的载体(可以被打开和关闭,连接或者断开连接)

* 回调  
    回调就是一个方法，一个指向提供给**另外一个方法**的 方法的引用。后者可以在适当的时候调用前者.  
    当一个回调被触发时,相关的事件可以被一个interface-ChannelHandler的实现处理.
    
* Future  
    异步操作结果的占位符，将在未来的某个时刻完成，提供对其结果的访问  
    JDK内置的只能手动检查对应的操作是否已经完成.所以Netty自己实现了ChannelFuture.  
    每一个Netty的出站IO操作都将返回一个ChannelFuture,所以都不会阻塞.

* 事件和ChannelHandler
    入站数据或者相关的状态更改而触发的事件:
    1. 连接已被激活或者连接失活
    2. 数据读取
    3. 用户事件
    4. 错误事件

    出站事件是未来将会触发的某个动作的操作结果:  
    1. 打开或者关闭到远程节点的连接
    2. 将数据写到或者冲刷到套接字

##### 总结
1. ChannelFuture是完全异步的,当调用方法之后会立即返回一个ChannelFuture.
2. 然后代码中对ChannelFuture增加对应的ChannelFutureListener,检查对应的状态之后,那么listener里边的代码会执行.

