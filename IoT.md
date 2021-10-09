

[阿里云物联网平台](https://help.aliyun.com/product/30520.html)



提供X.509证书的设备认证机制，支持基于MQTT协议直连的设备使用X.509证书进行认证。

    MQTT,
    GRPC,
    TCP,

使用MQTT、CoAP、HTTPS协议

RFC 7252 Constrained Application Protocol

Prometheus

flyway



提供RRPC和PUB/SUB两种通信模式

设备影子	是一个JSON文档，用于存储设备或者应用的当前状态信息。每个设备都会在云端有唯一的设备影子。无论该设备是否连接到Internet，您都可以使用设备影子通过MQTT协议或HTTP协议获取和设置设备的状态。

MQTT CoAP  HTTP AMQP

https://www.zhihu.com/question/485097906/answer/2107545765

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


https://github.com/Amazingwujun/mqttx

https://github.com/eclipse/mosquitto

gRPC 

OT是Operational Technology,运营技术

# MQTT

消息队列遥测传输  MQTT(Message Queuing Telemetry Transport）

[MQTT Specifications](https://mqtt.org/mqtt-specification/)

* 双向通讯：MQTT 允许设备到云之间以及云到设备之间的消息传递。
* 可靠的消息传递：MQTT 具有3种定义的服务质量级别：0-最多一次，1-至少一次，2-恰好一次，可根据业务场景保证消息传递的可靠性。
* 支持不可靠网络：许多物联网设备通过不可靠的蜂窝网络进行连接。MQTT 对持久性会话的支持减少了将客户端与代理重新连接的时间。
* 安全：MQTT 使您可以轻松地使用 TLS 加密消息并使用现代身份验证协议（例如OAuth）对客户端进行身份验证。


[2020 年常见 MQTT 客户端工具比较](https://www.emqx.com/zh/blog/mqtt-client-tools)

在CONNECT数据包可变头中，包含以下信息：
* 协议名称（Protocol Name）：值固定为字符 “MQTT”。
* 协议版本（Protocol Level）：对 MQTT 3.1.1 来说，该值为 4。
* 用户名标识（User Name Flag）：消息体中是否有用户名字段，1bit，0 或者 1。
* 密码标识（Password Flag）：消息体中是否有密码字段，1bit，0 或者 1。
* 遗愿消息Retain标识（Will Retain）：标识遗愿消息是否是 Retain 消息，1bit，0 或者 1。
* 遗愿消息 QOS 标识（Will QOS）：标识遗愿消息的 QOS，2bit，0、1 或者 2。
* 遗愿标识（Will Flag）：标识是否使用遗愿消息，1bit，0 或者 1。
* 会话清除标识（Clean Session）：标识Client是否建立一个持久化的会话，1bit，0或者1。当该标识设为0时，代表Client希望建立一个持久会话的连接，Broker将存储该Client订阅的主题和未接受的消息，否则Broker不会存储这些数据，同时在建立连接时清楚这个Client之前存在的持久化会话所保存的数据。
* 连接保活（Keep Alive）：设置一个以秒为单位的时间间隔，Client和Broker之间在这个时间间隔之内需要至少一次消息交互，否则Client和Broker会认为它们之间的连接已经断开。

CONNECT数据包的消息体中包含以下数据：
* 客户端标识符（Client Identifier）：Client Identifier 是用来标识 Client 身份的字段，在 MQTT 3.1.1 的版本中，这个字段的长度是 1 到 23 个字节，而且只能包含数字和 26 个字母（包括大小写），Broker 通过这个字段来区分不同的 Client。所以在连接的时候，应该保证 Client Identifier 是唯一的，所以我们可以使用UUID，唯一的设备硬件标识，或者在Android设备中使用的话，可以使用DEVICE_ID等作为Client Identifier的取值来源。MQTT协议中要求Client连接时必须带上Client Identifier，但是也允许Broker在Client Identifier为空时，会为Client分配一个内部唯一的Identifier。如果需要持久化会话的话，那必须为Client设定一个唯一的Identifier。
* 用户名（Username）：如果可变头中的用户名标识设为 1，那么消息体中将包含用户名字段，Broker 可以使用用户名和密码来对接入的 Client 进行验证，只允许已授权的 Client 接入。注意不同的 Client 需要使用不同的 Client Identifier，但它们可以使用同样的用户名和密码进行连接。
* 密码（Password）：如果可变头中的密码标识设为 1，那么消息体中将包含密码字段。
* 遗愿主题（Will Topic）：如果可变头中的遗愿标识设为 1，那么消息体中将包含遗愿主题，当 Client 非正常地中断连接的时候，Broker 将向指定的遗愿主题中发布遗愿消息。
* 遗愿消息（Will Message）：如果可变头中的遗愿标识设为 1，那么消息体中将包含遗愿消息，当 Client 非正常地中断连接的时候，Broker 将向指定的遗愿主题中发布由该字段指定的内容。



会话

https://www.emqx.com/zh/blog/mqtt-session

MQTT 传输的消息可以简化为：主题（Topic）和载荷（Payload）两部分：
* Topic，消息主题，订阅者向代理订阅主题后，一旦代理收到相应主题的消息，就会向订阅者转发该消息。
* Payload，消息载荷，订阅者在消息中真正关心的部分，通常是业务相关

MQTT 报文由三部分组成，分别为：固定报头（Fixed header）、可变报头（Variable header）以及有效载荷（Payload）

https://www.emqx.com/zh/blog/introduction-to-mqtt-qos

MQTT 设计了 3 个 QoS 等级。
* QoS 0：At most once，最多传递一次，因此如果当时客户端不可用，则会丢失该消息。
* QoS 1：At lease once，至少传递一次。
* QoS 2：Exactly once，精确传送一次。

QoS 0 是一种 "fire and forget" 的消息发送模式：Sender (可能是 Publisher 或者 Broker) 发送一条消息之后，就不再关心它有没有发送到对方，也不设置任何重发机制。

QoS 1 包含了简单的重发机制，Sender 发送消息之后等待接收者的 ACK，如果没收到 ACK 则重新发送消息。这种模式能保证消息至少能到达一次，但无法保证消息重复。

QoS 2 设计了重发和重复消息发现机制，保证消息到达对方并且严格只到达一次。


topic

主题过滤器中可以使用通配符，但是主题名不能使用通配符。单层通配符和多层通配符只能用于订阅 (subscribe) 消息而不能用于发布 (publish) 消息，层级分隔符两种情况下均可使用。

井字符号（“#” U+0023）是用于匹配主题中任意层级的通配符。多层通配符表示它的父级和任意数量的子层级。

加号 (“+” U+002B) 是只能用于单个主题层级匹配的通配符。


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


# AVRO

[AVRO](https://avro.apache.org/releases.html)


[thing model definition](https://help.aliyun.com/document_detail/213902.html?spm=a2c4g.11186623.0.0.7bd846a5OR5Bgl)

https://ietf-wg-asdf.github.io/SDF/sdf.html

https://www.ietf.org/archive/id/draft-ietf-asdf-sdf-05.html