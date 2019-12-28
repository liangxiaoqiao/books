### Netty传输
#### Channel
1. 传输API的核心是Channel
2. Channel都会分配一个ChannelPipeline和 ChannelConfig(ChannelConfig包含了Channel的所有设置配置)

##### ChannelHandler的用途:
* 转换数据格式
* 提供异常的通知
* 提供Channel变为活动的或者非活动的通知
* 提供Channel注册或者从EventLoop注销的通知
* 提供用户自定义事件的通知



### ByteBuf
