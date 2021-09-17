
ChannelInboundHandlerAdapter为ChannelInboundHandler提供了默认实现
* channelRead()—Called for each incoming message
* channelReadComplete()—Notifies the handler that the last call made to channelRead() was the last message in the current batch
* exceptionCaught()—Called if an exception is thrown during the read operation


Architecturally, ChannelHandlers help to keep your business logic decoupled from networking code.

性能上从低到高如下：
* OioSocketChannel：传统，阻塞式编程。
* NioSocketChannel：select/poll或者epoll，jdk 7之后linux下会自动选择epoll。epoll原理及与select/poll的伸缩性性能测试基准
* EpollSocketChannel：epoll，仅限linux，提供更多额外选项。
* EpollDomainSocketChannel：ipc模式，仅限客户端、服务端在相同主机的情况，从4.0.26版本开始支持

Epoll.isAvailable()用来判断是否支持Netty 自己设置的EpollServerSocketChannel