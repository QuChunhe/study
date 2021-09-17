    MQTT,
    GRPC,
    TCP,


MQTT、MQTT over WebSocket、CoAP/LwM2M

    消息队列遥测传输  MQTT(Message Queuing Telemetry Transport）

    AMQP

    https://mcxiaoke.gitbooks.io/mqtt-cn/content/mqtt/02-ControlPacketFormat.html

[MQTT协议中文版](https://github.com/mcxiaoke/mqtt)

https://blog.csdn.net/weixin_39080782/article/details/114287532

基于发布/订阅（publish/subscribe）模式
构建于TCP/IP协议上

M

https://github.com/emqx/emqx

https://blog.csdn.net/myyhtw/article/details/114041042


最低有效位（the least significant bit，lsb）是指一个二进制数字中的第0位（即最低位）

最高有效位（the Most Significant Bit，msb），是指一个n位二进制数字中的n-1位

LSB（全大写）有时也指Least Significant Byte，指多字节序列中最小权重的字节。

MSB（全大写）有时也指the Most Significant Byte，指多字节序列中具有最大权重的字节。

Packet Identifie

https://github.com/moquette-io/moquette

https://github.com/Wizzercn/MqttWk

https://github.com/daoshenzzg/socket-mqtt


gRPC 

OT是Operational Technology,运营技术

# MQTT

消息队列遥测传输  MQTT(Message Queuing Telemetry Transport）


* 双向通讯：MQTT 允许设备到云之间以及云到设备之间的消息传递。
* 可靠的消息传递：MQTT 具有3种定义的服务质量级别：0-最多一次，1-至少一次，2-恰好一次，可根据业务场景保证消息传递的可靠性。
* 支持不可靠网络：许多物联网设备通过不可靠的蜂窝网络进行连接。MQTT 对持久性会话的支持减少了将客户端与代理重新连接的时间。
* 安全：MQTT 使您可以轻松地使用 TLS 加密消息并使用现代身份验证协议（例如OAuth）对客户端进行身份验证。


[2020 年常见 MQTT 客户端工具比较](https://www.emqx.com/zh/blog/mqtt-client-tools)

会话

https://www.emqx.com/zh/blog/mqtt-session

MQTT 传输的消息可以简化为：主题（Topic）和载荷（Payload）两部分：
* Topic，消息主题，订阅者向代理订阅主题后，一旦代理收到相应主题的消息，就会向订阅者转发该消息。
* Payload，消息载荷，订阅者在消息中真正关心的部分，通常是业务相关

MQTT 报文由三部分组成，分别为：固定报头（Fixed header）、可变报头（Variable header）以及有效载荷（Payload）

https://www.emqx.com/zh/blog/introduction-to-mqtt-qos

MQTT 设计了 3 个 QoS 等级。
* QoS 0：消息最多传递一次，如果当时客户端不可用，则会丢失该消息。
* QoS 1：消息传递至少 1 次。
* QoS 2：消息仅传送一次。

QoS 0 是一种 "fire and forget" 的消息发送模式：Sender (可能是 Publisher 或者 Broker) 发送一条消息之后，就不再关心它有没有发送到对方，也不设置任何重发机制。

QoS 1 包含了简单的重发机制，Sender 发送消息之后等待接收者的 ACK，如果没收到 ACK 则重新发送消息。这种模式能保证消息至少能到达一次，但无法保证消息重复。

QoS 2 设计了重发和重复消息发现机制，保证消息到达对方并且严格只到达一次。

## Control Package 控制包

CONNECT CONNACK PUBLISH PUBACK PUBREC PUBREL PUBCOMP SUBSCRIBE SUBACK UNSUBSCRIBE UNSUBACK PINGREQ PINGRESP DISCONNECT AUTH


### CONNECT

清理会话 Clean Session

遗嘱标志 Will Flag


https://www.emqx.com/zh/blog/mqtt5-enhanced-authentication

增强认证中，认证方法通常为 SASL（ Simple Authentication and Security Layer ) 机制，

增强认证是基于 CONNECT 报文、CONNACK 报文以及 AUTH 报文三种 MQTT 报文类型实现的，三种报文都需要携带认证方法与认证数据达成双向认证的目的。


[请求响应 - MQTT 5.0 新特性](https://www.emqx.com/zh/blog/mqtt5-request-response)

与 HTTP 的请求响应模式不同，MQTT 的请求响应是异步的，这带来了一个问题，即响应消息与请求消息如何关联。最常用的办法就是在请求消息中携带一个特征字段，响应方在响应时将收到的字段原封不动地返回，请求方在收到响应消息时就可以根据其中的特征字段来匹配相应的请求。很显然 MQTT 也是这么考虑的，所以为 PUBLISH 报文新增了一个 对比数据（Correlation Data） 属性。


# gRPC

https://zhuanlan.zhihu.com/p/363672930

我们可以大致了解下gRPC的通信流程：
1. gRPC通信的第一步是定义IDL，即我们的接口文档（后缀为.proto）
2. 第二步是编译proto文件，得到存根（stub）文件，即上图深绿色部分。
3. 第三步是服务端（gRPC Server）实现第一步定义的接口并启动，这些接口的定义在存根文件里面
4. 最后一步是客户端借助存根文件调用服务端的函数，虽然客户端调用的函数是由服务端实现的，但是调用起来就像是本地函数一样。
