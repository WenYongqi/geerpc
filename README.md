# gee-rpc
gee-rpc是一个golang实现的简易的rpc框架
## 特性
- 协议交换(protocol exchange)支持使用不同的序列化协议，可扩展性较好，这里默认使用go自带的`encoding/gob`
- 客户端支持异步和并发
- 拥有连接超时和服务端处理超时的处理机制
- 支持 HTTP 协议，基于 HTTP 实现一个简单的 Debug 页面
- 通过随机选择和 Round Robin 轮询调度算法实现服务端负载均衡
- 实现注册中心，支持服务注册、接收心跳等功能，客户端实现基于注册中心的服务发现机制
## 目录结构
```txt
---codec/
    |---codec.go            定义编码解码器接口Codec（包括读写关闭方法）和相关常量
    |---gob.go              实现gob类型的编解码器实例GobCodec
---main/                
    |---main.go             程序入口
---main-http/
    |---main.go             支持http协议、debug页面的一个示例
---registry/            
    |---registry.go         注册中心，包含服务注册，发送/接收心跳，返回可用服务器列表
---xclient/
    |---discovery.go        一个简易的服务发现模块，采用负载均衡策略，已实现随机选择和 Round Robin 轮询调度算法
    |---discovery_gee.go    较完善的服务发现模块，定期更新可用服务器列表，负载均衡等复用discovery.go的
    |---xclient.go          一个支持负载均衡的rpc客户端，支持访问单个实例和广播，其余复用client.go
---client.go                rpc客户端
---debug.go                 一个简单的debug页面
---server.go                rpc服务端
---service.go               利用反射实现服务、方法的注册以及调用
```
