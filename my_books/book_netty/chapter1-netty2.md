#### Neety应用程序
#### 引导服务器
1. 绑定监听并接受传入连接请求的端口
2. 配置Channel,将有关的信息通知给ChannelHandler实例.

```java
@ChannelHandler.Sharable //标记一个channelhandler 可以被多个channel安全共享
public class EchoServerHandler extends ChannelInboundHandlerAdapter {

    //1. channel read 对于每一个传入的消息都要调用
    @Override
    public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
        ByteBuf in = (ByteBuf) msg;
        System.out.println("Server Received:" + in.toString(CharsetUtil.UTF_8));
        ctx.write(in);
    }

    //2. 通知ChannelInboundHandler最后一次对channelRead()的调用是当前批量读取中的最后一条消息
    @Override
    public void channelReadComplete(ChannelHandlerContext ctx) throws Exception {
        ctx.writeAndFlush(Unpooled.EMPTY_BUFFER).addListener(ChannelFutureListener.CLOSE);
    }

    //3. 在读取操作期间,有异常抛出时会调用
    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) throws Exception {
        cause.printStackTrace();
        ctx.close();
    }
}
```

#### 服务器实现的重要步骤
1. EchoServerHandler实现了业务逻辑
2. 创建**ServerBootstrap**的实例,引导和绑定服务器
3. 创建并分配**NioEventLoopGroup**实例进行时间的处理(接受新连接以及读写数据)
4. 指定服务器绑定的本地的**InetSocketAddress**
5. 使用EchoServerHandler的实例,初始化每一个新的Channel
6. 调用**ServerBootstrap.bind**方法以绑定服务器
```java
    final EchoServerHandler serverHandler = new EchoServerHandler();
    EventLoopGroup group = new NioEventLoopGroup();
    try {
        ServerBootstrap serverBootstrap = new ServerBootstrap();
        serverBootstrap.group(group)
                .channel(NioServerSocketChannel.class)
                .localAddress(new InetSocketAddress(port))
                .childHandler(new ChannelInitializer<SocketChannel>() {
                    @Override
                    protected void initChannel(SocketChannel ch) throws Exception {
                        ch.pipeline().addLast(serverHandler);
                    }
                });
        ChannelFuture channelFuture = serverBootstrap.bind().sync();
        channelFuture.channel().closeFuture().sync();
    } finally {
        group.shutdownGracefully().sync();
    }
```
#### 客户端
1. 连接到服务器
2. 发送一个或者多个消息
3. 对于每个消息,等待并接收从服务器发回的相同的消息
4. 关闭连接

#### 步骤
1. 初始化,建立一个**BootStrap**实例
2. 创建分配一个**NioEventLooGroup**,处理包括创建新的连接以及处理入站和出站数据
3. 建立一个到服务器的**InetSocketAddress**实例
4. 连接建立时,一个**ChannelHandler**实例会被安装到(该Channel的)ChannelPipeline中
5. 设置完成后, **Bootstrap.connect** 方法连接到远程节点
```java
@ChannelHandler.Sharable
public class EchoClientHandler extends SimpleChannelInboundHandler<ByteBuf> {

    // 在到服务器的连接已经建立之后将被调用
    @Override
    public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
        ctx.writeAndFlush(Unpooled.copiedBuffer("Netty clients!", CharsetUtil.UTF_8));
    }

    // 当从服务器接收到一条消息时被调用
    @Override
    protected void channelRead0(ChannelHandlerContext ctx, ByteBuf msg) throws Exception {
        System.out.println("Client Received:" + msg.toString(CharsetUtil.UTF_8));
    }

    // 在处理过程中引发异常时被调用
    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) throws Exception {
        cause.printStackTrace();
        ctx.close();
    }

}




public class EchoClient {
    private final String host;
    private final int port;

    public EchoClient(String host, int port) {
        this.host = host;
        this.port = port;
    }

    public static void main(String[] args) throws Exception {
        if (args.length != 2) {
            System.err.println("Usage:" + EchoClient.class.getSimpleName() + " <host><port>");
        }
        String host = args[0];
        int port = Integer.parseInt(args[1]);
        new EchoClient(host, port).start();
    }

    private void start() throws Exception {
        EventLoopGroup group = new NioEventLoopGroup();
        try {
            Bootstrap bootstrap = new Bootstrap();
            bootstrap.group(group)
                    .channel(NioSocketChannel.class)
                    .remoteAddress(new InetSocketAddress(host, port))
                    .handler(new ChannelInitializer<SocketChannel>() {

                        @Override
                        protected void initChannel(SocketChannel ch) throws Exception {
                            ch.pipeline().addLast(new EchoClientHandler());
                        }
                    });
            ChannelFuture future = bootstrap.connect().sync();
            future.channel().closeFuture().sync();
        } finally {
            group.shutdownGracefully().sync();
        }
    }
}
```