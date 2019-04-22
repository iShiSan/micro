# ch07

- go-micro
- gin
- etcd
- zipkin

![Image text](https://github.com/1819997197/micro/blob/master/dcxt/dcxt.png)

gin作为bff层，主要用它的路由功能，对外提供http接口

go-micro作为一个成熟的微服务框架提供服务，外部不可访问


## Usage

Run order service
```
make build
./order  --registry=etcdv3
```

Run user service
```
make build
./user  --registry=etcdv3
```

Run payservice
```
make build
./pay  --registry=etcdv3
```

Run api
```
make build
./api
```

Run
```
//curl或者postman
curl http://127.0.0.1:8080/
```

Zipkin
```
http://127.0.0.1:9411/zipkin
```

zipkin架构图


zipkin的基础架构一共包括4个核心组件
- collector：收集器组件，主要用于收集每个服务发送过来的信息，并将这些信息转换为zipkin内部处理的span格式，方便存储、分析、展示。
- storage：存储组件，支持内存和数据库存储（mysql、elasticsearch等）(默认：内存)
- restful API：API组件，提供了外部访问接口，方便自定义功能开发，如监控等
- Web UI：UI组件，基于API实现，方便查看跟踪信息

关于zipkin的几个核心概念
- Span：一个client服务从发出请求到被响应的过程称为span
- Trace：client发出请求到完成处理，中间会经历一个调用链，这个过程称为一个调用链追踪
- Transport：采集信息的传方式，最简单的http方式，高并发可以换成消息队列方式，如kafka(默认：http方式)
