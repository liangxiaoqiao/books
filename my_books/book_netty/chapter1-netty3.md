#### Netty的组件
Channel EventLoop ChannelFuture
ChannelHandler ChannelPipeline
##### Channel接口
1. 基本的IO操作(bind() connect() read() write())依赖于**底层网络传输所提供的源语**
2. Java原生的网络编程中,基本构造是class Socket
3. Netty的Channel接口提供的API降低了复杂性
4. EmbeddedChannel,LocalServerChannel, NioDatagramChannel, NioSctpChannel, NioSocketChannel
#### EventLoop接口
EventLoop定义了Netty的核心抽象
1. EventLoopGroup 包含多个 EventLoop
2. EventLoop只与一个Thread绑定
3. EventLoop可能会分配给多个Channel
4. Channel只会注册于一个EventLoop
5. EventLoop处理的IO事件都在专有的Thread上被处理
所以说: 一个Channel 多对一 EventLoop 一对一 Thread  
EventLoopGroup 多对一 EventLoop 一对多 Channel
#### ChannelFuture接口
Netty所有IO都是异步的, addListener()方法注册了一个**ChannelFutureListener**,以便在某个操作完成时得到通知.

